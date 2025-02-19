# Whale Sentinel Technology Stack

## Whale Sentinel Controller

| .No | Component               | Description      | TechStack                              | Integration Capabilities                                                                |
|-----|-------------------------|------------------|----------------------------------------|-----------------------------------------------------------------------------------------|
| 1   | WS Dashboard            | Frontend         | React v19                              | Integrates with the backend via RESTful APIs.                                           |
| 2   | WS Controller Service   | Backend          | Golang 1.23.5                          | Serves as the core logic layer, integrating with the frontend and WS Module via APIs.   |
| 3   | Database                | NoSQL            | MongoDB 8.0 / Amazon DynamoDB          | Connects to the backend using JDBC for efficient data retrieval and storage.            |
| 4   | Cache                   | Caching          | Redis / AWS ElastiCache                | Provides high-speed data caching for backend operations.                                |
| 5   | Event Message           | Streaming        | Apache Kafka 3.9.0 / AWS MSK           | Handles real-time data streaming between the WS Module and the backend system.          |
| 6   | Event Message           | Streaming        | Socket.IO 4.x                          | Facilitates bi-directional data streaming between the frontend and the backend system.  |


## Whale Sentinel Service 

| .No | Component                       | Description             | TechStack                | Integration Capabilities                                                                            |
|-----|---------------------------------|-------------------------|--------------------------|----------------------------------------------------------------------------------------------------|
| 1   | WS Module Web Attack Detection  | Module for web attack detection using AI models | Python 3.12, TensorFlow   | Integrates with the gateway via APIs to detect web attacks in real-time.                             |
| 2   | WS Module Logg                  | Log collection module   | Golang 1.23.5            | Consumes and centralizes logs from all WS Modules for monitoring and analysis.                     |
| 3   | WS Module Sync Configuration    | Configuration synchronization module | Golang 1.23.5            | Consumes configuration data from the backend and synchronizes it across all WS Modules and agents. |
| 4   | Cache                           | Caching                 | Redis / AWS ElastiCache  | Stores and provides quick access to configuration data for optimized performance.                  |
| 5   | Event Message                   | Streaming               | Apache Kafka 3.9.0 / AWS MSK | Streams real-time data between WS Modules and the backend for efficient communication and updates. |
| 6   | WS Module Gateway Service       | Module for receive and route request from WS Agent to specific WS module | Golang 1.23.5 | Integrates with the agent via APIs. |


## Whale Sentinel Agent 

| .No | Component               | Description                  | TechStack                              | Integration Capabilities                                                                |
|-----|-------------------------|------------------------------|----------------------------------------|-----------------------------------------------------------------------------------------|
| 1   | Python Agent            | Agent for Python language    | Flask 3.1.1, Django 5.1.5             | Integrates with WS Modules via APIs to monitor and process Python-based applications.   |
| 2   | Java Agent              | Agent for Java language      | Spring Boot 3.4.1                      | Integrates with WS Modules via APIs to monitor and process Java-based applications.     |
| 3   | Cache                   | Caching                      | Redis / AWS ElastiCache                | Provides caching for configuration data to optimize performance and reduce latency.     |
| 4   | Event Message           | Streaming                    | Apache Kafka 3.9.0 / AWS MSK           | Enables real-time data streaming between agents and WS Modules for seamless updates.    |

