# Whale Sentinel Data Flow

![Data Flow](https://github.com/noobpk/whale-sentinel/blob/main/diagrams/Whale_Sentinel_Data_Flow.png?raw=true)

### 1. WS Agents → WS Services (WS Gateway Service)

**Data Flow (Black):** The WS Agent submits content requests from the client to the WS Service via the WS Gateway Service.

### 2. WS Services Processing

Within WS Services, several modules handle different tasks:

#### (a) WS Module Web Attack Detection

- **Audit Flow (Green):** The Web Attack Detection module audits incoming content requests for security threats.
- **Configuration Flow (Red):** Receives updated security configurations from WS Module Sync Configuration.

#### (b) WS Module DGA Detection

- **Audit Flow (Green):** The DGA Detection module audits incoming content requests for domain generation algorithm threats.
- **Configuration Flow (Red):** Receives updated security configurations from WS Module Sync Configuration.

#### (c) WS Module Common Attack Detection

- **Audit Flow (Green):** The Common Attack Detection module audits incoming content requests for common attack patterns.
- **Configuration Flow (Red):** Receives updated security configurations from WS Module Sync Configuration.

#### (d) WS Module Log

- **Log Flow (Blue):** Collects logs from different WS Service modules.
- **Configuration Flow (Red):** Receives new configurations from WS Module Sync Configuration.

#### (e) WS Module Sync Configuration

- **Configuration Flow (Red):** Syncs new configurations to all WS modules, ensuring they operate with the latest security policies.

### 3. WS Service → WS Controller

**Log Flow (Blue):** Logs collected in WS Module Log are transferred to the WS Controller Database.

### 4. WS Controller (WS Dashboard & Database)

- **Data Flow (Black):** The WS Dashboard retrieves and displays data from the Database.
- **Data Flow (Black):** The Database exchanges data with external systems.
- **Log Flow (Blue):** Logs are transferred from the WS Controller to the Database.