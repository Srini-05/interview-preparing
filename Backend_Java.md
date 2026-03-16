# Backend - Java Basics

> **Note:** Interview Tips are highlighted in <span style="color: #007acc;">blue</span> for easy identification.
> **Accordion Feature:** Each question can be made collapsible by wrapping in `<details><summary>Question Title</summary> content </details>` (demonstrated for first few questions).

## Basic Java Interview Questions

<details>
<summary>1. What is Java?</summary>

Java is a high-level, object-oriented programming language developed by Sun Microsystems (now Oracle). It is platform-independent due to the JVM (Java Virtual Machine), which allows "Write Once, Run Anywhere" (WORA).

**Key Features:**
- Object-Oriented
- Platform-Independent
- Secure
- Robust
- Multithreaded
- Interpreted and Compiled

<span style="color: #007acc;">**Interview Tip:**</span> Emphasize platform-independence via bytecode and JVM.
</details>

</details>

<details>
<summary>2. What are the data types in Java?</summary>

Java has two types of data types: Primitive and Non-Primitive (Reference).

**Primitive Data Types:**
- byte (8-bit, -128 to 127)
- short (16-bit, -32,768 to 32,767)
- int (32-bit, -2^31 to 2^31-1)
- long (64-bit, -2^63 to 2^63-1)
- float (32-bit, IEEE 754)
- double (64-bit, IEEE 754)
- char (16-bit, Unicode)
- boolean (true/false)

**Non-Primitive (Reference):**
- Classes, Interfaces, Arrays, Strings

Example:
```java
int age = 25;
String name = "John";
```

<span style="color: #007acc;">**Interview Tip:**</span> Know the size and range of primitives. Strings are immutable objects.
</details>

</details>

<details>
<summary>3. What are the access modifiers in Java?</summary>

Access modifiers control the visibility of classes, methods, and variables.

- **public:** Accessible from anywhere.
- **protected:** Accessible within the same package and subclasses.
- **default (no modifier):** Accessible within the same package.
- **private:** Accessible only within the same class.

Example:
```java
public class Car {
    private String model;
    protected int year;
    public void drive() { }
}
```

<span style="color: #007acc;">**Interview Tip:**</span> private for encapsulation, public for APIs.
</details>

</details>

<details>
<summary>4. What is the difference between == and equals()?</summary>

- **==** compares reference equality (memory addresses) for objects, value equality for primitives.
- **equals()** compares content/value equality for objects.

Example:
```java
String s1 = new String("Hello");
String s2 = new String("Hello");
System.out.println(s1 == s2); // false (different objects)
System.out.println(s1.equals(s2)); // true (same content)
```

<span style="color: #007acc;">**Interview Tip:**</span> Override equals() and hashCode() together in custom classes.
</details>

### 5. What is the static keyword?
Static members belong to the class rather than instances.

- Static variables: Shared among all instances.
- Static methods: Can be called without creating an object.
- Static blocks: Executed when the class is loaded.

Example:
```java
class Counter {
    static int count = 0;
    Counter() { count++; }
    static void showCount() { System.out.println(count); }
}
```

**Interview Tip:** Static methods cannot access instance variables. Used for utility methods.

### 6. What is the final keyword?
Final makes variables, methods, or classes unchangeable.

- Final variable: Cannot be reassigned.
- Final method: Cannot be overridden.
- Final class: Cannot be subclassed.

Example:
```java
final int MAX = 100;
final class MathUtils { }
```

<span style="color: #007acc;">**Interview Tip:**</span> Final for constants, security, and performance.

### 7. What is the difference between String, StringBuffer, and StringBuilder?
- **String:** Immutable, thread-safe, slow for modifications.
- **StringBuffer:** Mutable, thread-safe, synchronized.
- **StringBuilder:** Mutable, not thread-safe, faster.

Example:
```java
String s = "Hello";
s += " World"; // Creates new string

StringBuilder sb = new StringBuilder("Hello");
sb.append(" World"); // Modifies same object
```

