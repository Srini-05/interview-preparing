# Microservices

> **Note:** Interview Tips are highlighted in <span style="color: #007acc;">blue</span> for easy identification.
> **Accordion Feature:** Each question can be made collapsible by wrapping in `<details><summary>Question Title</summary> content </details>`.

<details><summary>🏗️ Microservices Interview Preparation Guide</summary>

<details><summary style="font-size: 1.3em; font-weight: bold;">What are Microservices?</summary>

Microservices architecture is an approach to building applications as a collection of small, independent services that communicate over well-defined APIs. Each service is responsible for a specific business capability and can be developed, deployed, and scaled independently.

### Core Principles:
1. **Single Responsibility**: Each service handles one business function
2. **Independence**: Services can be developed by different teams using different technologies
3. **Decentralized Data**: Each service owns its data and database
4. **API-First Design**: Services communicate through APIs, not direct database access
5. **Failure Isolation**: Failure in one service doesn't bring down the entire system

### Real-World Analogy:
Think of a restaurant kitchen:
- **Monolith**: One big kitchen where everyone works together, sharing equipment and space
- **Microservices**: Specialized stations (grill, salad, dessert) that work independently but coordinate through the head chef (API gateway)

### Service Characteristics:
```java
// User Service - handles user management
@RestController
@RequestMapping("/users")
public class UserController {
    @PostMapping
    public User createUser(@RequestBody User user) {
        return userService.create(user);
    }

    @GetMapping("/{id}")
    public User getUser(@PathVariable Long id) {
        return userService.findById(id);
    }
}

// Order Service - handles order processing
@RestController
@RequestMapping("/orders")
public class OrderController {
    @PostMapping
    public Order createOrder(@RequestBody OrderRequest request) {
        // Calls User Service to validate user
        // Calls Inventory Service to check stock
        // Calls Payment Service to process payment
        return orderService.create(request);
    }
}
```

### Benefits:
- **Scalability**: Scale individual services based on demand
- **Technology Diversity**: Use different languages/frameworks per service
- **Faster Deployment**: Deploy services independently
- **Fault Isolation**: One service failure doesn't crash everything
- **Team Autonomy**: Teams can work independently

### Challenges:
- **Complexity**: Distributed systems are harder to debug
- **Data Consistency**: Managing consistency across services
- **Service Discovery**: Finding services at runtime
- **Testing**: Integration testing is more complex
- **Operational Overhead**: More infrastructure to manage

### Interview Explanation:
"Microservices break down monolithic applications into small, independent services that communicate via APIs. Each service owns its data, can be deployed separately, and focuses on one business capability. This enables teams to work independently, scale services individually, and use the best technology for each job. However, it introduces complexity in areas like service discovery, distributed transactions, and monitoring. I choose microservices when the application is large enough to benefit from independent scaling and when teams are organized around business domains."

**Interview Tip:** Microservices break monoliths into manageable services. Each service is a mini-app with its own data and deployment cycle.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">🚀 Spring Boot Annotations (Detailed Table)</summary>

### Core Component Annotations

| Annotation | Explanation |
|------------|-------------|
| `@Component` | • Marks a class as a Spring bean<br>• Automatically detected during component scan<br>• Used for generic components |
| `@Service` | • Special type of @Component<br>• Used in service layer<br>• Contains business logic |
| `@Repository` | • Used for DAO layer<br>• Handles database operations<br>• Provides exception translation |
| `@Controller` | • Handles web requests<br>• Returns view (HTML/JSP)<br>• Used in MVC applications |
| `@RestController` | • Combines @Controller + @ResponseBody<br>• Returns JSON/XML directly<br>• Used for REST APIs |

### Dependency Injection Annotations

| Annotation | Explanation |
|------------|-------------|
| `@Autowired` | • Injects dependencies automatically<br>• Removes need for manual object creation<br>• Works by type |
| `@Qualifier` | • Resolves multiple bean conflict<br>• Specifies exact bean to inject<br>• Used with @Autowired |
| `@Value` | • Injects values from properties file<br>• Used for configuration values<br>• Example: `${server.port}` |
| `@Configuration` | • Marks class as configuration class<br>• Used to define beans<br>• Replaces XML config |
| `@Bean` | • Creates and manages bean manually<br>• Defined inside @Configuration class<br>• Useful for third-party classes |

