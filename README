# Microservices Sample Project

A complete microservices architecture implementation using Spring Boot, Spring Cloud Gateway, Docker, and Docker Compose.

## 🏗️ Architecture

This project consists of four microservices:

- **API Gateway** (Port 8086) - Routes requests to appropriate services
- **Item Service** (Port 8089) - Manages items/products
- **Order Service** (Port 8088) - Handles order operations
- **Payment Service** (Port 8087) - Processes payments

```
┌─────────────────┐
│   API Gateway   │ :8086
│  (Port 8086)    │
└────────┬────────┘
         │
    ┌────┴────┬─────────┬──────────┐
    │         │         │          │
┌───▼───┐ ┌──▼───┐ ┌───▼────┐ ┌───▼────┐
│ Item  │ │Order │ │Payment │ │  ...   │
│Service│ │Service│ │Service │ │        │
│ :8089 │ │ :8088│ │ :8087  │ │        │
└───────┘ └──────┘ └────────┘ └────────┘
```

## 🛠️ Tech Stack

- **Java**: 17 (recommended) or 21
- **Spring Boot**: 3.2.0
- **Spring Cloud Gateway**: 2023.0.0
- **Docker**: For containerization
- **Docker Compose**: For multi-container orchestration
- **Maven**: Build tool

## 📋 Prerequisites

- Java 17 or 21
- Maven 3.6+
- Docker Desktop
- Git

## 🚀 Quick Start

### 1. Clone the Repository

```bash
git clone <repository-url>
cd Microservices-Sample
```

### 2. Build All Services

**Windows:**
```bash
build-all.bat
```

**Linux/Mac:**
```bash
chmod +x build-all.sh
./build-all.sh
```

Or manually:
```bash
cd itemservice && mvnw clean package -DskipTests && cd ..
cd orderservice && mvnw clean package -DskipTests && cd ..
cd paymentservice && mvnw clean package -DskipTests && cd ..
cd apigateway && mvnw clean package -DskipTests && cd ..
```

### 3. Start Services with Docker Compose

```bash
docker-compose up --build
```

### 4. Stop Services

```bash
docker-compose down
```

## 📡 API Endpoints

All requests go through the API Gateway at `http://localhost:8086`

### Item Service

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/items` | Get all items |
| POST | `/items` | Add new item |
| GET | `/items/{id}` | Get item by ID |

**Examples:**
```bash
# Get all items
curl http://localhost:8086/items

# Add a new item
curl -X POST http://localhost:8086/items \
  -H "Content-Type: application/json" \
  -d '"Tablet"'

# Get item by ID
curl http://localhost:8086/items/0
```

### Order Service

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/orders` | Get all orders |
| POST | `/orders` | Create new order |
| GET | `/orders/{id}` | Get order by ID |

**Examples:**
```bash
# Get all orders
curl http://localhost:8086/orders

# Create a new order
curl -X POST http://localhost:8086/orders \
  -H "Content-Type: application/json" \
  -d '{"item":"Book","quantity":2}'

# Get order by ID
curl http://localhost:8086/orders/0
```

### Payment Service

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/payments` | Get all payments |
| POST | `/payments/process` | Process payment |
| GET | `/payments/{id}` | Get payment by ID |

**Examples:**
```bash
# Get all payments
curl http://localhost:8086/payments

# Process a payment
curl -X POST http://localhost:8086/payments/process \
  -H "Content-Type: application/json" \
  -d '{"orderId":1,"amount":100.00}'