**Interview Tip:** Use StringBuilder for single-threaded string manipulations, StringBuffer for multi-threaded.

### 8. What are arrays in Java?
Arrays are fixed-size, homogeneous data structures.

Declaration: `int[] arr = new int[5];`
Initialization: `int[] arr = {1, 2, 3, 4, 5};`

**Interview Tip:** Arrays have fixed size; use ArrayList for dynamic size.

### 9. What is inheritance in Java?
Inheritance allows a class to inherit properties and methods from another class using `extends`.

Example:
```java
class Animal {
    void eat() { System.out.println("Eating"); }
}

class Dog extends Animal {
    void bark() { System.out.println("Barking"); }
}
```

**Interview Tip:** Java supports single inheritance. Use interfaces for multiple inheritance.

### 10. What are interfaces in Java?
Interfaces define a contract with abstract methods. Classes implement interfaces using `implements`.

Example:
```java
interface Animal {
    void sound();
}

class Dog implements Animal {
    public void sound() { System.out.println("Bark"); }
}
```

**Interview Tip:** All methods are public abstract by default. From Java 8, can have default and static methods.

### 11. What are abstract classes?
Abstract classes cannot be instantiated and may contain abstract methods.

Example:
```java
abstract class Shape {
    abstract void draw();
}

class Circle extends Shape {
    void draw() { System.out.println("Drawing circle"); }
}
```

**Interview Tip:** Use abstract classes when sharing code, interfaces when defining contracts.

### 12. What is method overloading and overriding?
- **Overloading:** Same method name, different parameters in the same class (compile-time polymorphism).
- **Overriding:** Same method signature in subclass (runtime polymorphism).

Example Overloading:
```java
void print(int i) { }
void print(String s) { }
```

Example Overriding:
```java
class Parent {
    void show() { }
}

class Child extends Parent {
    @Override
    void show() { }
}
```

**Interview Tip:** Overloading changes behavior, overriding replaces behavior.

### 13. What is a constructor?
Constructors initialize objects. Same name as class, no return type.

Types: Default, Parameterized, Copy.

Example:
```java
class Person {
    String name;
    Person(String name) { this.name = name; }
}
```

**Interview Tip:** If no constructor, Java provides default. Cannot be inherited.

### 14. What is the this keyword?
`this` refers to the current object instance.

Uses: Differentiate instance variables, call other constructors, pass current object.

Example:
```java
class Person {
    String name;
    Person(String name) { this.name = name; }
}
```

**Interview Tip:** Used to avoid name conflicts.

### 15. What is the super keyword?
`super` refers to the parent class.

Uses: Call parent constructor, access parent methods/variables.

Example:
```java
class Dog extends Animal {
    Dog() { super(); } // calls parent constructor
}
```

**Interview Tip:** Must be first statement in constructor.

### 16. What are packages in Java?
Packages organize classes and avoid name conflicts.

Example: `import java.util.*;`

**Interview Tip:** Use reverse domain naming convention.

### 17. What is the difference between ArrayList and LinkedList?
- **ArrayList:** Dynamic array, fast random access, slow insertions/deletions.
- **LinkedList:** Doubly linked list, fast insertions/deletions, slow random access.

**Interview Tip:** Choose based on use case: ArrayList for reads, LinkedList for modifications.

### 18. What is the difference between HashSet and TreeSet?
- **HashSet:** Unordered, uses hash, faster.
- **TreeSet:** Ordered, uses red-black tree, slower.

**Interview Tip:** HashSet for uniqueness, TreeSet for sorted order.

### 19. What is the difference between HashMap and HashTable?
- **HashMap:** Not synchronized, allows null keys/values, faster.
- **HashTable:** Synchronized, doesn't allow null, thread-safe but slower.

**Interview Tip:** Use HashMap for single-threaded, ConcurrentHashMap for multi-threaded.

### 20. What is the try-with-resources statement?
Automatically closes resources that implement AutoCloseable.

