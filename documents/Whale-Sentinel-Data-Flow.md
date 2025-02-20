# Whale Sentinel Data Flow

![Data Flow](https://github.com/noobpk/whale-sentinel/blob/main/diagrams/Whale_Sentinel_Data_Flow.png?raw=true)

### 1. WS Agent → WS Service (WS Gateway Service)

Data Flow: The WS Agent submits content requests from the client to the WS Service via the WS Gateway Service.

### 2. WS Service Processing

Within WS Service, several modules handle different tasks:

#### (a) WS Module Web Attack Detection

Audit Flow (Green): The Web Attack Detection module audits incoming content requests for security threats.

Configuration Flow (Red): Receives updated security configurations from WS Module Sync Configuration.

#### (b) WS Module Log

Log Flow (Orange): Collects logs from different WS Service modules.

Configuration Flow (Red): Receives new configurations from WS Module Sync Configuration.

#### (c) WS Module Sync Configuration

Configuration Flow (Red): Syncs new configurations to all WS modules, ensuring they operate with the latest security policies.

### 3. WS Service → WS Controller

Log Flow (Orange): Logs collected in WS Module Log are transferred to the WS Controller Database.

### 4. WS Controller (WS Dashboard & Database)

Data Flow: The WS Dashboard retrieves and displays logs from the Database.
