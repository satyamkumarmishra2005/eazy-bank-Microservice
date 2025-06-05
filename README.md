
# Eazy Bank Microservices

A modern banking application demonstrating microservices architecture using Java, Spring Boot, Spring Cloud, Docker, and Kubernetes.

## Table of Contents

* [Overview](#overview)
* [Architecture](#architecture)
* [Microservices](#microservices)
* [Infrastructure Components](#infrastructure-components)
* [Prerequisites](#prerequisites)
* [Getting Started](#getting-started)
* [Configuration](#configuration)
* [Running the Application](#running-the-application)
* [Monitoring & Observability](#monitoring--observability)
* [Security](#security)
* [Contributing](#contributing)
* [License](#license)

## Overview

Eazy Bank Microservices is designed to showcase the implementation of a scalable and resilient microservices-based banking application. It leverages cloud-native technologies to ensure flexibility, maintainability, and ease of deployment.

## Architecture


![Architecture Diagram](https://github.com/satyamkumarmishra2005/eazy-bank-Microservice/blob/70ef8f8a4239e1722f45f18ac8d79f9be244ecfe/Microservices%20(1).png)

## Microservices

* **Accounts Service**: Manages customer account information.
* **Cards Service**: Handles credit/debit card details and operations.
* **Loans Service**: Manages loan accounts and related transactions.
* **Message Service**: Handles messaging functionalities within the application.

## Infrastructure Components

* **Config Server**: Centralized configuration management for all microservices.
* **Gateway Server**: API Gateway that routes requests to appropriate microservices.
* **Kubernetes**: Container orchestration platform for deploying and managing microservices.

## Prerequisites

Before you begin, ensure you have the following installed:

* Java 17
* Maven
* Docker & Docker Compose
* Kubernetes CLI (kubectl)
* Helm (for Kubernetes package management)

## Getting Started

1. **Clone the Repository**:

   ```bash
   git clone https://github.com/satyamkumarmishra2005/eazy-bank-Microservice.git
   cd eazy-bank-Microservice
   ```



2. **Build the Microservices**:

   ```bash
   mvn clean install
   ```



3. **Build Docker Images**:

   ```bash
   docker build -t accounts-service ./accounts
   docker build -t cards-service ./cards
   docker build -t loans-service ./loans
   docker build -t message-service ./message
   docker build -t config-server ./configserver
   docker build -t gateway-server ./gatewayserver
   ```



## Configuration

The application uses a centralized configuration managed by the Config Server. Configuration files are located in the `configserver` directory. Ensure that the configuration files for each environment (e.g., `accounts-dev.properties`, `cards-dev.properties`) are properly set up.

## Running the Application

### Using Docker Compose

A `docker-compose.yml` file can be created to manage and run all services together. Here's a basic example:

```yaml
version: '3.8'
services:
  config-server:
    image: config-server
    ports:
      - "8888:8888"
  gateway-server:
    image: gateway-server
    ports:
      - "8080:8080"
    depends_on:
      - config-server
  accounts-service:
    image: accounts-service
    depends_on:
      - config-server
  cards-service:
    image: cards-service
    depends_on:
      - config-server
  loans-service:
    image: loans-service
    depends_on:
      - config-server
  message-service:
    image: message-service
    depends_on:
      - config-server
```



Run the application:

```bash
docker-compose up
```



### Using Kubernetes

1. **Deploy Config Server**:

   ```bash
   kubectl apply -f kubernetes/configserver-deployment.yaml
   ```



2. **Deploy Other Services**:

   Apply the respective deployment and service YAML files located in the `kubernetes` directory for each microservice.

3. **Access the Application**:

   Use `kubectl port-forward` or expose services using LoadBalancer or Ingress to access the application endpoints.

## Monitoring & Observability

Integrate monitoring tools like Prometheus and Grafana for real-time metrics and dashboards. Logs can be aggregated using ELK Stack or similar solutions.

## Security

Implement security best practices:

* **Authentication & Authorization**: Use OAuth2 and JWT for securing APIs.
* **Secure Communication**: Ensure all inter-service communication is over HTTPS.
* **Configuration Management**: Avoid hardcoding sensitive information; use secure vaults or environment variables.

## Contributing

Contributions are welcome! Please fork the repository and submit a pull request for any enhancements or bug fixes.

## License

This project is licensed under the MIT License