Example:
```java
try (FileReader fr = new FileReader("file.txt")) {
    // use fr
} // automatically closed
```

**Interview Tip:** Prevents resource leaks.

## 1. What is the difference between RestTemplate and WebClient?

In Spring Framework / Spring Boot, both RestTemplate and WebClient are used to call external REST APIs, but they differ mainly in programming model and performance.

### RestTemplate
- Blocking (Synchronous)
- One request → thread waits until response
- Simple to use
- Older API (now in maintenance mode)

Example:
```java
RestTemplate restTemplate = new RestTemplate();
String response = restTemplate.getForObject("https://api.example.com/users", String.class);
```

Additional Example: Posting data
```java
User user = new User("John", "Doe");
ResponseEntity<String> response = restTemplate.postForEntity("https://api.example.com/users", user, String.class);
```

### WebClient
- Non-blocking (Reactive)
- Supports asynchronous calls
- High performance
- Works with Reactive Streams (Mono / Flux)

Example:
```java
WebClient client = WebClient.create();
Mono<String> response = client.get()
    .uri("https://api.example.com/users")
    .retrieve()
    .bodyToMono(String.class);
```

Additional Example: Handling errors
```java
WebClient client = WebClient.create();
Mono<String> response = client.get()
    .uri("https://api.example.com/users")
    .retrieve()
    .onStatus(HttpStatus::is4xxClientError, clientResponse -> Mono.error(new RuntimeException("Client error")))
    .bodyToMono(String.class);
```

### Key Differences
| Feature          | RestTemplate          | WebClient              |
|------------------|-----------------------|-----------------------|
| Type            | Synchronous          | Asynchronous / Reactive |
| Blocking        | Yes                  | No                    |
| Performance     | Lower under heavy load | Better scalability    |
| Introduced in   | Spring MVC           | Spring WebFlux        |
| Status          | Maintenance mode     | Recommended for new apps |

### When to Use Each
- Use RestTemplate: Legacy Spring applications, simple API calls, no need for reactive programming
- Use WebClient: Microservices, high-concurrency systems, reactive applications

**Interview Tip:** RestTemplate blocks threads, which can lead to performance issues in high-load scenarios. WebClient is non-blocking, making it ideal for reactive applications. Always prefer WebClient for new projects.

## 2. How do you handle microservice communication failures?

In microservices, communication failures can happen due to network issues, service downtime, or high latency. To handle these failures, we use several resilience patterns:

1. Retry Mechanism: If a service call fails temporarily, we retry the request a few times before failing.
2. Circuit Breaker Pattern: Using tools like Resilience4j, the circuit breaker stops calling a failing service and returns a fallback response to avoid cascading failures.
3. Fallback Mechanism: If a service is unavailable, we return a default response or cached data.
4. Timeout Configuration: We configure timeouts so that a service does not wait indefinitely for another service.
5. Global Exception Handling: Inside a microservice, we can use @ControllerAdvice to handle exceptions and return standardized error responses.

Example with Resilience4j:
```java
@CircuitBreaker(name = "userService", fallbackMethod = "fallbackGetUser")
public Mono<User> getUser(String id) {
    return webClient.get().uri("/users/" + id).retrieve().bodyToMono(User.class);
}

public Mono<User> fallbackGetUser(String id, Throwable t) {
    return Mono.just(new User("default", "user"));
}
```

**Interview Tip:** Resilience patterns prevent system-wide failures. Circuit breakers are crucial in microservices to avoid cascading failures. Tools like Hystrix or Resilience4j implement these patterns easily.

## 3. What are the types of Garbage Collectors (GC) in Java?

In Java, Garbage Collectors (GC) automatically manage memory by removing unused objects from the heap. Over different Java versions, several types of GC algorithms have been introduced.

### Types of Garbage Collectors in Java
1. Serial Garbage Collector
   - Uses a single thread for garbage collection.
   - Suitable for small applications and single-CPU environments.
   - It pauses the entire application (Stop-the-World) during GC.
   - JVM option: -XX:+UseSerialGC

