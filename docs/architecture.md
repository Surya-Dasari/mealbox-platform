# 📦 MealBox – System Architecture Documentation

## 1. Overview

MealBox is a microservices-based e-commerce platform designed to demonstrate real-world DevOps practices using independently deployable services, a centralized API Gateway, and strict cold-start validation.

The system is intentionally built incrementally, validating each layer before moving to the next.

---

## 2. High-Level Architecture

Frontend (React)
      |
      v
API Gateway (9100)
      |
      +--> Auth Service          (9101)
      +--> Restaurant Service    (9102)
      +--> Cart Service          (9103)
      +--> Order Service         (9104)
      +--> Inventory Service    (9105)
      +--> Payment Service      (9106)
      +--> Notification Service (9107)

### Key Characteristics
- Single entry point via API Gateway
- Backend services are independently deployable
- No direct frontend-to-service communication
- Clear responsibility boundaries

---

## 3. Service Responsibilities

### 3.1 API Gateway (Port 9100)
**Purpose**
- Single entry point for all clients
- Request routing
- CORS handling

**Does NOT**
- Contain business logic
- Manage service lifecycle
- Store data

---

### 3.2 Auth Service (Port 9101)
**Purpose**
- Authentication and authorization

**Future Enhancements**
- JWT token generation
- OAuth2 integration
- Role-based access control

---

### 3.3 Restaurant Service (Port 9102)
**Purpose**
- Restaurant and menu metadata

**Future Enhancements**
- Restaurant listings
- Menu management
- Search and filtering

---

### 3.4 Cart Service (Port 9103)
**Purpose**
- Temporary user cart management

**Characteristics**
- Stateful by nature
- Short-lived data

**Future Enhancements**
- Redis integration
- Cart expiration logic

---

### 3.5 Order Service (Port 9104)
**Purpose**
- Order creation and lifecycle management

**Future Enhancements**
- Order status tracking
- Saga / orchestration patterns

---

### 3.6 Inventory Service (Port 9105)
**Purpose**
- Product availability and stock management

**Future Enhancements**
- Database integration
- Stock reservation logic

---

### 3.7 Payment Service (Port 9106)
**Purpose**
- Payment processing boundary

**Future Enhancements**
- External payment gateway integration
- Retry and failure handling

---

### 3.8 Notification Service (Port 9107)
**Purpose**
- User notifications

**Characteristics**
- Asynchronous workload

**Future Enhancements**
- Email/SMS integrations
- Event-driven processing (Kafka/RabbitMQ)

---

## 4. Port Allocation Strategy

| Component | Port |
|---------|------|
| API Gateway | 9100 |
| Auth Service | 9101 |
| Restaurant Service | 9102 |
| Cart Service | 9103 |
| Order Service | 9104 |
| Inventory Service | 9105 |
| Payment Service | 9106 |
| Notification Service | 9107 |

Ports are chosen to avoid conflicts with Jenkins, Nexus, SonarQube, and Docker services.

---

## 5. Startup & Cold-Start Methodology

**Rule**
Startup is bottom-up, traffic is top-down.

### Correct Startup Order
1. Backend services
2. API Gateway
3. Frontend

Cold-start validation ensures production readiness and mirrors Docker/Kubernetes behavior.

---

## 6. Current System State

### Implemented
- All backend services
- API Gateway routing
- Health endpoints
- Cold-start validation
- Multi-repo Git version control

### Planned (Future Phases)
- Docker & Docker Compose
- CI/CD with Jenkins
- Security scanning (Trivy, SonarQube)
- Kubernetes / OpenShift
- Observability (Prometheus, Grafana, Loki)

---

## 7. Architectural Principles

- Single Responsibility Principle
- Loose coupling
- Independent deployability
- Production-first validation
- DevOps-driven design

---

## 8. Summary

MealBox is a production-grade microservices architecture built with strong DevOps discipline, focusing on correctness, clarity, and future scalability.
