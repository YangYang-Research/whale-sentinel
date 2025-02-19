# Whale Sentinel (WS) Design Board

## Whale Sentinel Solution



## High Level Architecture

![High Level Architecture](https://github.com/noobpk/whale-sentinel/blob/main/diagrams/WS_High_Level_Architecture.png?raw=true)

### Scope 

| **No.** | **System**            | **Service Name**                 | **Description**                                                                                           |
|---------|-----------------------|----------------------------------|-----------------------------------------------------------------------------------------------------------|
| 1       | **WS Web Agent**      | **Python Agent**                | A Python-based agent designed for seamless integration with Flask and Django applications, providing logging, monitoring, and security features. |
| 2       |                       | **Java Agent**                  | A Java-based agent optimized for integration with Spring Boot applications, enabling enhanced performance monitoring and secure communications. |
| 3       | **WS Service**        | **WS Module Web Attack Detection** | An AI-driven module designed to detect and mitigate web-based attacks in real time, offering robust protection against threats like SQL injection and XSS. |
| 4       |                       | **WS Module Logg**              | A centralized log collection and analysis module that gathers, processes, and forwards logs to Elasticsearch for real-time monitoring and analytics. |
| 5       |                       | **WS Module Sync Configuration** | A module ensuring real-time synchronization of configuration changes across all connected agents and systems, minimizing downtime and inconsistencies. |
| 6       | **WS Controller**     | **WS Dashboard**                | A user-friendly frontend interface for monitoring, managing, and visualizing system data, providing real-time insights and actionable metrics. |
| 7       |                       | **WS Controller Service**       | The backend service powering the WS Dashboard, responsible for processing requests, managing system logic, and integrating with external APIs. |
| 8       |                       | **WS Module ELK Integration**   | A service designed to streamline the integration between WS systems and the ELK stack, ensuring seamless log forwarding, indexing, and visualization. It connects **WS Module Logg** to **Elasticsearch** via Logstash and provides dashboards and visualizations through Kibana. |
| 9       | **Data Stores**       | **MongoDB /. Amazon DynamoDB**   | A highly scalable NoSQL database solution used for storing configuration data, agent metadata, and other structured records. |
| 10      |                       | **Redis / AWS ElastiCache**     | A high-performance in-memory data store for caching frequently accessed data, ensuring low latency and high throughput for WS systems. |
| 11      | **Messaging**         | **Kafka / MSK Topics**          | A distributed messaging system (Apache Kafka or Amazon MSK) used for reliable message streaming between modules and agents. |

## WS-Web Agent Architecture

The WS-Web Agent Architecture is designed for integration with web framework like Flask, Spring Boot, ..., providing logging, monitoring, and security features. Following LangSec principles ensures that all input handling routines are formal language recognizers, strictly validating inputs to mitigate security risks.

![WS-Web Agent](https://github.com/noobpk/whale-sentinel/blob/main/diagrams/WS_Web_Agent_Architecture.png?raw=true)

## WS-Deep Learning Model Web Attack Detection 

![WS-Model Detection](https://github.com/noobpk/whale-sentinel/blob/main/diagrams/WS_Deep_Learning_Model_Web_Attack_Detection.png?raw=true)

## WS-Web Agent - AWS Deployment Architecture

This is a detection method that using combine Convolutional Neural Network (CNN) and a family of Recurrent Neural Network (RNN) to analyze features and relationships in requests from users and predict whether they are attack or not.

![WS-Web Agent AWS](https://github.com/noobpk/whale-sentinel/blob/main/diagrams/WS_Web_Agent_AWS_Deployment_Architecture.png?raw=true)

### Conection table

| **No.** | **Source**         | **IP**             | **Destination**            | **IP**                  | **Port** | **Protocols**   | **Purpose**                                                                 | **Number of IPs Assigned** |
|---------|--------------------|--------------------|----------------------------|-------------------------|----------|-----------------|-----------------------------------------------------------------------------|---------------------------|
| 1       | **WS Web Agent**    | 10.0.0.0/22        | **WS Service**             | 10.0.4.0/22             | 443      | HTTPS, TLS 1.2  | Connection between WS Web Agent and WS Service for secure communication, enabling logging, monitoring, and web attack detection. | 1024                      |
| 2       | **WS Service**      | 10.0.4.0/22        | **WS Controller**          | 10.0.8.0/28             | 443      | HTTPS, TLS 1.2  | Communication between WS Service and WS Controller to transmit monitoring data, system alerts, and control configurations. | 1024                      |
| 3       | **WS Service**      | 10.0.4.0/22        | **Kafka**                  | 10.0.12.0/24            | 9080     | HTTPS, TLS 1.2  | Enable secure, high-throughput data streaming between WS Service and Kafka, ensuring reliable message queuing and processing. | 1024                      |
| 4       | **WS Controller**   | 10.0.8.0/28        | **Database MongoDB / Amazon DynamoDB** | 10.0.16.0/24            | 27017 / 8000 | HTTPS, TLS 1.2  | Secure connection from WS Controller to the database for accessing and storing configuration, monitoring logs, and application data. | 16                        |
| 5       | **Kafka / MSK**     | 10.0.12.0/24       | **WS Controller**          | 10.0.8.0/28             | 9080     | HTTPS, TLS 1.2  | Kafka communicates with WS Controller to push data such as logs, messages, and event triggers for further analysis and processing. | 256                       |
| 6       | **WS Controller**   | 10.0.8.0/28        | **WS Service**             | 10.0.4.0/22             | 443      | HTTPS, TLS 1.2  | WS Controller communicates with WS Service to manage service configurations, control system states, and update monitoring parameters. | 16                        |

## Security

### Application

Implementing Language-theoretic Security (LangSec) in application development involves designing input-handling routines as formal language recognizers, ensuring that all inputs are strictly validated and parsed according to well-defined grammars, thereby mitigating vulnerabilities and enhancing overall security.

- All data is validated at both the frontend and backend.
  - Text input / output
    - All data is validated at both the frontend and backend, and special characters are filtered and removed. ``!` @ # $ % ^ & * () - _ = + { } [ ] | \ : ; " ' < > , . ? / ~ \``
    - Use prepared statements (also known as parameterized queries) to prevent SQL Injection.
    - Ensure data is encoded before it is sent back to the application.
    - Do not display detailed error messages in the application. Instead, show a general error message or redirect users to an error page.
    - Masking sensitive information, such as passwords and personally identifiable information (PII).
  - File upload
    - Whitelist file extensions (e.g., pdf, png, jpg, etc.).
    - Check the end of the file name string against the whitelist to validate the file extension.
    - Check the metadata header of the file to validate the file type.
    - Check the file size does not exceed 25MB.
    - Create a random name for the file before saving it.
    - Save the file to the specified directory.
-  Check authentication and authorization before performing any action.
-  Use the GET method to retrieve data and the POST method to update data.

### Network 

- By default, deny all connections. Allow connections only when needed.
- All connections are encrypted in transit using HTTPS and at least TLS 1.2 for secure communication.
- Use SFTP with TLS 1.2 or above for file transfers.
<!-- - Use CCA (CLient Certificate Authentication) for ... -->


### Data

- Classify and label sensitive information, such as passwords and personally identifiable information (PII).
- Enable data encryption features when storing data on AWS services such as RDS, S3, ElastiCache, ..., or other cloud services.
- Encrypt all backup data.

### Cryptography

- Implement strong cryptographic practices.
  - Strong Hash Algorithms : SHA-256, SHA-3, BLAKE2, BLAKE2.
  - Strong Encryption Algorithms : AES 256, RSA 2048, ECC.
- Use AES256 to encryption E2E message with sensitve data when transfer.
- Use PGP to encryption file when tranfer.
- Use SHA256withRSA for request signing.
- Use JWT with RS256 (RSA Signature with SHA-256) for REST API authentication with a secret key length of 2048 bits or RSA 2048 for public and private keys.
- Follow the X.509 Version 3 Certificate format for certificates.

## Automation 

### DevSecOps 

Implementing DevSecOps in application development involves integrating security practices into the DevOps workflow, ensuring that security is considered at every stage of the software development lifecycle, from planning and coding to testing, deployment, and maintenance.

![DevSecOps](https://github.com/noobpk/whale-sentinel/blob/main/diagrams/WS_DevSecOps_Architecture.png?raw=true)

### MLSecOps

Implementing MLSecOps in developing and training AI models involves integrating security practices into the machine learning lifecycle, ensuring that data, models, and infrastructure are protected at every stage, from data collection and preprocessing to model training, deployment, and monitoring.

![MLSecOps](https://github.com/noobpk/whale-sentinel/blob/main/diagrams/WS_MLSecOps_Architecture.png?raw=true)
