# Whale Sentinel API Document

| **No.** | **System**        | **Service Name**              | **API**                                        | **Description**                                                                                       | **Timeout** | **API Spec** |
|---------|-------------------|-------------------------------|------------------------------------------------|-------------------------------------------------------------------------------------------------------|-------------|--------------|
| 1       | **WS Controllers**  | **WS Controller Service**      | POST /api/v1/ws/controller/login               | Authenticates a user and establishes a session with WS Controller.                                      | 30s         | [Specification Link] |
| 2       | **WS Controllers**  | **WS Controller Service**      | GET /api/v1/ws/controller/logout              | Logs out the user and terminates the active session with WS Controller.                               | 30s         | [Specification Link] |
| 3       | **WS Controllers**  | **WS Controller Service**      | POST /api/v1/ws/controller/agent               | Retrieves a list of registered agents within the WS Controllers system.                                 | 30s         | [Specification Link] |
| 4       | **WS Controllers**  | **WS Controller Service**      | POST /api/v1/ws/controller/agent/create       | Creates a new agent within the WS Controllers system for monitoring and configuration.                 | 30s         | [Specification Link] |
| 5       | **WS Controllers**  | **WS Controller Service**      | POST /api/v1/ws/controller/agent/update       | Updates configuration or status of an existing agent in the WS Controller system.                     | 30s         | [Specification Link] |
| 6       | **WS Controllers**  | **WS Controller Service**      | POST /api/v1/ws/controller/agent/configuration | Fetches the current configuration of a specific agent in the system.                                  | 30s         | [Specification Link] |
| 7       | **WS Controllers**  | **WS Controller Service**      | POST /api/v1/ws/controller/agent/configuration| Updates the configuration of a specific agent in the WS Controllers system.                           | 30s         | [Specification Link] |
| 8       | **WS Services**     | **WS Module Gateway Service** | POST /api/v1/ws/services/gateway | Handles incoming data from agents, validates requests, and routes them to appropriate processing modules for further analysis and execution.| 30s | [Specification Link](https://github.com/YangYang-Research/whale-sentinel-services/issues/2) |
| 9       | **WS Services**     | **WS Module Web Attack Detection** | POST /api/v1/ws/services/web-attack-detection | Submits web traffic data for AI-based prediction and detection of potential web attacks (e.g., SQL Injection, XSS). | 30s         | [Specification Link](https://github.com/YangYang-Research/whale-sentinel/issues/3) |
| 10       | **WS Services**     | **WS Module Web Attack Detection** | GET /api/v1/ws/services/web-attack-detection/ping | This endpoint checks the status of the WS Module Web Attack Detection. | 30s         | [Specification Link](https://github.com/YangYang-Research/whale-sentinel/issues/3) |
| 11       | **WS Services**     | **WS Module Common Attack Detection** | GET /api/v1/ws/services/common-attack-detection | Submits web traffic data for Rule-based detection of potential web attacks (e.g., SQL Injection, XSS). | 30s         | [Specification Link](https://github.com/YangYang-Research/whale-sentinel-services/issues/3) |
| 12       | **WS Services**     | **WS Module Sync Configuration** | POST /api/v1/ws/services/sync-configuration | Synchronizes the configuration from WS Controllers to WS Services and WS Agents to ensure up-to-date rules and settings. | 30s         | [Specification Link] |
| 13       | **WS Services**     | **WS Module DGA Detection** | POST /api/v1/ws/services/dga-detection | Detects domain generation algorithms (DGAs) in network traffic to identify potential malware activity.  | 30s         | [Specification Link](https://github.com/YangYang-Research/whale-sentinel-services/issues/5) |
| 14       | **WS Services**     | **WS Module DGA Detection** | GET /api/v1/ws/services/dga-detection/ping | This endpoint checks the status of the WS Module DGA Detection. | 30s         | [Specification Link](https://github.com/YangYang-Research/whale-sentinel-services/issues/5) |

## HTTP Status Code

| **Status Code** | **Description**                                          |
|------------------|----------------------------------------------------------|
| 200              | Success: The request was successfully processed.         |
| 400              | Bad Request: The server could not understand the request due to invalid syntax. |
| 401              | Unauthorized: Authentication is required and has failed or has not been provided. |
| 403              | Forbidden: The server understands the request but refuses to authorize it. |
| 404              | Not Found: The requested resource could not be found.    |
| 405              | Method Not Allowed: The method specified in the request is not allowed for the resource. |
| 408              | Request Timeout: The server timed out waiting for the request. |
| 500              | Internal Server Error: The server encountered an unexpected condition that prevented it from fulfilling the request. |
| 502              | Bad Gateway: The server, while acting as a gateway or proxy, received an invalid response from the upstream server. |
| 503              | Service Unavailable: The server is currently unable to handle the request due to a temporary overload or maintenance. |
| 504              | Gateway Timeout: The server, while acting as a gateway or proxy, did not receive a timely response from the upstream server. |