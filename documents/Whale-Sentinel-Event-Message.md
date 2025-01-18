# Whale Sentinel Event Message

| .No | Topic                                | Flow                                                    | Description                                                                                      | Detail Message         |
|-----|--------------------------------------|---------------------------------------------------------|--------------------------------------------------------------------------------------------------|------------------------|
| 1   | topic-controler-service-sync-config | WS Controller Service -> Kafka -> WS Module Sync Configuration | The WS Controller Service publishes configuration updates to Kafka. The WS Module Sync Configuration consumes these updates and synchronizes them across all modules and agents. | {}                     |
| 2   | topic-service-log-controler         | WS Module Logg -> Kafka -> WS Controller Service        | The WS Module Logg sends log data to Kafka, which is consumed by the WS Controller Service for centralized logging and monitoring. | {}                     |