2. Parallel Garbage Collector
   - Also called Throughput Collector.
   - Uses multiple threads to perform garbage collection.
   - Focuses on high throughput rather than low pause time.
   - JVM option: -XX:+UseParallelGC

3. CMS (Concurrent Mark Sweep) Garbage Collector
   - Performs most GC work concurrently with the application.
   - Designed to reduce pause times.
   - Now deprecated in newer Java versions.
   - JVM option: -XX:+UseConcMarkSweepGC

4. G1 Garbage Collector
   - Stands for Garbage First GC.
   - Divides the heap into regions and collects the most garbage-filled regions first.
   - Provides predictable pause times.
   - Default GC from Java 9 onward.
   - JVM option: -XX:+UseG1GC

5. ZGC (Z Garbage Collector)
   - Designed for very low latency.
   - Pause times are typically less than 10 ms.
   - Suitable for large heap sizes (TB level).
   - JVM option: -XX:+UseZGC

6. Shenandoah GC
   - Another low-pause garbage collector.
   - Performs concurrent compaction to reduce pause time.
   - JVM option: -XX:+UseShenandoahGC

**Interview Tip:** G1 is the default GC in modern Java. For low-latency applications, choose ZGC or Shenandoah. Serial GC is for small apps, Parallel for throughput, CMS/G1 for balanced performance.

## 4. Explain the end-to-end deployment flow.

Code → Build → Test → Artifact → Deploy → Monitor.

Detailed Flow:
1. Code: Developers write and commit code to version control (e.g., Git).
2. Build: CI/CD tools like Jenkins or GitHub Actions compile the code and run builds.
3. Test: Automated tests (unit, integration) are executed.
4. Artifact: Build artifacts (JAR/WAR) are created and stored in repositories like Nexus.
5. Deploy: Artifacts are deployed to environments (dev, staging, prod) using tools like Kubernetes or Docker.
6. Monitor: Use tools like Prometheus, Grafana to monitor application health, logs, and metrics.

Example: In a Spring Boot app, use Maven to build, then deploy to AWS ECS.

**Interview Tip:** Understand CI/CD pipelines. Deployment involves containerization (Docker) and orchestration (Kubernetes) for scalability.

## 5. Method Overloading vs Method Overriding

### Method Overloading
- Definition: Multiple methods in the same class have the same name but different parameter lists (number or type of parameters).
- Key points:
  - Happens at compile-time (compile-time polymorphism).
  - Return type can be different, but parameters must differ.
  - Same class only (or in subclass, but generally overloading is within the class).

Example:
```java
class Calculator {
    int add(int a, int b) { return a + b; }
    double add(double a, double b) { return a + b; }
}
```

### Method Overriding
- Definition: A subclass provides its own version of a method that is already defined in its parent class.
- Key points:
  - Happens at runtime (runtime polymorphism).
  - Method signature (name + parameters) must be the same.
  - Return type must be the same (or covariant).
  - Access modifier cannot be more restrictive than the parent.
  - Used for implementing specific behavior in subclass.

Example:
```java
class Animal {
    void sound() { System.out.println("Animal sound"); }
}

class Dog extends Animal {
    @Override
    void sound() { System.out.println("Bark"); }
}
```

**Interview Tip:** Overloading is compile-time, overriding is runtime. Overriding requires inheritance and same signature. Use @Override annotation for clarity.

## 6. volatile vs transient Keyword

### volatile Keyword
- Used with variables to tell the JVM that the variable can be modified by multiple threads simultaneously.
- Ensures visibility of changes across threads.
- Key Points:
  - Only applies to instance variables (not local variables).
  - Reads/writes go directly to main memory.
  - Does not guarantee atomicity for compound operations (count++ is not atomic).

Example:
```java
class Example {
    volatile boolean running = true;

    public void stop() {
        running = false; // change is immediately visible to other threads
    }
}
```

### transient Keyword
- Used with variables to indicate that they should not be serialized.
- When an object is written to a stream (e.g., using ObjectOutputStream), transient fields are skipped.
- Key Points:
  - Only affects serialization.
  - After deserialization, transient variables are initialized to default values (0, null, false).

Example:
```java
import java.io.*;

class User implements Serializable {
    String name;
    transient String password; // will not be serialized
}
```

### Key Differences
| Feature          | volatile              | transient             |
|------------------|-----------------------|-----------------------|
| Purpose         | Thread visibility (concurrent programming) | Serialization control |
| Applies to      | Variables             | Variables             |
| Effect          | Reads/writes go to main memory immediately | Field is skipped during serialization |
| Atomicity       | No guarantee for compound operations | Not related to atomicity |
| Default value after serialization/deserialization | N/A | Default value (0, false, null) |
| Use case        | Shared flags, counters, multi-threaded access | Sensitive data, non-persistent fields |

**Interview Tip:** volatile for thread safety in multi-threading, transient for excluding sensitive data from serialization. Never use volatile for atomic operations like increment.

## 7. JDK vs JRE vs JVM

### JDK (Java Development Kit)
- Provides tools to develop and run Java programs.
- Includes JRE + development tools (javac, javadoc, etc.).

### JRE (Java Runtime Environment)
- Provides environment to run Java programs.
- Includes JVM + core libraries.

### JVM (Java Virtual Machine)
- Executes Java bytecode.
- Platform-independent.

Real-Life Example: Cooking
- JVM → Gas stove (actually cooks the food)
- JRE → Kitchen (stove + utensils)
- JDK → Kitchen + recipe book + tools (for cooking)

**Interview Tip:** JDK for development, JRE for running apps, JVM for bytecode execution. JDK includes JRE.

## 8. How Java works internally

Java Source (.java)
    ↓
Java Compiler (javac)
    ↓
Bytecode (.class)
    ↓
ClassLoader
    ↓
Bytecode Verifier
    ↓
Runtime Memory Areas
    ↓
Execution Engine (Interpreter + JIT)
    ↓
Garbage Collector

**Interview Tip:** Understand the compilation to bytecode and execution by JVM. Bytecode is platform-independent.

## 9. Memory Areas in Java

### Heap Memory
- Stores: Objects, Instance variables, Arrays
- Key points: Shared among all threads, Managed by Garbage Collector, Slower than stack, Large memory area

### Stack Memory
- Stores: Method calls, Local variables, References to objects
- Key points: One stack per thread, Faster than heap, Memory automatically freed (LIFO), Not managed by Garbage Collector

### Metaspace (Java 8+)
- Stores: Class metadata, Method metadata, Static variables, Runtime constant pool
- Key points: Replaced PermGen, Uses native memory, Grows dynamically, Controlled using -XX:MaxMetaspaceSize

**Interview Tip:** Heap for objects, Stack for method execution. OutOfMemoryError in heap, StackOverflowError in stack.

## 10. Garbage Collection (basic types, when it runs)

Garbage Collection is an automatic memory management process in Java that removes unused objects from heap memory when JVM needs more space.

### When Does Garbage Collection Run?
- GC runs automatically when: Heap memory is full or near full, JVM needs more memory for new objects, Based on JVM GC algorithms & thresholds.

**Interview Tip:** GC is automatic, but tuning GC can improve performance. Use tools like VisualVM to monitor GC.

## 11. OOPS (Object-Oriented Programming System)

OOPS is a programming approach based on objects that contain Data (variables) and Behavior (methods).

Real-life example: Car (object) - Data: color, speed; Behavior: drive(), brake()

### Encapsulation
- Wrapping data + methods together and hiding internal details.
- Real-life example: Capsule medicine.
- Java: private variables + getters/setters.

Example:
```java
class Car {
    private String color;
    public String getColor() { return color; }
    public void setColor(String color) { this.color = color; }
}
```

### Inheritance
- One class acquires properties and behaviors of another class.
- Real-life example: Parent → Child.
- Java: extends keyword.

