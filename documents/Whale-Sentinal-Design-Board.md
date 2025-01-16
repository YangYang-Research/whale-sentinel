# Whale Sentinel (WS) Design Board

## Whale Sentinel Solution

- WS-Web Agent
- WS-Mobile Agent

## High Level Architecture

![High Level Architecture](https://github.com/noobpk/whale-sentinel/blob/main/diagrams/WS_High_Level_Architecture.png?raw=true)


## WS-Web Agent Architecture

![WS-Web Agent](https://github.com/noobpk/whale-sentinel/blob/main/diagrams/WS_Web_Agent_Architecture.png?raw=true)

## WS-Web Agent - AWS Deployment Architecture

![WS-Web Agent AWS](https://github.com/noobpk/whale-sentinel/blob/main/diagrams/WS_Web_Agent_AWS_Deployment_Architecture.png?raw=true)

## Security Standard

### Application

Implementing Language-theoretic Security (LangSec) in application development involves designing input-handling routines as formal language recognizers, ensuring that all inputs are strictly validated and parsed according to well-defined grammars, thereby mitigating vulnerabilities and enhancing overall security.

- All data is validated at both the frontend and backend.
  - Input
    - All data is validated at both the frontend and backend, and special characters are filtered and removed. ``!` @ # $ % ^ & * () - _ = + { } [ ] | \ : ; " ' < > , . ? / ~ \``
    - Use prepared statements (also known as parameterized queries) to prevent SQL Injection.
  - Output
    - Ensure data is encoded before it is sent back to the application.
    - Disable debug mode. Do not display detailed error messages in the application. Instead, show a general error message or redirect users to an error page.
    - Masking sensitive information, such as passwords and personally identifiable information (PII).
  - File upload
    - Whitelist file extensions (e.g., pdf, png, jpg, etc.).
    - Check the end of the file name string against the whitelist to validate the file extension.
    - Check the metadata header of the file to validate the file type.
    - Check the file size does not exceed 25MB.
    - Create a random name for the file before saving it.
    - Save the file to the specified directory.
-  Check authentication and authorization before performing any action.

### Network 

- All connections are encrypted in transit using HTTPS and at least TLS 1.2 for secure communication.
- Use SFTP with TLS 1.2 or above for file transfers.
- Use CCA (CLient Certificate Authentication) for ... 


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
- Use RSA for signing and SHA-256 for checksums.
- Use JWT with RS256 (RSA Signature with SHA-256) for REST API authentication with a secret key length of 2048 bits or RSA 2048 for public and private keys.
- Follow the X.509 Version 3 Certificate format for certificates.

### DevSecOps 

Implementing DevSecOps in application development involves integrating security practices into the DevOps workflow, ensuring that security is considered at every stage of the software development lifecycle, from planning and coding to testing, deployment, and maintenance.

![DevSecOps](https://github.com/noobpk/whale-sentinel/blob/main/diagrams/WS_DevSecOps_Architecture.png?raw=true)

### MLSecOps

Implementing MLSecOps in developing and training AI models involves integrating security practices into the machine learning lifecycle, ensuring that data, models, and infrastructure are protected at every stage, from data collection and preprocessing to model training, deployment, and monitoring.

![MLSecOps](https://github.com/noobpk/whale-sentinel/blob/main/diagrams/WS_MLSecOps_Architecture.png?raw=true)