### HTTP Request Mapping Annotations

| Annotation | Explanation |
|------------|-------------|
| `@RequestMapping` | • Maps HTTP requests to methods<br>• Supports all HTTP methods<br>• Can be used at class & method level |
| `@GetMapping` | • Handles GET requests<br>• Shortcut for @RequestMapping(method=GET)<br>• Used to fetch data |
| `@PostMapping` | • Handles POST requests<br>• Used to create data<br>• Sends data in request body |
| `@PutMapping` | • Handles PUT requests<br>• Used to update data<br>• Idempotent operation |
| `@DeleteMapping` | • Handles DELETE requests<br>• Used to delete resources<br>• Returns status response |

### Parameter Binding Annotations

| Annotation | Explanation |
|------------|-------------|
| `@PathVariable` | • Extracts value from URL path<br>• Used in REST APIs<br>• Example: `/user/{id}` |
| `@RequestParam` | • Gets query parameters<br>• Example: `/user?id=1`<br>• Optional or required |
| `@RequestBody` | • Converts JSON to Java object<br>• Used in POST/PUT APIs<br>• Uses HTTP request body |
| `@ResponseBody` | • Converts Java object to JSON<br>• Sends response directly<br>• Used in REST APIs |

### Application Configuration Annotations

| Annotation | Explanation |
|------------|-------------|
| `@SpringBootApplication` | • Main Spring Boot annotation<br>• Combines 3 annotations<br>• Starts application |
| `@EnableAutoConfiguration` | • Automatically configures Spring Boot<br>• Based on dependencies<br>• Reduces manual setup |
| `@ComponentScan` | • Scans packages for beans<br>• Detects @Component, @Service etc.<br>• Registers them in context |

### JPA/Entity Annotations

| Annotation | Explanation |
|------------|-------------|
| `@Entity` | • Marks class as DB entity<br>• Maps to table<br>• Used in JPA |
| `@Table` | • Specifies table name<br>• Used with @Entity<br>• Optional if names match |
| `@Id` | • Marks primary key<br>• Unique identifier<br>• Required in entity |
| `@GeneratedValue` | • Auto-generates ID<br>• Supports strategies (AUTO, IDENTITY)<br>• Used with @Id |
| `@Column` | • Maps field to column<br>• Can define name, length, nullable<br>• Optional customization |
| `@OneToMany` | • One entity → many entities<br>• Example: One user → many orders<br>• Defines relationship |
| `@ManyToOne` | • Many entities → one entity<br>• Example: Many orders → one user<br>• Foreign key mapping |

**Interview Tip:** Spring Boot annotations reduce boilerplate code. @Autowired injects dependencies, @RestController creates REST endpoints, @Entity maps to database tables.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">Monolith vs Microservices</summary>

### Monolithic Architecture
A monolithic application is a single, unified codebase where all components are tightly coupled and deployed as one unit. This was the traditional way of building applications.

#### Characteristics:
- **Single Codebase**: All features in one repository
- **Shared Database**: All components access the same database
- **Tight Coupling**: Components depend heavily on each other
- **Single Deployment**: Entire application deployed together
- **Technology Stack**: Usually one language/framework
- **Development**: One team works on everything

#### Example Structure:
```
monolithic-app/
├── controllers/
│   ├── UserController.java
│   ├── OrderController.java
│   └── PaymentController.java
├── services/
│   ├── UserService.java
│   ├── OrderService.java
│   └── PaymentService.java
├── repositories/
│   ├── UserRepository.java
│   ├── OrderRepository.java
│   └── PaymentRepository.java
└── models/
    ├── User.java
    ├── Order.java
    └── Payment.java
```

#### Advantages:
- **Simple Development**: Easy to develop and test locally
- **Single Deployment**: Simple CI/CD pipelines
- **Performance**: No network overhead between components
- **Transactions**: Easy ACID transactions across components
- **Debugging**: Simple stack traces and logging

