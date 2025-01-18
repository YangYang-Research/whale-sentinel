# Whale Sentinel First Design Board

## Introduction

The Whale Sentinel is a security solution designed to protect web applications, mobile applications, and more. It aims to provide comprehensive security features to ensure the integrity and safety of applications in real-time. The solution integrates advanced threat detection mechanisms and continuous monitoring to proactively identify and mitigate potential risks. By leveraging state-of-the-art security technologies, Whale Sentinel ensures that applications are safeguarded against a wide range of cyber threats.

### Overall busineess requirements

The Whale Sentinel solution must meet the following business requirements:

- Security: Ensure the highest level of security for applications by providing real-time threat detection and mitigation.
- Scalability: The solution must be scalable to accommodate the growing needs of businesses and applications of varying sizes.
- Performance: Maintain optimal performance levels without affecting the quality of service of the installed applications.
- User-friendly Interface: Provide an intuitive and easy-to-use interface for monitoring and managing security events.
- Compliance: Ensure compliance with industry standards and regulations to meet the security and privacy requirements of different sectors.

### High level approach

This solution provides comprehensive runtime protection features, ensuring that applications remain secure against potential attacks. Additionally, the system integrates a continuous and intuitive monitoring interface, enabling administrators to easily oversee and manage security effectively.

### Functional requirements

#### WS Agent 

- The WS Agent is responsible for monitoring and protecting the runtime environment of the application. It performs real-time analysis and detection of potential threats, ensuring minimal impact on system performance. The agent communicates with the WS Service to report security events and receive configuration updates.

#### WS Service

- The WS Service acts as the central management component, coordinating the activities of all WS Agents deployed across different environments. It processes the security data received from the agents, provides a user interface for monitoring and managing security events, and ensures that the latest security policies are applied.

#### WS Controller

- The WS Controller is responsible for orchestrating the deployment and updates of WS Agents and WS Services. It handles the configuration management, deployment automation, and scaling of the security components to adapt to the changing needs of the application environment.

### Business sizing

- Depends on the installed application.

### Performance

- Agent does not affect the service quality of the installed application.

## Overall Design

![Overall](https://github.com/noobpk/whale-sentinel/blob/main/diagrams/Whale-Sentinel-Overall-Design.png?raw=true)

## References