Example:
```java
class Vehicle {
    void start() { System.out.println("Starting"); }
}

class Car extends Vehicle {
    void drive() { System.out.println("Driving"); }
}
```

### Polymorphism
- One method, many forms.
- Real-life example: "Call" button.
- Java: Method overloading and overriding.

Example: See overriding example above.

### Abstraction
- Hiding implementation and showing only essential details.
- Real-life example: Driving a car.
- Java: Abstract classes and interfaces.

Example:
```java
abstract class Vehicle {
    abstract void start();
}

class Car extends Vehicle {
    void start() { System.out.println("Car starting"); }
}
```

**Interview Tip:** Encapsulation hides data, Inheritance reuses code, Polymorphism allows flexibility, Abstraction simplifies complexity.

## 12. Exception Handling

### Types:
- Checked: Checked at compile-time (e.g., IOException)
- Unchecked: Runtime exceptions (e.g., NullPointerException)
- Error: Serious problems (e.g., OutOfMemoryError)

### throw vs throws
- throw: Explicitly throw an exception inside a method.
- throws: Indicate that the method may throw certain exceptions.

Example:
```java
void method() throws IOException {
    if (condition) {
        throw new IOException("Error");
    }
}
```

**Interview Tip:** Use try-catch for handling, throws for declaration. Checked exceptions must be handled or declared.

## 13. Access Modifiers

- private: Accessible only within the same class.
- protected: Accessible within the same package and subclasses.
- public: Accessible from anywhere.
- default (no modifier): Accessible within the same package.

**Interview Tip:** private for encapsulation, public for API, protected for inheritance.

## 14. What is Dependency Injection?

Dependency Injection (DI) is a design pattern where the dependencies of a class are provided from outside instead of the class creating them itself.

In Spring, the IoC container manages the lifecycle of beans and injects dependencies using constructor, setter, or field injection. It helps achieve loose coupling and makes the application easier to test and maintain.

Example:
```java
@Service
class UserService {
    private final UserRepository repo;

    @Autowired
    UserService(UserRepository repo) {
        this.repo = repo;
    }
}
```

**Interview Tip:** DI promotes loose coupling. Constructor injection is preferred over field injection.

## 15. What is Auto-Configuration in Spring Boot?

Spring Boot automatically configures beans based on the dependencies present in the classpath.

Example: Add spring-boot-starter-data-jpa → Spring Boot configures DataSource, EntityManager, etc.

### How It Works Internally?
- @SpringBootApplication = @Configuration + @EnableAutoConfiguration + @ComponentScan
- @EnableAutoConfiguration scans classpath and loads auto-config classes from META-INF/spring.factories
- Uses conditional annotations like @ConditionalOnClass, @ConditionalOnMissingBean

**Interview Tip:** Auto-configuration reduces boilerplate. Use @ConditionalOnProperty for custom configs.

## 16. Global Exception Handling

Instead of writing try-catch in every controller method, we handle exceptions centrally.

Spring provides @ControllerAdvice or @RestControllerAdvice. We define methods annotated with @ExceptionHandler to handle specific exceptions.

Example:
```java
@RestControllerAdvice
class GlobalExceptionHandler {
    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity<String> handleNotFound(ResourceNotFoundException e) {
        return ResponseEntity.status(404).body("Resource not found");
    }
}
```

**Interview Tip:** Centralizes error handling, improves maintainability.

## 17. How do you validate request body in Spring Boot?

Use Bean Validation (JSR-380) with annotations like @NotNull, @Size, @Email in the DTO class.

In the controller, use @Valid with @RequestBody to trigger validation.

If validation fails, Spring throws MethodArgumentNotValidException.

Example:
```java
class UserDTO {
    @NotNull
    @Size(min = 2, max = 50)
    private String name;

    @Email
    private String email;
}

@PostMapping("/users")
public ResponseEntity<User> createUser(@Valid @RequestBody UserDTO dto) {
    // logic
}
```

