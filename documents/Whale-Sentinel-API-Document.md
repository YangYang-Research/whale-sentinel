# Whale Sentinel API Document

| **No.** | **System**        | **Service Name**              | **API**                                        | **Description**                                                                                       | **Timeout** | **API Spec** |
|---------|-------------------|-------------------------------|------------------------------------------------|-------------------------------------------------------------------------------------------------------|-------------|--------------|
| 1       | **WS Controller**  | **WS Controller Service**      | POST /api/v1/ws/controller/login               | Authenticates a user and establishes a session with WS Controller.                                      | 30s         | [Specification Link] |
| 2       | **WS Controller**  | **WS Controller Service**      | GET /api/v1/ws/controller/logout              | Logs out the user and terminates the active session with WS Controller.                               | 30s         | [Specification Link] |
| 3       | **WS Controller**  | **WS Controller Service**      | POST /api/v1/ws/controller/agent               | Retrieves a list of registered agents within the WS Controller system.                                 | 30s         | [Specification Link] |
| 4       | **WS Controller**  | **WS Controller Service**      | POST /api/v1/ws/controller/agent/create       | Creates a new agent within the WS Controller system for monitoring and configuration.                 | 30s         | [Specification Link] |
| 5       | **WS Controller**  | **WS Controller Service**      | POST /api/v1/ws/controller/agent/update       | Updates configuration or status of an existing agent in the WS Controller system.                     | 30s         | [Specification Link] |
| 6       | **WS Controller**  | **WS Controller Service**      | POST /api/v1/ws/controller/agent/configuration | Fetches the current configuration of a specific agent in the system.                                  | 30s         | [Specification Link] |
| 7       | **WS Controller**  | **WS Controller Service**      | POST /api/v1/ws/controller/agent/configuration| Updates the configuration of a specific agent in the WS Controller system.                           | 30s         | [Specification Link] |
| 8       | **WS Service**     | **WS Module Gateway Service** | POST /api/v1/ws/service/gateway | Handles incoming data from agents, validates requests, and routes them to appropriate processing modules for further analysis and execution.| 30s | [Specification Link] |
| 9       | **WS Service**     | **WS Module Web Attack Detection** | POST /api/v1/ws/service/attack-detection/predict | Submits web traffic data for AI-based prediction and detection of potential web attacks (e.g., SQL Injection, XSS). | 30s         | [Specification Link] |

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

## Detail API Spec

### POST /api/v1/ws/controller/login

#### Request Body:

```json
{
  "username": "admin",
  "password": "password123",
}
```
#### Response Body:
- Success Response:
  
```json
{
  "status": "success",
  "message": "Login successful",
  "data": {
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkFkbWluIiwiaWF0IjoxNTE2MjM5MDIyfQ.HxN7AdhZxxKkJhr6vB4i8DhQdFk4wO6hR9f1gqZ9JEI",
    "expires_in": 3600
  }
}
```
- Error Response (Invalid credentials):
  
```json
{
  "status": "error",
  "message": "Invalid username or password",
  "data": null
}
```

### GET /api/v1/ws/controller/logout

#### Request Header:

```http
GET /api/v1/ws/controller/logout HTTP/1.1
Host: localhost
Authorization: Bearer <your_access_token>
```

#### Request Body: This API does not require a request body. The request is made with the user's authentication token in the header.

#### Response Body:
- Success Response:
  
```json
{
  "status": "success",
  "message": "Logout successful",
  "data": null
}
```
- Error Response (Invalid or Missing Token):
  
```json
{
  "status": "error",
  "message": "Authentication token is invalid or expired",
  "data": null
}
```
- Error Response (User Not Logged In):

```json
{
  "status": "error",
  "message": "User is not logged in",
  "data": null
}
```

### POST /api/v1/ws/controller/agent

#### Request Body:

```json
{
  "agent_id": "string"  // Optional. If null, all agents will be retrieved.
}
```

