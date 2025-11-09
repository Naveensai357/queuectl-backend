# queuectl-backend
CLI-based Background Job Queue System (Spring Boot)

A **CLI-based Background Job Queue System** built using **Java Spring Boot**, supporting background job execution, retry mechanisms with exponential backoff, and a dead-letter queue (DLQ) for permanently failed jobs.

This project implements the backend for **QueueCTL**, a lightweight, extensible system to manage distributed job queues — designed for backend developer internship evaluation.

## Features

| Category | Description |
|-----------|--------------|
| **Job Management** | Enqueue and track background jobs with states: pending, processing, completed, failed, and dead |
| **Retry Logic** | Automatic retries with **exponential backoff** for failed jobs |
| **Dead Letter Queue** | Permanently failed jobs move to DLQ after exhausting retries |
| **Multi-Worker Execution** | Parallel job execution with proper locking and graceful shutdown |
| **Persistent Storage** | Job data stored persistently using an embedded **H2 database** |
| **Configuration Management** | CLI/Config API for retry limits and backoff settings |
| **Status and Monitoring** | APIs to view job state summaries, DLQ, and worker status |

## Tech Stack

| Component | Technology |
|------------|-------------|
| Language | Java 17 |
| Framework | Spring Boot 3.x |
| Database | H2 (Embedded) |
| Build Tool | Maven |
| CLI Integration | Spring Shell / REST Endpoints |
| Testing | JUnit 5 |

---

## Project Structure

CLI_naveen1/
│
├── src/
│ ├── main/
│ │ ├── java/edu/amrita/
│ │ │ ├── CliNaveen1Application.java # Main entry point
│ │ │ ├── controller/
│ │ │ │ └── HomeController.java # Health check endpoint
│ │ │ ├── model/
│ │ │ │ └── Job.java # Job entity
│ │ │ ├── repository/
│ │ │ │ └── JobRepository.java # Data access layer
│ │ │ └── service/
│ │ │ └── JobService.java # Core logic: retry, DLQ, backoff
│ │ └── resources/
│ │ ├── application.properties # Configurations (DB, server port, etc.)
│ │ └── schema.sql / data.sql (optional)
│ └── test/java/edu/amrita/
│ └── CliNaveen1ApplicationTests.java # Unit tests
│
├── pom.xml
├── mvnw / mvnw.cmd
├── HELP.md
├── .gitignore
└── README.md

## Configuration (application.properties)

properties
# Server configuration
server.port=8080

# H2 Database configuration
spring.datasource.url=jdbc:h2:file:./data/queuectl-db
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=

# Hibernate / JPA
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.h2.console.enabled=true
spring.h2.console.path=/h2-console

# Custom queue settings
queuectl.max-retries=3
queuectl.backoff-base=2