**Interview Tip:** Validation happens before controller logic. Handle validation errors in @ControllerAdvice.

## 18. JPA (Java Persistence API)

- Object-Relational Mapping (ORM): Maps Java classes to database tables.
- Provides methods for CRUD operations.
- Supports JPQL.
- JPA is a specification; Hibernate is an implementation.

Example:
```java
@Entity
class User {
    @Id @GeneratedValue
    private Long id;
    private String name;
}

@Repository
interface UserRepository extends JpaRepository<User, Long> {
    List<User> findByName(String name);
}
```

**Interview Tip:** JPA abstracts database operations. Use @Query for custom queries.

## 19. ResponseEntity

Used to customize HTTP response: status code, headers, body.

Example:
```java
return ResponseEntity.ok().body(data);
```

Additional Example:
```java
return ResponseEntity.status(HttpStatus.CREATED).header("Custom-Header", "value").body(data);
```

**Interview Tip:** Use for custom responses, not just returning objects.

## 20. .map vs .flatMap

### .map
- Transforms each element into another object.
- One-to-one mapping.

Example:
```java
List<String> names = users.stream().map(User::getName).collect(Collectors.toList());
```

### .flatMap
- Transforms each element into a stream and flattens into a single stream.
- One-to-many mapping.

Example:
```java
List<String> allOrders = users.stream()
    .flatMap(user -> user.getOrders().stream())
    .map(Order::getId)
    .collect(Collectors.toList());
```

**Interview Tip:** map for transformation, flatMap for flattening nested collections.

## 21. Types of Exceptions (from GlobalExceptionHandler)

- 403 Forbidden: AccessDeniedException
- 404 Not Found: UsernameNotFoundException, ResourceNotFoundException
- 400 Bad Request: ExecutionException, InterruptedException, MethodArgumentNotValidException, etc.
- 405 Method Not Allowed: HttpRequestMethodNotSupportedException
- 500 Internal Server Error: Exception (generic)

**Interview Tip:** Map exceptions to appropriate HTTP status codes for REST APIs.

## 22. Multithreading

Multithreading allows a program to run multiple threads concurrently within the same process to improve performance and responsiveness.

### Thread Lifecycle
NEW → RUNNABLE → WAITING/BLOCKED → TERMINATED

### Process vs Thread
| Feature    | Process              | Thread                |
|------------|----------------------|-----------------------|
| Definition | Independent program  | Part of a process     |
| Memory     | Own memory           | Shares memory         |
| Communication | Slow               | Fast                  |
| Creation cost | High              | Low                   |

Example:
```java
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread running");
    }
}

MyThread t = new MyThread();
t.start();
```

**Interview Tip:** Threads share heap, have separate stacks. Use synchronized for thread safety.

## 23. Collections Framework

Provides data structures to store, retrieve, and manipulate groups of objects dynamically.

### Main Interfaces
1. List: Ordered, allows duplicates (ArrayList, LinkedList)
2. Set: No duplicates (HashSet, TreeSet)
3. Map: Key-value pairs (HashMap, TreeMap)

Example:
```java
List<String> list = new ArrayList<>();
list.add("Apple");
list.add("Apple"); // duplicates allowed

Set<String> set = new HashSet<>();
set.add("Apple");
set.add("Apple"); // no duplicates

Map<String, Integer> map = new HashMap<>();
map.put("Apple", 1);
```

**Interview Tip:** ArrayList for random access, LinkedList for insertions/deletions. HashMap for fast lookups.

## 24. Streams

A sequence of elements from a data source that supports operations to process those elements.

- Does not store data, processes data from source.
- Operations: map, filter, reduce, etc.

Example:
```java
List<String> names = users.stream()
    .filter(u -> u.getAge() > 18)
    .map(User::getName)
    .collect(Collectors.toList());
```

**Interview Tip:** Streams are lazy, use collect() to materialize. Parallel streams for performance.

## 25. SOLID Principles

### S - Single Responsibility Principle
A class should have only ONE reason to change.