#### Disadvantages:
- **Scalability Issues**: Can't scale individual features
- **Technology Lock-in**: Hard to adopt new technologies
- **Large Codebase**: Difficult to maintain and understand
- **Deployment Risk**: Bug in one feature affects entire application
- **Team Coordination**: Large teams working on same codebase

### Microservices Architecture
An application built as a collection of small, independent services that communicate through APIs. Each service is responsible for a specific business capability.

#### Characteristics:
- **Independent Services**: Each service is a separate application
- **Database per Service**: Each service owns its data
- **Loose Coupling**: Services communicate via APIs/events
- **Independent Deployment**: Deploy services separately
- **Technology Diversity**: Different tech stacks per service
- **Team Autonomy**: Teams own entire service lifecycle

#### Example Structure:
```
microservices-app/
├── user-service/
│   ├── src/main/java/com/app/user/
│   ├── Dockerfile
│   └── deployment.yaml
├── order-service/
│   ├── src/main/java/com/app/order/
│   ├── Dockerfile
│   └── deployment.yaml
├── payment-service/
│   ├── src/main/java/com/app/payment/
│   ├── Dockerfile
│   └── deployment.yaml
├── api-gateway/
│   ├── src/main/java/com/app/gateway/
│   ├── Dockerfile
│   └── deployment.yaml
└── service-discovery/
    ├── eureka-server/
    └── config-server/
```

#### Advantages:
- **Independent Scaling**: Scale services based on demand
- **Technology Freedom**: Choose best tech for each service
- **Fault Isolation**: One service failure doesn't crash others
- **Faster Deployment**: Deploy services independently
- **Team Autonomy**: Teams work independently with clear boundaries
- **Easier Maintenance**: Smaller codebases are easier to understand

#### Disadvantages:
- **Complexity**: Distributed systems are harder to design/debug
- **Network Latency**: API calls add overhead
- **Data Consistency**: Managing consistency across services
- **Testing Complexity**: Integration testing is harder
- **Operational Overhead**: More infrastructure to manage

### Migration Strategy:
1. **Strangler Pattern**: Gradually replace monolith parts with microservices
2. **Anti-Corruption Layer**: Interface between old and new systems
3. **Parallel Run**: Run both systems until new one is proven

### When to Choose What:
- **Start with Monolith**: For small teams, simple applications, proof-of-concepts
- **Migrate to Microservices**: When application grows, teams scale, need independent deployments
- **Hybrid Approach**: Keep core as monolith, extract high-traffic features as services

### Interview Explanation:
"Monoliths are like a single-family home - simple to build and maintain but hard to expand. Microservices are like a neighborhood of houses - each independent but requiring coordination. I start with monoliths for simplicity, then migrate to microservices when scaling needs arise. The key is understanding the trade-offs: monoliths are easier to develop but harder to scale, while microservices offer flexibility at the cost of complexity. I use the strangler pattern for migration, gradually replacing monolith parts with services."

**Interview Tip:** Monoliths are simple to start, microservices for scalability. Migration is complex - use strangler pattern.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">REST vs Async Communication</summary>

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

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">Service Discovery</summary>

Service discovery allows microservices to dynamically locate and communicate with each other at runtime without hard-coding network details.

Service Discovery = "How one service finds another service at runtime."

Tools: Eureka, Consul, Kubernetes DNS.

Example: Service registers with Eureka, client looks up via Eureka client.

**Interview Tip:** Essential in dynamic environments like Kubernetes.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">API Gateway</summary>

An API Gateway acts as a single entry point for all client requests in a microservices architecture. It handles cross-cutting concerns like routing, authentication, rate limiting, and response aggregation, allowing backend services to focus on business logic.

### Core Responsibilities:

#### 1. **Request Routing**
Routes requests to appropriate microservices based on URL patterns.