# Get payment by ID
curl http://localhost:8086/payments/0
```

## 📂 Project Structure

```
Microservices-Sample/
├── apigateway/              # API Gateway service
│   ├── src/
│   ├── Dockerfile
│   └── pom.xml
├── itemservice/             # Item management service
│   ├── src/
│   │   └── main/
│   │       └── java/.../controller/
│   │           └── ItemController.java
│   ├── Dockerfile
│   └── pom.xml
├── orderservice/            # Order management service
│   ├── src/
│   ├── Dockerfile
│   └── pom.xml
├── paymentservice/          # Payment processing service
│   ├── src/
│   ├── Dockerfile
│   └── pom.xml
└── docker-compose.yml       # Docker Compose configuration
```

## ⚙️ Configuration

### Service Ports

| Service | Port | Access URL |
|---------|------|------------|
| API Gateway | 8086 | http://localhost:8086 |
| Item Service | 8089 | http://localhost:8089 (direct) |
| Order Service | 8088 | http://localhost:8088 (direct) |
| Payment Service | 8087 | http://localhost:8087 (direct) |

### Application Properties

Each service has its own `application.properties`:

**Item Service** ([`itemservice/src/main/resources/application.properties`](itemservice/src/main/resources/application.properties)):
```properties
spring.application.name=item-service
server.port=8089
```

**API Gateway** ([`apigateway/src/main/resources/application.properties`](apigateway/src/main/resources/application.properties)):
```properties
spring.application.name=api-gateway
server.port=8086

spring.cloud.gateway.routes[0].id=item-service
spring.cloud.gateway.routes[0].uri=http://item-service:8089
spring.cloud.gateway.routes[0].predicates[0]=Path=/items/**

spring.cloud.gateway.routes[1].id=order-service
spring.cloud.gateway.routes[1].uri=http://order-service:8088
spring.cloud.gateway.routes[1].predicates[0]=Path=/orders/**

spring.cloud.gateway.routes[2].id=payment-service
spring.cloud.gateway.routes[2].uri=http://payment-service:8087
spring.cloud.gateway.routes[2].predicates[0]=Path=/payments/**
```

## 🐳 Docker

### Individual Service Dockerfile

Each service uses the same Dockerfile structure:

```dockerfile
FROM eclipse-temurin:17-jdk-alpine
WORKDIR /app
COPY target/*.jar app.jar
EXPOSE 808X
ENTRYPOINT ["java", "-jar", "app.jar"]
```

### Docker Compose

The [`docker-compose.yml`](docker-compose.yml) orchestrates all services:

```yaml
services:
  api-gateway:
    build: ./apigateway
    ports:
      - "8086:8086"
    depends_on:
      - item-service
      - order-service
      - payment-service
  # ... other services
```

## 🧪 Testing

### Run Tests

```bash
# Test individual service
cd itemservice
mvnw test

# Test all services
mvnw test
```

### Manual Testing

Use the provided curl commands or tools like Postman to test the endpoints.

## 🔧 Troubleshooting

### Docker Desktop Not Running
```
Error: open //./pipe/dockerDesktopLinuxEngine: The system cannot find the file specified
```
**Solution**: Start Docker Desktop and wait for it to fully initialize.

### Java Version Mismatch
```
Error: release version 21 not supported
```
**Solution**: Ensure your [`pom.xml`](itemservice/pom.xml) matches your installed Java version, or install the required Java version.

### Port Already in Use
```
Error: Bind for 0.0.0.0:8086 failed: port is already allocated
```
**Solution**: Stop the service using the port or change the port in `application.properties` and [`docker-compose.yml`](docker-compose.yml).

### Build Failures
```
Error: Failed to execute goal maven-compiler-plugin
```
**Solution**: 
1. Clean Maven cache: `mvnw clean`
2. Update Maven wrapper: `mvnw wrapper:wrapper`
3. Check JAVA_HOME environment variable

## 📝 Development

### Adding a New Microservice

1. Create a new Spring Boot project
2. Add a Dockerfile
3. Update [`docker-compose.yml`](docker-compose.yml)
4. Add routes in API Gateway's `application.properties`
5. Build and deploy

### Hot Reload (Development)

For development without Docker:

```bash
# Terminal 1 - Item Service
cd itemservice
mvnw spring-boot:run

# Terminal 2 - Order Service
cd orderservice
mvnw spring-boot:run

# Terminal 3 - Payment Service
cd paymentservice
mvnw spring-boot:run

# Terminal 4 - API Gateway
cd apigateway
mvnw spring-boot:run
```
---

**Happy Coding! 🚀**