Example: Separate UserService for business logic, EmailService for notifications.

### O - Open/Closed Principle
Software entities should be open for extension but closed for modification.

Example: Use interfaces to add new payment methods without changing existing code.

### L - Liskov Substitution Principle
Objects of a superclass should be replaceable with objects of a subclass without affecting correctness.

Example: Rectangle and Square - ensure Square doesn't break Rectangle behavior.

### I - Interface Segregation Principle
Clients should not be forced to depend on interfaces they do not use.

Example: Separate Printable and Scannable interfaces instead of one big Printer interface.

### D - Dependency Inversion Principle
High-level modules should not depend on low-level modules. Both should depend on abstractions.

Example: Service depends on Repository interface, not concrete implementation.

**Interview Tip:** SOLID ensures maintainable code. S for focus, O for extensibility, L for inheritance safety, I for interface design, D for decoupling.

## 26. Spring Boot Topics

### Core Concepts
- @SpringBootApplication
- Auto-configuration
- Application properties/YAML
- Profiles
- Actuator

### REST APIs
- @RestController, @RequestMapping
- @RequestParam, @PathVariable, @RequestBody
- ResponseEntity

### Data Persistence
- Spring Data JPA
- Entities, Repositories
- @Transactional

### Security
- Spring Security
- Authentication/Authorization
- JWT/OAuth2

### Testing
- @SpringBootTest, @WebMvcTest
- JUnit, Mockito

### Advanced
- Caching, Messaging, Scheduling, Async

**Interview Tip:** Master auto-configuration and profiles for environment-specific configs.

## 27. Spring Boot Annotations

### Stereotype
- @Component, @Service, @Repository, @Controller, @RestController

### Configuration
- @Configuration, @Bean, @ComponentScan

### Web
- @RequestMapping, @GetMapping, @PostMapping, @RequestParam, @PathVariable, @RequestBody, @ResponseBody

### DI
- @Autowired, @Qualifier, @Value

### Data
- @Entity, @Table, @Transactional

### Validation
- @Valid, @NotNull, @Size

### Testing
- @SpringBootTest, @MockBean

**Interview Tip:** @RestController = @Controller + @ResponseBody.

## 28. RequestParam, PathVariable, RequestBody, ResponseBody

| Annotation     | Used For              | Example URL          | Example Usage |
|----------------|-----------------------|----------------------|---------------|
| @RequestParam | Query parameters     | /greet?name=Srini   | @GetMapping("/greet") public String greet(@RequestParam String name) |
| @PathVariable | URL path variables    | /users/101          | @GetMapping("/users/{id}") public String getUser(@PathVariable int id) |
| @RequestBody  | JSON body to object   | /createUser (POST)  | @PostMapping("/createUser") public String createUser(@RequestBody User user) |
| @ResponseBody | Return value as response | /welcome           | @GetMapping("/welcome") @ResponseBody public String welcome() |

**Interview Tip:** @RequestParam for optional params, @PathVariable for required path parts.

## 29. HashMap vs ConcurrentHashMap

HashMap is not thread-safe and allows one null key and multiple null values, whereas ConcurrentHashMap is thread-safe, does not allow null keys or values, and provides better performance in concurrent environments by locking at bucket level instead of locking the whole map.

Example:
```java
Map<String, String> map = new ConcurrentHashMap<>();
map.put("key", "value"); // thread-safe
```

**Interview Tip:** Use ConcurrentHashMap for multi-threaded access, HashMap for single-threaded.

## 30. @Autowired vs Constructor Injection

@Autowired is an annotation used to inject dependencies. It can be used in field, setter, or constructor injection. Constructor injection is recommended because it makes dependencies mandatory, supports immutability, improves testability, and follows good design principles.

Example:
```java
@Service
class Service {
    private final Repo repo;

    Service(Repo repo) { // no @Autowired needed in Spring 4.3+
        this.repo = repo;
    }
}
```

**Interview Tip:** Constructor injection prevents null dependencies and is testable.