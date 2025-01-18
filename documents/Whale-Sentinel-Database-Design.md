# Whale Sentinel Database Design

# Database model

## Database: WS_Controller_DB

## **users**
- **_id** (ObjectId): Unique identifier for the user.
- **username** (string): The username chosen by the user.
- **email** (string): The email address of the user.
- **passwordHash** (string): The hashed password for secure authentication.
- **roles** (array): List of roles assigned to the user (references `roles._id`).
- **status** (string): Status of the user account (e.g., "active", "inactive", "suspended").
- **createdAt** (ISODate): Timestamp indicating when the user account was created.
- **updatedAt** (ISODate): Timestamp indicating the last update to the user record.
- **profile** (object): Additional user details:
  - **firstName** (string): First name of the user.
  - **lastName** (string): Last name of the user.
  - **phone** (string): Contact phone number of the user.
  - **address** (object): User's address details:
    - **street** (string): Street name or address.
    - **city** (string): City name.
    - **state** (string): State or region.
    - **zipCode** (string): ZIP or postal code.

## **roles**
- **_id** (ObjectId): Unique identifier for the role.
- **name** (string): Name of the role (e.g., "admin", "editor", "viewer").
- **permissions** (array): List of permissions granted to the role (e.g., ["read", "write", "delete"]).
- **description** (string): Brief description of the role and its purpose.
- **createdAt** (ISODate): Timestamp indicating when the role was created.
- **updatedAt** (ISODate): Timestamp indicating the last update to the role record.

## **agents**
- **_id** (ObjectId): Unique identifier for the agent.
- **type** (string): Type of the agent (e.g., web, mobile).
- **ip** (string): IP address of the agent.
- **healthy** (boolean): Indicates the health status of the agent (e.g., true = healthy, false = unhealthy).
- **status** (string): Current operational status of the agent.

## **agentConfigurations**
- **_id** (ObjectId): Unique identifier for the agent configuration.
- **agent_id** (ObjectId): Reference to the `agents._id` field, associating the configuration with an agent.
- **is_use_ws_module_web_attack_detection** (integer): Indicator for enabling WS Module Web Attack Detection.
- **ws_ws_module_web_attack_detection_threshold** (integer): Threshold settings for Web Attack Detection.
- **ws_agent_authen_key** (string): Authentication key for agent-to-WS services communication.
- **agent_running_mode** (string): Running mode for the agent (e.g., "normal", "debug").
- **max_requests_per_minute** (integer): Maximum number of requests allowed per minute.
- **cors** (object): Cross-Origin Resource Sharing configuration for the agent.
- **is_safe_redirect** (integer): Indicator for enabling safe redirects.
- **protect_response** (integer): Flag to protect responses from potential threats.
- **anti_dos** (integer): Anti-DoS configuration for mitigating denial-of-service attacks.
- **trust_domain** (string): Specifies the trusted domains for the agent.
- **created_at** (ISODate): Timestamp indicating when the configuration was created.
- **updated_at** (ISODate): Timestamp indicating the last update to the configuration.

## **requestlogs**
- **_id** (ObjectId): Unique identifier for the request log entry.
- **time** (ISODate): Timestamp of the request.
- **ipaddress** (string): IP address of the client making the request.
- **url** (string): URL of the requested resource.
- **method** (string): HTTP method used (e.g., GET, POST).
- **useragent** (string): User-Agent string of the client making the request.
- **status_code** (string): HTTP response status code.
- **req_param** (string): Request parameters.
- **req_body** (string): Request body content.
- **req_size** (integer): Size of the request payload.
- **response** (string): Response data sent to the client.
- **res_content** (string): Content of the response.
- **res_size** (integer): Size of the response payload.
- **attack_type** (string): Detected type of attack (if applicable).
- **ws_module_web_attack_detection_score** (float): Score from WS Module Web Attack Detection analysis.
- **req_hash** (string): Unique hash representing the request.
- **event_id** (string): Identifier for the associated event.
- **latitude** (float): Latitude of the client's location.
- **longitude** (float): Longitude of the client's location.
- **status** (string): Status of the request (e.g., "completed", "blocked").
- **review** (string): Comments or reviews related to the request.
- **created_at** (ISODate): Timestamp when the log entry was created.
- **updated_at** (ISODate): Timestamp when the log entry was last updated.

## **feedbacks**
- **_id** (ObjectId): Unique identifier for the feedback entry.
- **sentence** (string): Feedback content provided by a user or system.
- **label** (string): Category or label assigned to the feedback (e.g., "positive", "negative").
- **created_at** (ISODate): Timestamp when the feedback entry was created.
- **updated_at** (ISODate): Timestamp when the feedback entry was last updated.
