# Whale Sentinel Technology Stack

## Whale Sentinel Controllers

| .No | Component               | Description      | TechStack                              | Integration Capabilities                                                                |
|-----|-------------------------|------------------|----------------------------------------|-----------------------------------------------------------------------------------------|
| 1   | WS Manage Dashboard         | Frontend         | React v19                              | Integrates with the backend via RESTful APIs.                                           |
| 2   | WS Processor   | Backend          | Golang 1.24.0                          | Serves as the core logic layer, integrating with the frontend and WS Module via APIs.   |
| 3   | Database                | NoSQL            | MongoDB 8.0 / Amazon DynamoDB          | Connects to the backend using JDBC for efficient data retrieval and storage.            |
| 4   | WS Monitor Dashboard   | Frontend          | OpenSearch Dashboard                   | Visualziation data from OpenSearch DB.   |
| 5   | OpenSearch DB                | NoSQL            |           | Store log of all services.            |
| 6   | Cache                   | Caching          | Redis / AWS ElastiCache                | Provides high-speed data caching for backend operations.                                |
| 7   | Event Message           | Streaming        | Apache Kafka 3.9.0 / AWS MSK           | Handles real-time data streaming between the WS Module and the backend system.          |
| 8   | Event Message           | Streaming        | Socket.IO 4.x                          | Facilitates bi-directional data streaming between the frontend and the backend system.  |


## Whale Sentinel Services

| .No | Component                       | Description             | TechStack                | Integration Capabilities                                                                            |
|-----|---------------------------------|-------------------------|--------------------------|----------------------------------------------------------------------------------------------------|
| 1   | WS Module Web Attack Detection  | Module for web attack detection using AI models | Python 3.9, TensorFlow, FastAPI   | Integrates with the gateway via APIs to detect web attacks in real-time.                             |
| 2   | WS Module Configuration Service   | Configuration synchronization module | Golang 1.24.0            | Consumes configuration data from the backend and synchronizes it across all WS Modules and agents. |
| 3   | Cache                           | Caching                 | Redis / AWS ElastiCache  | Stores and provides quick access to configuration data for optimized performance.                  |
| 4   | Event Message                   | Streaming               | Apache Kafka 3.9.0 / AWS MSK | Streams real-time data between WS Modules and the backend for efficient communication and updates. |
| 5   | WS Module Gateway Service       | Module for receive and route request from WS Agent to specific WS module | Golang 1.24.0 | Integrates with the agent via APIs. |
| 6   | Fluent-bit       | Get log from service then push to OpenSearch DB. |

## Whale Sentinel Agents

| .No | Component               | Description                  | TechStack                              | Integration Capabilities                                                                |
|-----|-------------------------|------------------------------|----------------------------------------|-----------------------------------------------------------------------------------------|
| 1   | Python Agent            | Agent for Python language    | Flask 3.1.1, Django 5.1.5             | Integrates with WS Modules via APIs to monitor and process Python-based applications.   |
| 2   | Java Agent              | Agent for Java language      | Spring Boot 3.4.1                      | Integrates with WS Modules via APIs to monitor and process Java-based applications.     |
