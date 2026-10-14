\# Real-Time Production Log Intelligence \& Root-Cause Analysis



A real-time monitoring and root-cause analysis project that uses telemetry, stream processing, and simulated failures to identify abnormal behavior across a distributed microservices application.



\## Overview



Modern distributed applications consist of multiple services, making it difficult to identify which component is responsible when failures occur. This project builds a pipeline to collect service telemetry, detect anomalies in streaming data, simulate operational failures, and rank potential root-cause services.



\## Architecture



```text

Microservices

&#x20;    |

&#x20;    v

Telemetry Producer

&#x20;    |

&#x20;    v

Kafka: telemetry

&#x20;    |

&#x20;    v

PySpark Structured Streaming

&#x20;    |

&#x20;    v

Anomaly Detection

&#x20;    |

&#x20;    v

Kafka: spark-detections

&#x20;    |

&#x20;    v

Root-Cause Analysis \& Evaluation

```



The system also includes a failure injector to simulate different operational problems and evaluate detection behavior.



\## Technology Stack



\- \*\*Python\*\* — telemetry generation, failure injection, and analysis

\- \*\*Apache Kafka\*\* — streaming telemetry and detection events

\- \*\*Apache Spark\*\* — Structured Streaming and window-based processing

\- \*\*Docker \& Docker Compose\*\* — containerized microservices and infrastructure

\- \*\*Microservices architecture\*\* — independent application services

\- \*\*Git \& GitHub\*\* — source control and project hosting



\## Microservices



The application consists of six services:



| Service | Responsibility |

|---|---|

| API Gateway | Entry point for application requests |

| User Service | User-related operations |

| Order Service | Order processing |

| Inventory Service | Inventory operations |

| Payment Service | Payment-related operations |

| Database Service | Database-related operations |



\## Key Features



\- Streaming telemetry through Kafka.

\- Window-based telemetry processing with PySpark Structured Streaming.

\- Anomaly scores and binary anomaly predictions.

\- Simulated failure scenarios for controlled testing.

\- Root-cause analysis to rank potentially faulty services.

\- Evaluation scripts for detection, latency, throughput, and RCA.



\## Simulated Failure Scenarios



The failure injector supports scenarios including:



\- CPU spike

\- Memory leak

\- Database latency

\- Database connection exhaustion

\- HTTP 5xx spike

\- Network latency

\- Service crash

\- Traffic spike



These scenarios help test the system under controlled conditions.



\## Project Structure



```text

Production-Log-Intelligence-RCA/

├── compose.yaml

├── services/

│   ├── api-gateway/

│   ├── user-service/

│   ├── order-service/

│   ├── inventory-service/

│   ├── payment-service/

│   └── database-service/

├── telemetry/

│   └── producer.py

├── failure\_injection/

│   └── injector.py

├── streaming/

│   ├── Dockerfile

│   └── spark\_job.py

├── rca/

│   └── rca\_engine.py

├── evaluation/

│   ├── evaluate\_detection.py

│   ├── evaluate\_rca.py

│   ├── benchmark\_detection.py

│   ├── benchmark\_detection\_latency.py

│   ├── benchmark\_spark\_latency.py

│   └── benchmark\_throughput.py

└── README.md

```



\## Prerequisites



\- Docker Desktop with Docker Compose

\- Python 3

\- Git (optional, for cloning the repository)



\## Setup and Execution



\### 1. Clone the repository



```bash

git clone https://github.com/Porwez/Production-Log-Intelligence-RCA.git

cd Production-Log-Intelligence-RCA

```



\### 2. Start the containers



```bash

docker compose up -d

```



Check container status:



```bash

docker compose ps

```



\### 3. Check the API Gateway



```bash

curl http://localhost:8000/health

```



Test the request-processing endpoint:



```bash

curl http://localhost:8000/process

```



\### 4. Start telemetry generation



Open a separate terminal in the project directory:



```bash

python -m pip install kafka-python

python telemetry/producer.py

```



\### 5. Inject failures



Open another terminal:



```bash

python failure\_injection/injector.py

```



\### 6. Run evaluation



For detection evaluation:



```bash

python evaluation/evaluate\_detection.py

```



For root-cause analysis evaluation:



```bash

python evaluation/evaluate\_rca.py

```



Some evaluation scripts may expect telemetry or injected incidents to be running. Follow the prompts printed by each script.



> \*\*Note:\*\* The exact startup order and Kafka topic initialization may depend on the current configuration. If Spark reports that the `telemetry` topic does not exist, create the topic using the Kafka configuration in `compose.yaml` before restarting the Spark container.



\## Evaluation



The project includes scripts to evaluate:



\- Detection behavior against simulated incidents

\- Detection latency

\- Spark processing latency

\- Event throughput

\- Root-cause analysis accuracy



Results should be reported with their test conditions, sample sizes, and measurement boundaries. Controlled failure-injection results do not automatically establish production performance.



\## Limitations and Future Improvements



\- Test against more realistic production telemetry.

\- Evaluate false-positive and false-negative rates across larger datasets.

\- Test cascading failures across dependent services.

\- Measure sustained throughput under increasing load.

\- Improve observability with dashboards and alerting.

\- Validate root-cause rankings against more diverse incidents.



\## Learning Outcomes



This project explores distributed systems, event streaming, stream processing, anomaly detection, controlled failure injection, and root-cause analysis. It also demonstrates how to containerize and test a multi-service application.



\## Author



\*\*Porwez Hussain\*\*



GitHub: \[@Porwez](https://github.com/Porwez)