#### Response Body:
- Success Response (Get All Agents):
```json
{
  "status": "success",
  "message": "Agents retrieved successfully",
  "data": [
    {
      "agent_id": "agent-12345",
      "name": "Agent Alpha",
      "platform": "Windows",
      "ip": "127.0.0.1",
      "port": "9768",
      "status": "active",
      "created_at": "2025-01-01T12:00:00Z"
    },
    {
      "agent_id": "agent-67890",
      "name": "Agent Beta",
      "platform": "WebApp",
      "ip": "127.0.0.1",
      "port": "443",
      "status": "inactive",
      "created_at": "2025-01-02T14:30:00Z"
    }
  ]
}

```
- Success Response (Get Specific Agent):
```json
{
  "status": "success",
  "message": "Agent retrieved successfully",
  "data": {
    "agent_id": "agent-12345",
    "name": "Agent Alpha",
    "platform": "Windows",
    "ip": "127.0.0.1",
    "port": "9768",
    "status": "active",
    "created_at": "2025-01-01T12:00:00Z"
  }
}
```
- Error Response (Agent Not Found (Specific Agent)):
 ```json
{
  "status": "error",
  "message": "Agent not found",
  "data": null
}
 ```
- Error Response (Invalid Request (Malformed Body)):
 ```json
{
  "status": "error",
  "message": "Invalid request body",
  "data": null
}
 ```
-  Error Response (Server Error):
```json
{
  "status": "error",
  "message": "Internal server error",
  "data": null
}
```

### POST /api/v1/ws/controller/agent/create  

#### Request Body:

```json
{
  "name": "string",
  "platform": "string",  // Allowed values: Windows, Linux, WebApp, MobileApp
  "ip": "string",
  "port": "number",
  "status": "string"  // Example: active, inactive, pending
}
```

#### Response Body:
- Success Response:
```json
{
  "status": "success",
  "message": "Agent created successfully",
  "data": {
    "agent_id": "agent-12345",
    "name": "Agent Alpha",
    "platform": "Linux",
    "ip": "10.0.1.15",
    "port": 8080,
    "status": "active",
    "created_at": "2025-02-18T12:00:00Z"
  }
}
```

- Error Response (Invalid Request Body):
```json
{
  "status": "error",
  "message": "Invalid request parameters",
  "data": null
}
```

- Error Response (Missing Required Fields):
```json
{
  "status": "error",
  "message": "Missing required fields: name, platform",
  "data": null
}
```

- Error Response (Duplicate Agent Name/IP):
```json
{
  "status": "error",
  "message": "Agent with this name or IP already exists",
  "data": null
}
```

- Error Response (Server Error)
```json
{
  "status": "error",
  "message": "Internal server error",
  "data": null
}
```

### POST /api/v1/ws/controller/agent/update  

#### Request Body:
#### Response Body:
- Success Response:
- Error Response:

### POST /api/v1/ws/controller/agent/configuration  

#### Request Body:
#### Response Body:
- Success Response:
- Error Response:

### POST /api/v1/ws/service/gateway

#### Request Body:

```json
{
  "agent_id": "string", 
  "rule": "object", // (WS Module Web Attack Detection, WS Module DGA Detection,...)
  "payload": {
    "data": "object" // Dynamic data based on request_type
  },
  "timestamp": "string" // ISO 8601 format (e.g., "2025-02-18T12:34:56Z")
}

#### Response Body:
```json
{
  "status": "success",
  "message": "Request processed successfully",
  "data": {
    "ws_module_web_attack_detection_score": 50,
    "ws_module_dga_detection_score": 10,
    "ws_module_common_attack_detection": {
      "open_redirect": true,
      "large_request": false,
      "http_method_tampering": false,
      "sql_injection": false,
      "cross_site_scripting": false,
    },
    "hash": "917b28a070ce73b87ab92a3976bec7038aa27dff1ea56d592e19c32612c3def0",
  },
  "processed_at": "string" // ISO 8601 format
}
```
- Success Response:
- Error Response: