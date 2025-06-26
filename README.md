# 🐋 Whale Sentinel (WS)

## Introduction

**Whale Sentinel** is a comprehensive cybersecurity platform designed to **protect modern applications**—from web to mobile and endpoint environments—against a wide range of cyber threats. By combining **AI-powered detection**, **real-time monitoring**, and **modular components**, Whale Sentinel gives developers and security teams a proactive edge against malicious attacks.

Whether you're a startup scaling fast or an enterprise securing sensitive operations, Whale Sentinel offers a **plug-and-play**, **highly customizable** solution that’s both **developer-friendly** and **robust in protection**.

---

## 🚨 Why Whale Sentinel?

Modern applications face evolving threats: SQL injections, bot traffic, logic abuse, DGA-based attacks, and more. Whale Sentinel addresses these challenges by:

- 🧠 Leveraging **AI-driven analysis** for smarter, faster detection  
- 🔐 Providing **layered protection** from the edge to the backend  
- 🛠️ Supporting **framework-level integration** (e.g., Flask, Spring Boot)  
- 📈 Enabling **centralized monitoring & threat correlation**  
- ⚙️ Allowing **extensive customization** with minimal configuration  

---

## 🛡️ Solution Modules & Capabilities

### 🌐 Web Application Protection

Protect your APIs, websites, and backend services from critical vulnerabilities:

| Threat Type                        | Detection Method               | AI/ML Enhanced     | Protection Level   |
|-----------------------------------|--------------------------------|--------------------|--------------------|
| **SQL Injection (SQLi)**          | Pattern & behavior analysis    | ✅ Deep Learning    | 🔒 High            |
| **Cross-Site Scripting (XSS)**    | Pattern & behavior analysis    | ✅ Deep Learning    | 🔒 High            |
| **Command Injection (CMDi)**      | Pattern & behavior analysis            | ✅ Deep Learning    | 🔒 High            |
| **Local File Inclusion (LFi)**    | Pattern & behavior analysis       | ✅ Deep Learning    | 🔒 High            |
| **Domain Generation Algorithm (DGA)** | Behavior analysis     | ✅ Deep Learning   | 🔒 High     |
| **HTTP Large Requests**           | Payload size & entropy check   | ❌                  | 🟡 Medium          |
| **HTTP Verb Tampering**           | Method validation layer        | ❌                  | 🟡 Medium          |
| **Insecure Redirects**            | Redirect sanitization          | ❌                  | 🟢 Essential          |
| **Insecure File Uploads**         | MIME & file type validation    | ❌                  | 🟡 Medium          |
| **Unknown Exploit Patching**      | Pattern & behavior analysis | ✅ Deep Learning  | 🔒 High            |
| **Secure Response Headers**       | HTTP header hardening          | ❌                  | 🟢 Essential        |
| **Request Rate Limiting**         | IP/session throttling          | ❌                  | 🟢 Essential        |

> Supports integrations with Web framework, Flask, Spring Boot, and more.

---

### 🔍 Legend

- **Detection Method**: Shows the primary technique used to detect the threat.
- **AI/ML Enhanced**: Whether the detection leverages machine learning or deep learning.
- **Protection Level**:
  - 🔒 **High**: Near real-time detection and automatic mitigation
  - 🟡 **Medium**: Rule-based or threshold-based control
  - 🟢 **Essential**: Security best practices to reduce risk surface

---

### 📱 Mobile App Protection *(Coming Soon)*

- Emulator and root detection  
- Secure data storage enforcement  
- In-app runtime behavior monitoring  
- Network traffic anomaly detection  

---

### 💻 Endpoint Protection *(Coming Soon)*

- Behavioral anomaly detection  
- File system & process integrity monitoring  
- Real-time response with threat intelligence  

---

## 🚀 Getting Started

To learn how Whale Sentinel works under the hood and how to deploy it in your stack, check out the [Whale Sentinel Design Board](https://github.com/YangYang-Research/whale-sentinel/blob/main/documents/Whale-Sentinel-Design-Board.md).

You’ll learn:

- 📚 WS architecture and how the components work together
- 🧩 How to integrate WS Web Agent with frameworks like Flask/Spring
- 🔬 Detection logic for SQLi, XSS, DGA, and more
- 💾 How logs and data are processed with OpenSearch, MongoDB, and Redis
- 🧠 Real-world use of AI to detect and react to attacks in real time

---

## 📦 Whale Sentinel Ecosystem

Whale Sentinel is composed of multiple modular repositories:

- 🖥️ **[WS-Controllers](https://github.com/YangYang-Research/whale-sentinel-controllers)**  
  Dashboard, Configuration Manager, and RAG-based AI Assistant  

- ⚙️ **[WS-Services](https://github.com/YangYang-Research/whale-sentinel-services)**  
  Logging, Detection Engines, Data Flow, and Core APIs  

- 👻 **[WS-Agents](https://github.com/YangYang-Research/whale-sentinel-agents)**  
  Lightweight agents for securing your edge (Web, API, Reverse Proxy)  

---

## 🧠 AI-Powered RAG Assistant

Whale Sentinel includes a **RAG (Retrieval-Augmented Generation) Assistant** to support:

- 🤖 Log summarization and threat explanation  
- 🔍 Retrieval of incident context from OpenSearch & MongoDB  
- 🧭 Guided threat investigation and remediation workflows  

---

## 👥 Contributing

We welcome contributions, suggestions, and collaborations.  
To get started:

1. Fork the repo
2. Create a feature branch
3. Submit a Pull Request

Check out our contributing guidelines. By contributing, you agree to abide by our Code of Conduct.

---

## 🪪 License

**Whale Sentinel** is open-source software licensed under the [MIT License](LICENSE).  
Built by [lethanhphuc](https://github.com/noobpk) aka `noobpk`.

---

## 🛡️ Security & Responsible Disclosure

If you discover a security issue or vulnerability, please report it responsibly:

- Open a private issue on GitHub
- Or contact the maintainers directly

We take security seriously and appreciate responsible disclosures.

---
