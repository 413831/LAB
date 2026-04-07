# LAB

# Go Microservices App
This repository contains a robust, scalable microservices ecosystem built in Go (Golang). It demonstrates modern backend architecture patterns, including API Gateway design, inter-service HTTP communication, and asynchronous event-driven messaging. 
## 🏗️ Architecture & Services
The application is fully containerized using Docker Compose and consists of the following core components:
- **Broker Service (API Gateway)**: Acts as the single entry point for all frontend requests. It handles RESTful routing and dispatches asynchronous background tasks to a message queue.
- **Authentication Service**: Manages secure user authentication and interacts with a **PostgreSQL** database.
- **Logger Service**: A dedicated service for persisting application logs into a **MongoDB** database.
- **Mail Service**: Handles outbound email deliveries asynchronously (using MailHog for local development).
- **Listener Service**: A worker process that continuously consumes events from RabbitMQ and triggers the appropriate actions in the background.
- **Frontend App**: The client-side application that interacts with the Broker service.
## 🚀 Tech Stack
- **Language**: Go
- **Databases**: PostgreSQL, MongoDB
- **Message Broker**: RabbitMQ
- **Containerization**: Docker & Docker Compose