```yaml
# Spring Cloud Gateway Configuration
spring:
  cloud:
    gateway:
      routes:
      - id: user-service
        uri: lb://user-service  # Load balanced
        predicates:
        - Path=/api/users/**
        filters:
        - RewritePath=/api/users/(?<path>.*), /${path}
      - id: order-service
        uri: lb://order-service
        predicates:
        - Path=/api/orders/**
        filters:
        - RewritePath=/api/orders/(?<path>.*), /${path}
```

#### 2. **Authentication & Authorization**
Centralized security handling.

```java
@Configuration
public class GatewaySecurityConfig {

    @Bean
    public SecurityWebFilterChain securityWebFilterChain(ServerHttpSecurity http) {
        return http
            .authorizeExchange()
                .pathMatchers("/api/public/**").permitAll()
                .pathMatchers("/api/admin/**").hasRole("ADMIN")
                .anyExchange().authenticated()
            .and()
            .oauth2Login()
            .and()
            .build();
    }
}
```

#### 3. **Rate Limiting**
Prevents abuse and ensures fair usage.

```yaml
spring:
  cloud:
    gateway:
      routes:
      - id: api-route
        uri: lb://service
        filters:
        - name: RequestRateLimiter
          args:
            redis-rate-limiter.replenishRate: 10  # requests per second
            redis-rate-limiter.burstCapacity: 20   # burst capacity
```

#### 4. **Response Aggregation**
Combines data from multiple services into a single response.

```java
@RestController
public class ProductController {

    @Autowired
    private WebClient.Builder webClientBuilder;

    @GetMapping("/products/{id}")
    public Mono<ProductDetails> getProductDetails(@PathVariable String id) {
        // Get product info
        Mono<Product> product = webClientBuilder.build()
            .get().uri("lb://product-service/products/" + id)
            .retrieve().bodyToMono(Product.class);

        // Get inventory
        Mono<Inventory> inventory = webClientBuilder.build()
            .get().uri("lb://inventory-service/inventory/" + id)
            .retrieve().bodyToMono(Inventory.class);

        // Get reviews
        Mono<List<Review>> reviews = webClientBuilder.build()
            .get().uri("lb://review-service/reviews/product/" + id)
            .retrieve().bodyToFlux(Review.class)
            .collectList();

        // Aggregate all data
        return Mono.zip(product, inventory, reviews)
            .map(tuple -> new ProductDetails(
                tuple.getT1(),
                tuple.getT2(),
                tuple.getT3()
            ));
    }
}
```

#### 5. **Cross-Cutting Concerns**
- **Logging**: Request/response logging
- **Metrics**: Performance monitoring
- **Caching**: Response caching
- **CORS**: Cross-origin resource sharing
- **Request/Response Transformation**: Modify requests/responses

### Popular API Gateway Solutions:

#### Spring Cloud Gateway
- Built on Spring WebFlux (reactive)
- Java-based configuration
- Integration with Spring ecosystem
- Good for Java microservices

#### Netflix Zuul
- Blocking I/O
- Mature and battle-tested
- Good for Netflix-style architectures

#### Kong
- Plugin-based architecture
- Supports multiple languages
- Enterprise features
- Good for API management

#### AWS API Gateway
- Managed service
- Serverless integration
- Built-in authentication
- Auto-scaling

### Gateway Patterns:

#### Backend for Frontend (BFF)
Different gateways for different client types (mobile, web, etc.).

```
Mobile App → Mobile Gateway → Services
Web App    → Web Gateway    → Services
```

#### Gateway Aggregation
Gateway calls multiple services and aggregates responses.

### Interview Explanation:
"API Gateway is the single entry point for microservices, handling routing, security, rate limiting, and response aggregation. It prevents clients from knowing about individual services and allows backend services to focus on business logic. I use Spring Cloud Gateway for Java ecosystems because of its reactive nature and Spring integration. For complex scenarios, I implement response aggregation where the gateway calls multiple services and combines their data. The key benefits are centralized cross-cutting concerns and simplified client communication."

**Interview Tip:** Gateway handles auth, logging, etc., keeping services focused on business logic. Use for routing, security, rate limiting, and aggregation.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">Resilience in Microservices</summary>

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

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">Communication Patterns</summary>

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

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">Data Management</summary>

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

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">Deployment & Scaling</summary>

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

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">Challenges</summary>

- Service discovery
- Distributed tracing
- Configuration management
- Testing complexity
- Data consistency

**Interview Tip:** Use tools like Zipkin for tracing, Config Server for configs.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">Tools & Technologies</summary>

- Spring Boot/Cloud for Java
- Docker/Kubernetes
- API Gateway (Spring Cloud Gateway, Zuul)
- Service Discovery (Eureka, Consul)
- Messaging (Kafka, RabbitMQ)
- Monitoring (ELK stack, Prometheus)

**Interview Tip:** Microservices require DevOps skills. Start with Spring Cloud for Java.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">Interview Questions</summary>

<details><summary style="font-size: 1.3em; font-weight: bold;">What are microservices and their benefits?</summary>

**Explanation:** Microservices are small, independent services that work together to form an application, each handling a specific business function.

**Example:** User Service, Order Service, Payment Service instead of one monolithic app.

**Real-time Example:** Netflix uses microservices so their video streaming, user recommendations, and billing can scale independently.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">Explain service discovery and why it's important.</summary>

**Explanation:** Service discovery allows services to find and communicate with each other dynamically, without hard-coded addresses.

**Example:** Using Eureka server where services register themselves and clients query for locations.

**Real-time Example:** In a cloud environment like AWS, services scale up/down, and discovery ensures load balancers route traffic correctly.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">What is an API Gateway and its role?</summary>

**Explanation:** API Gateway is a single entry point for clients, handling routing, authentication, rate limiting, and aggregating responses from multiple services.

**Example:** Gateway routes /users to User Service, /orders to Order Service, and combines data if needed.

**Real-time Example:** Amazon API Gateway handles millions of requests, authenticating users and routing to backend services securely.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">How do you handle data consistency in microservices?</summary>

**Explanation:** Use patterns like Saga for distributed transactions, event sourcing, or eventual consistency instead of traditional ACID.

**Example:** Saga pattern: Orchestrate compensating actions if a step fails (e.g., cancel order if payment fails).

**Real-time Example:** In Uber, booking a ride involves multiple services; sagas ensure if driver assignment fails, the booking is rolled back.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">What are circuit breakers and why use them?</summary>

**Explanation:** Circuit breakers prevent cascading failures by stopping calls to a failing service and allowing fallback responses.

**Example:** If Inventory Service is down, circuit breaker opens, returns cached data or default response.

**Real-time Example:** During high traffic, if a payment service slows, circuit breaker protects the order service from hanging.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">Explain synchronous vs asynchronous communication in microservices.</summary>

**Explanation:** Synchronous uses HTTP/REST for immediate responses, asynchronous uses messaging for decoupling and scalability.

**Example:** REST call for user details (synchronous), event publishing for order updates (asynchronous).

**Real-time Example:** In e-commerce, payment processing is synchronous (wait for approval), inventory updates are asynchronous (event-driven).

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">What is distributed tracing and why is it important?</summary>

**Explanation:** Distributed tracing tracks requests across multiple services to identify performance bottlenecks and failures.

**Example:** Tools like Zipkin or Jaeger trace a request from API Gateway through multiple services.

**Real-time Example:** In a complex system, tracing helps identify why a user registration is slow by showing time spent in each service.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">How do you handle configuration in microservices?</summary>

**Explanation:** Use centralized configuration servers like Spring Cloud Config to manage configs across all services.

**Example:** Config server stores database URLs, feature flags, shared across dev/staging/prod environments.

**Real-time Example:** Change log level from INFO to DEBUG for all services without redeployment.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">What are the challenges of microservices and how to overcome them?</summary>

**Explanation:** Challenges include distributed transactions, service discovery, monitoring. Overcome with sagas, service mesh, centralized logging.

**Example:** Use event sourcing for data consistency, circuit breakers for resilience.

**Real-time Example:** Netflix solved scaling challenges with microservices, using tools like Hystrix for resilience.

</details>

</details>

</details>
