# Microservices

## What are Microservices?

Microservices are an architectural style where an application is built as a collection of small, independent services, each responsible for a specific business capability.

Microservices are an architectural approach where applications are composed of small, independent services that are loosely coupled, independently deployable, and aligned with business capabilities.

### Key Characteristics of Microservices
- Single responsibility (one business function per service)
- Independently deployable
- Loosely coupled
- Technology independent (polyglot)
- Own their own data

**Interview Tip:** Microservices break monoliths into manageable services. Each service is a mini-app.

## Monolith vs Microservices

### Monolith Architecture
A monolithic application is built as one single, tightly coupled unit.
Characteristics:
- Single codebase
- Single deployment
- Shared database
- All features packaged together

Example: One app handling User management, Orders, Payments, Inventory - all deployed together.

### Microservices Architecture
An application built as multiple small, independent services, each handling a specific business capability.
Characteristics:
- Independent services
- Independent deployments
- Each service owns its data
- Communicate via APIs or events

Example:
- User Service
- Order Service
- Payment Service
- Inventory Service
- Each can scale and deploy separately.

A monolith is a single deployable application, while microservices split the system into independently deployable services aligned with business capabilities.

**Interview Tip:** Monoliths are simple to start, microservices for scalability. Migration is complex.

## REST vs Async Communication

REST is commonly used for synchronous communication where an immediate response is required, while asynchronous communication uses events or messages to achieve loose coupling, scalability, and resilience.

### Sync vs Async
Synchronous communication requires the caller to wait for a response, while asynchronous communication allows processing to continue without waiting, improving scalability and resilience.

Real-World Example: Order placement
- Sync → validate user, check inventory
- Async → send confirmation email, update reports

Example Sync (REST):
```java
ResponseEntity<Order> response = restTemplate.postForEntity("/orders", order, Order.class);
```

Example Async (Kafka):
```java
kafkaTemplate.send("order-created", order);
```

**Interview Tip:** Sync for immediate responses, async for decoupling and scalability.

## Service Discovery

Service discovery allows microservices to dynamically locate and communicate with each other at runtime without hard-coding network details.

Service Discovery = "How one service finds another service at runtime."

Tools: Eureka, Consul, Kubernetes DNS.

Example: Service registers with Eureka, client looks up via Eureka client.

**Interview Tip:** Essential in dynamic environments like Kubernetes.

## API Gateway

An API Gateway is needed to provide a single entry point for clients, handling routing, security, rate limiting, and other cross-cutting concerns in a microservices architecture.

API Gateway = one door for many microservices.

Example: One API call → User + Order + Payment data

### Benefits
1. Single Entry Point
2. Routing & Request Aggregation
3. Security
4. Rate Limiting & Throttling
5. Load Balancing
6. Cross-Cutting Concerns
7. API Versioning & Backward Compatibility

Tools: Spring Cloud Gateway, Zuul, Kong.

Example Configuration:
```yaml
spring:
  cloud:
    gateway:
      routes:
      - id: user-service
        uri: lb://user-service
        predicates:
        - Path=/users/**
```

**Interview Tip:** Gateway handles auth, logging, etc., keeping services focused on business logic.

## Resilience in Microservices

If one microservice is down, dependent requests may fail, but with resilience patterns like circuit breakers, retries, fallbacks, and asynchronous messaging, the system can isolate failures, degrade gracefully, and recover without impacting all services.

Patterns:
- Circuit Breaker: Stop calling failing service
- Retry: Retry failed calls
- Fallback: Return default response
- Bulkhead: Isolate failures

Example with Resilience4j:
```java
@CircuitBreaker(name = "inventory", fallbackMethod = "fallbackInventory")
public Mono<Inventory> checkInventory(String itemId) {
    return webClient.get().uri("/inventory/" + itemId).retrieve().bodyToMono(Inventory.class);
}

public Mono<Inventory> fallbackInventory(String itemId, Throwable t) {
    return Mono.just(new Inventory(itemId, 0)); // default
}
```

**Interview Tip:** Resilience prevents cascading failures. Use libraries like Resilience4j.

## Communication Patterns

### Synchronous
- REST, gRPC
- Immediate response
- Tight coupling

Example REST:
```java
@GetMapping("/users/{id}")
public User getUser(@PathVariable String id) {
    return userService.getUser(id);
}
```

### Asynchronous
- Message queues (Kafka, RabbitMQ)
- Event-driven
- Loose coupling

Example Kafka Producer:
```java
@Autowired
private KafkaTemplate<String, OrderEvent> kafkaTemplate;

public void createOrder(Order order) {
    kafkaTemplate.send("order-events", new OrderEvent(order));
}
```

**Interview Tip:** Sync for simple, async for complex workflows.

## Data Management

Each microservice owns its data, but challenges arise with distributed transactions.

### Patterns
- Database per service
- Event sourcing
- Saga pattern for distributed transactions

Example Saga:
- Step 1: Create order
- Step 2: Reserve inventory
- Step 3: Process payment
- If payment fails, compensate by releasing inventory

**Interview Tip:** Avoid distributed transactions; use sagas or events.

## Deployment & Scaling

- Containerization (Docker)
- Orchestration (Kubernetes)
- Independent scaling
- CI/CD pipelines

Example Dockerfile:
```dockerfile
FROM openjdk:11
COPY target/app.jar app.jar
ENTRYPOINT ["java","-jar","app.jar"]
```

Example Kubernetes Deployment:
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: user-service
spec:
  replicas: 3
  selector:
    matchLabels:
      app: user-service
  template:
    metadata:
      labels:
        app: user-service
    spec:
      containers:
      - name: user-service
        image: user-service:latest
        ports:
        - containerPort: 8080
```

**Interview Tip:** Docker for packaging, Kubernetes for orchestration.

## Challenges
- Service discovery
- Distributed tracing
- Configuration management
- Testing complexity
- Data consistency

**Interview Tip:** Use tools like Zipkin for tracing, Config Server for configs.

## Tools & Technologies
- Spring Boot/Cloud for Java
- Docker/Kubernetes
- API Gateway (Spring Cloud Gateway, Zuul)
- Service Discovery (Eureka, Consul)
- Messaging (Kafka, RabbitMQ)
- Monitoring (ELK stack, Prometheus)

**Interview Tip:** Microservices require DevOps skills. Start with Spring Cloud for Java.