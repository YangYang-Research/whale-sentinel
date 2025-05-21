# Whale Sentinel System Context

![System Context](https://github.com/YangYang-Research/whale-sentinel/blob/main/diagrams/Whale_Sentinel_System_Context.png?raw=true)

## **System Domains**
- **WS Agents**
- **WS Services**
- **WS Controllers**

---

## 🔄 Connections and Data Flows

### 1. **WS Agents → WS Services**
- **Submit content request to WS Gateway Service**
  - **Type:** `Data exchange` (black arrow)
  - **Purpose:** Forward client requests to Whale Sentinel services.

---

### 2. **WS Gateway Service → Detection Modules**
- **Modules:**
  - `WS Module Web Attack Detection`
  - `WS Module DGA Detection`
  - `WS Module Common Attack Detection`
- **Connection:** Predict content request
  - **Type:** `Audit process` (green arrow)
  - **Purpose:** Audit requests for threat detection.

---

### 3. **Configuration Handling**

#### a. **Modules ↔ Redis Cache**
- **Query configuration from cache**
  - **Type:** Internal call (dashed black line)
  - **Purpose:** Retrieve module configuration quickly from cache.

#### b. **Modules ↔ WS Module Configuration Service**
- **If cache miss → Query configuration service**
  - **Type:** Internal call (dashed black line)
- **WS Module Configuration Service → Redis Cache**
  - **Sync new configuration**
  - **Type:** `Configuration sync` (red arrow)
- **WS Module Configuration Service → Modules**
  - **Push configuration**
  - **Type:** `Configuration sync` (red arrow)

---

### 4. **Log Transfer**

- **WS Modules → OpenSearch DB (via Fluent-bit)**
  - **Type:** `Log transfer` (blue arrow)
  - **Purpose:** Centralized logging and analysis in OpenSearch.

---

### 5. **WS Controllers (Dashboards & Management)**

#### a. **WS OpenSearch Dashboard ↔ OpenSearch DB**
- **Type:** `Data exchange` (black arrow)
- **Purpose:** Query logs and visualize data.

#### b. **WS Manage Dashboard ↔ Postgres DB**
- **Type:** `Data exchange` (black arrow)
- **Purpose:** Manage configuration and system state.

#### c. **WS Manage Dashboard ↔ WS Processor**
- **Type:** `Data exchange` (black arrow)
- **Purpose:** Send and receive system management actions.

#### d. **WS Processor → WS Module Configuration Service**
- **Type:** `Configuration sync` (red arrow)
- **Purpose:** Push updated configurations into the system.

---

### 6. **WS Modules → WS Gateway Service**
- **Return prediction results**
  - **Type:** `Audit process` (green arrow)
  - **Purpose:** Provide threat assessment results back to Gateway.

---

## 📘 Legend (from diagram)

| Arrow Color  | Meaning               |
|--------------|------------------------|
| ⚫ Black      | Data exchange          |
| 🟢 Green      | Audit process          |
| 🔴 Red        | Configuration sync     |
| 🔵 Blue       | Log transfer           |