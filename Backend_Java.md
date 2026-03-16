# Backend - Java Basics

> **Note:** Interview Tips are highlighted in <span style="color: #007acc;">blue</span> for easy identification.
> **Accordion Feature:** Each question can be made collapsible by wrapping in `<details><summary>Question Title</summary> content </details>` (demonstrated for first few questions).

<details><summary>📚 Java Interview Preparation Guide</summary>

## Basic Java Interview Questions

<details><summary style="font-size: 1.3em; font-weight: bold;">1. What is Java?</summary>

Java is a high-level, object-oriented programming language developed by Sun Microsystems (now Oracle). It is platform-independent due to the JVM (Java Virtual Machine), which allows "Write Once, Run Anywhere" (WORA).

**Key Features:**
- Object-Oriented
- Platform-Independent
- Secure
- Robust
- Multithreaded
- Interpreted and Compiled

### Interview Explanation:
"When I explain Java in interviews, I emphasize its platform independence through bytecode and JVM. Java code compiles to bytecode that runs on any platform with a JVM, unlike C++ which compiles to platform-specific machine code. This 'write once, run anywhere' capability made Java revolutionary for enterprise applications and web development. I also highlight its robustness with automatic memory management via garbage collection, which prevents memory leaks common in languages like C. The strong type system and exception handling make Java reliable for large-scale applications."

**Interview Tip:** Emphasize platform-independence via bytecode and JVM.
</details>

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">2. What are the data types in Java?</summary>

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

### Interview Explanation:
"Java has 8 primitive types for performance and memory efficiency, plus reference types for objects. Primitives are stored on the stack and have default values (0 for numeric, false for boolean, \u0000 for char), while references point to objects on the heap. I choose primitives for simple values to avoid object overhead, but use wrapper classes (Integer, Double) when I need null values or collections. For example, in a banking app, I'd use double for amounts but BigDecimal for precise financial calculations to avoid floating-point precision issues."

**Interview Tip:** Know the size and range of primitives. Strings are immutable objects.
</details>

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">3. What are the access modifiers in Java?</summary>

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

### Interview Explanation:
"Access modifiers in Java control encapsulation and API design. I use private for implementation details that shouldn't be exposed, protected for inheritance hierarchies, default for package-private functionality, and public for the API. For example, in a service class, I'd make the constructor package-private (default) to allow testing within the package but prevent external instantiation, while keeping business methods public. This follows the principle of least privilege and makes refactoring safer."

**Interview Tip:** private for encapsulation, public for APIs.
</details>

</details>

<details>
<summary style="font-size: 1.3em; font-weight: bold;">4. What is the difference between == and equals()?</summary>

- **==** compares reference equality (memory addresses) for objects, value equality for primitives.
- **equals()** compares content/value equality for objects.

Example:
```java
String s1 = new String("Hello");
String s2 = new String("Hello");
System.out.println(s1 == s2); // false (different objects)
System.out.println(s1.equals(s2)); // true (same content)
```

### Interview Explanation:
"The == operator checks if two references point to the same object in memory, while equals() checks if two objects have the same logical value. For primitives, == compares values directly. For objects, == is rarely what you want - it would only return true for the same instance. I always override equals() and hashCode() together in my domain objects, following the contract that equal objects must have equal hash codes. In collections like HashSet or HashMap keys, this is crucial for correct behavior."

**Interview Tip:** Override equals() and hashCode() together in custom classes.
</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">5. What is the static keyword?</summary>

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

### Interview Explanation:
"Static members belong to the class itself, not to instances. Static variables are shared across all instances and can be used for constants or global state. Static methods are useful for utility functions that don't need instance state, like Math.max(). I use static blocks for one-time initialization, such as loading configuration or registering drivers. However, I avoid static state for business logic as it makes testing harder and creates tight coupling. In Spring applications, I prefer dependency injection over static utility classes."

**Interview Tip:** Static methods cannot access instance variables. Used for utility methods.
</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">6. What is the final keyword?</summary>

Final makes variables, methods, or classes unchangeable.

- Final variable: Cannot be reassigned.
- Final method: Cannot be overridden.
- Final class: Cannot be subclassed.

Example:
```java
final int MAX = 100;
final class MathUtils { }
```

### Interview Explanation:
"Final provides immutability guarantees in Java. Final variables create constants (use UPPER_CASE naming), final methods prevent overriding in inheritance hierarchies, and final classes like String prevent extension. I use final extensively for thread safety - final fields can be safely accessed from multiple threads without synchronization. In method parameters, final prevents accidental reassignment. However, final doesn't make objects immutable if they have mutable state - for that I use immutable classes or libraries like Immutables."

**Interview Tip:** Final for constants, security, and performance.
</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">7. What is the difference between String, StringBuffer, and StringBuilder?</summary>

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

### Interview Explanation:
"String is immutable - every modification creates a new object, which is expensive for concatenation in loops. StringBuffer is thread-safe with synchronization, making it safe for multi-threaded environments but slower. StringBuilder is the fastest option for single-threaded string building, with the same API as StringBuffer but without synchronization overhead. In modern Java, the compiler optimizes string concatenation with +, but for loops I always use StringBuilder. For logging or single concatenations, String is fine, but for building complex strings, I choose based on thread safety requirements."

**Interview Tip:** Use StringBuilder for single-threaded string manipulations, StringBuffer for multi-threaded.
</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">7.5. Why is String Immutable in Java?</summary>

In Java, String is actually immutable, not mutable. This is a very common interview question, so it's important to understand clearly.

### What Does Immutable Mean?

Immutable means the value of the object cannot be changed after it is created.

For example:

```java
String str = "Hello";
str = str + " World";
```

Here it looks like the string changed, but actually:

- "Hello" object is created.
- "Hello World" is created as a new object.
- str now references the new object.
- The original "Hello" string still exists in memory.

### Example Showing Immutability

```java
String s1 = "Java";
String s2 = s1;

s1 = s1 + " Programming";

System.out.println(s1); // Java Programming
System.out.println(s2); // Java
```

s2 still points to "Java" because the original string was not modified.

### Why String Is Immutable in Java

1️⃣ **Security**

Strings are used in:
- file paths
- network connections
- database URLs

Immutability prevents malicious modification.

2️⃣ **String Pool Optimization**

Java uses a String Constant Pool to save memory.

Example:

```java
String a = "Java";
String b = "Java";
```

Both a and b reference the same object in the pool.

This works safely because strings cannot change.

3️⃣ **Thread Safety**

Since strings cannot change, they are automatically thread-safe in multi-threaded environments.

4️⃣ **Hashcode Caching**

Strings are used as keys in HashMap.

Example:

```java
Map<String, Integer> map = new HashMap<>();
```

If strings were mutable, the hashcode could change, breaking the map.

### Mutable Alternatives

If you need a modifiable string, Java provides:

- StringBuilder
- StringBuffer

Example:

```java
StringBuilder sb = new StringBuilder("Hello");
sb.append(" World");

System.out.println(sb); // Hello World
```

### Interview One-Line Answer

In Java, String is immutable, meaning its value cannot be changed after creation. This improves security, enables string pooling, ensures thread safety, and allows efficient hashing.

**Interview Tip:** String immutability is crucial for security, performance, and thread safety. Always mention the String pool and HashMap usage.
</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">8. What are arrays in Java?</summary>

Arrays are fixed-size, homogeneous data structures.

Declaration: `int[] arr = new int[5];`
Initialization: `int[] arr = {1, 2, 3, 4, 5};`

### Interview Explanation:
"Arrays in Java are fixed-size containers for elements of the same type, stored contiguously in memory for fast access. They have O(1) access time but fixed size makes them inflexible. I use arrays when I know the size in advance and need performance, but prefer ArrayList for dynamic collections. Multi-dimensional arrays are arrays of arrays, useful for matrices. The JVM performs bounds checking to prevent buffer overflows, though it costs a small performance penalty. For primitives, arrays store values directly; for objects, they store references."

**Interview Tip:** Arrays have fixed size; use ArrayList for dynamic size.
</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">9. What is inheritance in Java?</summary>

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

### Interview Explanation:
"Inheritance creates an 'is-a' relationship where subclasses inherit behavior from superclasses. It promotes code reuse but can create tight coupling. I use inheritance for specialization, like different types of vehicles inheriting from a base Vehicle class. However, I prefer composition over inheritance when possible, as it provides more flexibility. In Java, all classes implicitly extend Object, giving access to methods like toString(), equals(), and hashCode(). Multiple inheritance isn't allowed for classes to avoid the diamond problem, but interfaces provide a way to achieve similar behavior."

**Interview Tip:** Java supports single inheritance. Use interfaces for multiple inheritance.
</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">10. What are interfaces in Java?</summary>

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

### Interview Explanation:
"Interfaces define contracts that implementing classes must fulfill, enabling polymorphism and loose coupling. Before Java 8, interfaces only had abstract methods, but now they can have default methods (providing implementation) and static methods. I use interfaces for dependency injection and testing - I can easily mock interface implementations. In Spring, interfaces like Repository, Service, and Controller are markers that enable framework features. Multiple interface implementation allows mixin-like behavior, and functional interfaces (single abstract method) work with lambdas for functional programming."

**Interview Tip:** All methods are public abstract by default. From Java 8, can have default and static methods.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">11. What are abstract classes?</summary>

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

### Interview Explanation:
"Abstract classes provide partial implementation and force subclasses to implement certain methods. I use them when I want to share common code among related classes but prevent direct instantiation. Unlike interfaces, abstract classes can have state and concrete methods. In frameworks, abstract classes often provide template methods that subclasses customize. For example, in Spring Data JPA, repository interfaces extend from interfaces but the framework provides abstract base classes for common functionality. I choose abstract classes over interfaces when I need to share implementation details among closely related classes."

**Interview Tip:** Use abstract classes when sharing code, interfaces when defining contracts.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">12. What is method overloading and overriding?</summary>

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

### Interview Explanation:
"Overloading provides compile-time polymorphism with multiple methods of the same name but different signatures, resolved by the compiler based on arguments. Overriding provides runtime polymorphism where subclasses can change parent behavior. I use overloading for convenience (like String.valueOf() with different types) and overriding for specialization. The @Override annotation helps catch errors and documents intent. In inheritance hierarchies, overriding allows the Liskov Substitution Principle - any subclass can be used where the parent is expected."

**Interview Tip:** Overloading changes behavior, overriding replaces behavior.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">13. What is a constructor?</summary>

Constructors initialize objects. Same name as class, no return type.

Types: Default, Parameterized, Copy.

Example:
```java
class Person {
    String name;
    Person(String name) { this.name = name; }
}
```

### Interview Explanation:
"Constructors initialize object state when created with new. Java provides a default no-arg constructor if none is defined, but I always define parameterized constructors for required fields. Constructor chaining with this() calls other constructors in the same class, while super() calls parent constructors. In immutable classes, all fields are final and set in the constructor. For complex initialization, I use builder patterns or factory methods. In Spring, the framework uses reflection to call constructors for dependency injection."

**Interview Tip:** If no constructor, Java provides default. Cannot be inherited.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">14. What is the this keyword?</summary>

`this` refers to the current object instance.

Uses: Differentiate instance variables, call other constructors, pass current object.

Example:
```java
class Person {
    String name;
    Person(String name) { this.name = name; }
}
```

### Interview Explanation:
"The this keyword refers to the current instance, helping distinguish between instance variables and parameters with the same name. I use this.field = parameter in constructors and setters. this() calls other constructors in the same class for constructor chaining. In method chaining (fluent interfaces), I return this to allow method calls like obj.method1().method2(). In inner classes, this refers to the inner class instance, and OuterClass.this refers to the outer class. It's essential for object-oriented programming and prevents shadowing issues."

**Interview Tip:** Used to avoid name conflicts.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">15. What is the super keyword?</summary>

`super` refers to the parent class.

Uses: Call parent constructor, access parent methods/variables.

Example:
```java
class Dog extends Animal {
    Dog() { super(); } // calls parent constructor
}
```

### Interview Explanation:
"Super accesses parent class members, essential for inheritance. super() must be the first statement in a constructor to call parent constructors. I use super.method() to call overridden parent methods, and super.field to access hidden parent fields. In method overriding, super allows calling the parent's version before or after adding subclass behavior. Without explicit super() calls, Java automatically calls the parent's no-arg constructor. Understanding super is crucial for proper inheritance hierarchies and avoiding initialization issues."

**Interview Tip:** Must be first statement in constructor.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">16. What are packages in Java?</summary>

Packages organize classes and avoid name conflicts.

Example: `import java.util.*;`

### Interview Explanation:
"Packages provide namespace management and access control in Java. They follow reverse domain naming (com.company.project) to ensure uniqueness. Classes in the same package have package-private access to each other, which I use for internal implementation classes. Import statements bring classes into scope, with * for all classes in a package. The classpath tells JVM where to find packages. In enterprise applications, packages organize code by functionality (controller, service, repository) and help with modular development and testing."

**Interview Tip:** Use reverse domain naming convention.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">17. What is the difference between ArrayList and LinkedList?</summary>

- **ArrayList:** Dynamic array, fast random access, slow insertions/deletions.
- **LinkedList:** Doubly linked list, fast insertions/deletions, slow random access.

### Interview Explanation:
"ArrayList is backed by a dynamic array, offering O(1) random access but O(n) insertions/deletions in the middle due to shifting. LinkedList uses nodes with pointers, providing O(1) insertions/deletions at ends but O(n) random access. I choose ArrayList for read-heavy operations like iterating or getting by index, and LinkedList for write-heavy scenarios like frequent additions/removals. Both implement List interface, so they're interchangeable in most code. For stacks/queues, I prefer ArrayDeque over LinkedList for better performance."

**Interview Tip:** Choose based on use case: ArrayList for reads, LinkedList for modifications.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">18. What is the difference between HashSet and TreeSet?</summary>

- **HashSet:** Unordered, uses hash, faster.
- **TreeSet:** Ordered, uses red-black tree, slower.

### Interview Explanation:
"HashSet provides O(1) average time complexity for add/remove/contains operations using hashing, but doesn't maintain order. TreeSet keeps elements sorted using a red-black tree, offering O(log n) operations but with ordering guarantees. I use HashSet for fast lookups when order doesn't matter, and TreeSet when I need sorted unique elements. Both implement Set interface and prevent duplicates. For concurrent access, I use ConcurrentSkipListSet (TreeSet equivalent) or ConcurrentHashMap-based sets."

**Interview Tip:** HashSet for uniqueness, TreeSet for sorted order.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">19. What is the difference between HashMap and HashTable?</summary>

- **HashMap:** Not synchronized, allows null keys/values, faster.
- **HashTable:** Synchronized, doesn't allow null, thread-safe but slower.

### Interview Explanation:
"HashTable is the legacy synchronized version from Java 1.0, while HashMap is the modern non-synchronized implementation. HashTable doesn't allow null keys or values (throws NullPointerException), while HashMap allows one null key and multiple null values. For thread safety, I use ConcurrentHashMap instead of HashTable, as it provides better concurrency with segment-level locking. HashMap is faster for single-threaded use, which is most common. In Spring applications, I use HashMap for configuration maps and ConcurrentHashMap for shared caches."

**Interview Tip:** Use HashMap for single-threaded, ConcurrentHashMap for multi-threaded.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">20. What is the try-with-resources statement?</summary>

Automatically closes resources that implement AutoCloseable.

Example:
```java
try (FileReader fr = new FileReader("file.txt")) {
    // use fr
} // automatically closed
```

### Interview Explanation:
"Try-with-resources automatically closes resources at the end of the try block, preventing resource leaks. Resources must implement AutoCloseable (or Closeable). The close() methods are called in reverse order of declaration. This is much safer than manual try-finally blocks, which are error-prone. I use it for files, database connections, sockets, and any resource that needs cleanup. In Spring Boot, connection pooling handles this automatically, but for direct JDBC or file operations, try-with-resources is essential."

**Interview Tip:** Prevents resource leaks.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">1. What is the difference between RestTemplate and WebClient?</summary>

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

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">2. How do you handle microservice communication failures?</summary>

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

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">3. What are the types of Garbage Collectors (GC) in Java?</summary>

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

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">4. Explain the end-to-end deployment flow.</summary>

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

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">5. Method Overloading vs Method Overriding</summary>

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

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">6. volatile vs transient Keyword</summary>

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

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">7. JDK vs JRE vs JVM</summary>

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

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">8. How Java works internally</summary>

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

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">9. Memory Areas in Java</summary>

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

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">10. Garbage Collection (basic types, when it runs)</summary>

Garbage Collection is an automatic memory management process in Java that removes unused objects from heap memory when JVM needs more space.

### When Does Garbage Collection Run?
- GC runs automatically when: Heap memory is full or near full, JVM needs more memory for new objects, Based on JVM GC algorithms & thresholds.

**Interview Tip:** GC is automatic, but tuning GC can improve performance. Use tools like VisualVM to monitor GC.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">11. OOPS (Object-Oriented Programming System)</summary>

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

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">12. Exception Handling</summary>

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

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">13. Access Modifiers</summary>

- private: Accessible only within the same class.
- protected: Accessible within the same package and subclasses.
- public: Accessible from anywhere.
- default (no modifier): Accessible within the same package.

**Interview Tip:** private for encapsulation, public for API, protected for inheritance.

</details>

## Interview Questions

<details><summary style="font-size: 1.3em; font-weight: bold;">Q: What is the difference between JDK, JRE, and JVM?</summary>

**Explanation:** JDK (Java Development Kit) is for development with compilers and tools, JRE (Java Runtime Environment) provides the runtime environment, and JVM (Java Virtual Machine) executes bytecode.

**Example:** JDK includes JRE, which includes JVM. You need JDK to develop, JRE to run applications.

**Real-time Example:** In a production server, you deploy with JRE since you only need to run, not compile code.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">Q: Explain the main principles of OOP in Java.</summary>

**Explanation:** OOP principles are Encapsulation (data hiding), Inheritance (code reuse), Polymorphism (many forms), and Abstraction (hiding complexity).

**Example:** A Car class encapsulates data, inherits from Vehicle, overrides methods polymorphically, and uses abstract methods for abstraction.

**Real-time Example:** In a banking app, Account class encapsulates balance, different account types inherit from it, and methods like calculateInterest show polymorphism.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">Q: What is the difference between ArrayList and LinkedList?</summary>

**Explanation:** ArrayList uses dynamic arrays for fast random access but slow insertions, LinkedList uses nodes for fast insertions but slow random access.

**Example:** Use ArrayList for reading data frequently, LinkedList for frequent additions/removals.

**Real-time Example:** In a task manager app, use ArrayList for displaying tasks (mostly reading), LinkedList for managing a queue of tasks to process.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">Q: How does exception handling work in Java?</summary>

**Explanation:** Exceptions are handled using try-catch-finally blocks. Checked exceptions must be caught or declared, unchecked are runtime exceptions.

**Example:** try { risky code } catch (Exception e) { handle } finally { cleanup }

**Real-time Example:** In file operations, catch IOException for missing files, use finally to ensure file streams are closed.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">Q: What are the different types of memory areas in Java?</summary>

**Explanation:** Heap stores objects, Stack stores method calls and local variables, Metaspace stores class metadata.

**Example:** Objects go to heap, method variables to stack, class information to metaspace.

**Real-time Example:** In a web application, user sessions are stored in heap, method parameters in stack, and loaded classes in metaspace.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">Q: Explain method overloading vs method overriding.</summary>

**Explanation:** Overloading is same method name different parameters in same class (compile-time), overriding is same signature in subclass (runtime).

**Example:** print(int) and print(String) is overloading, Dog overriding Animal.sound() is overriding.

**Real-time Example:** Calculator class overloads add() for int and double, while Dog overrides Animal's makeSound() method.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">Q: What is the purpose of the static keyword?</summary>

**Explanation:** Static members belong to the class, not instances. Used for constants, utility methods, and shared state.

**Example:** Math.PI is static constant, Collections.sort() is static utility method.

**Real-time Example:** In a configuration class, static constants hold database URLs shared across all instances.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">Q: How does garbage collection work in Java?</summary>

**Explanation:** GC automatically frees memory by removing unreachable objects. Different algorithms like G1, ZGC optimize for different needs.

**Example:** When heap is full, GC marks unreachable objects and reclaims memory.

**Real-time Example:** In a long-running server application, GC prevents memory leaks by cleaning up unused HTTP request objects.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">Q: What are the differences between String, StringBuffer, and StringBuilder?</summary>

**Explanation:** String is immutable, StringBuffer is thread-safe mutable, StringBuilder is non-thread-safe mutable.

**Example:** Use StringBuilder for building strings in loops, StringBuffer for multi-threaded string building.

**Real-time Example:** In logging frameworks, StringBuilder is used for efficient log message construction in single-threaded contexts.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">Q: Explain the concept of inheritance in Java.</summary>

**Explanation:** Inheritance allows a class to inherit properties and methods from another class using extends keyword.

**Example:** Dog extends Animal to inherit eat() method and add bark().

**Real-time Example:** In an e-commerce system, CreditCardPayment extends Payment to inherit common payment logic while adding card-specific methods.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">Q: What are the different types of garbage collectors in Java?</summary>

**Explanation:** Java has several GC algorithms: Serial (single-threaded), Parallel (multi-threaded throughput), CMS (concurrent low-pause), G1 (region-based), ZGC (ultra-low pause).

**Example:** Use G1 for most applications as it's the default, ZGC for sub-10ms pause requirements.

**Real-time Example:** In a high-throughput trading system, Parallel GC maximizes throughput, while in a user-facing app, ZGC minimizes pauses.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">Q: Explain the difference between abstract classes and interfaces.</summary>

**Explanation:** Abstract classes can have concrete methods and state, interfaces define contracts with default methods. Classes extend one abstract class but implement multiple interfaces.

**Example:** Abstract Vehicle class with drive() implementation, Vehicle interface with start() contract.

**Real-time Example:** In a game, Character is abstract with common behavior, Movable and Attackable are interfaces for different capabilities.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">Q: What is the Java Memory Model and why is it important?</summary>

**Explanation:** JMM defines how threads interact through memory, ensuring visibility and ordering of operations across threads.

**Example:** Volatile variables ensure writes are visible to all threads, synchronized blocks create memory barriers.

**Real-time Example:** In a multi-threaded cache, volatile ensures all threads see the latest cached value.

</details>

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">Q: How does Java handle memory management?</summary>

**Explanation:** Java uses automatic garbage collection to manage heap memory, while stack memory is managed automatically with method calls.

**Example:** Objects are created on heap, method variables on stack. GC reclaims unreachable objects.

**Real-time Example:** In a web server, GC prevents memory leaks from HTTP request objects that are no longer referenced.

</details>

## Advanced Java Concepts - Multi-threading

<details><summary style="font-size: 1.3em; font-weight: bold;">🚀 Multi-threading Made Simple</summary>

Multi-threading is a core Java concept that allows concurrent execution of multiple threads within a single process. Understanding threads is crucial for building scalable, responsive applications.

### 🍳 Real-world Analogy
Imagine a **restaurant kitchen** as your program (process). Each **chef** is a **thread** — they share the same kitchen space (memory) but work on different dishes simultaneously. One chef grills, another chops, another plates. That's multi-threading!

### Key Concepts:
- **Process**: A running program with its own memory space (heavyweight)
- **Thread**: Smallest unit of execution inside a process (lightweight)
- **Concurrency**: Multiple tasks appear to run simultaneously (single CPU core)
- **Parallelism**: Multiple tasks actually run simultaneously (multiple CPU cores)

**Interview Tip:** Threads share memory but processes have separate memory spaces. Threads are faster to create and communicate with.
</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">1. Thread Lifecycle</summary>

A thread goes through several states during its lifetime:

### Thread States:
1. **NEW**: Thread created but not started
2. **RUNNABLE**: Thread is ready to run (start() called)
3. **RUNNING**: Thread is actively executing
4. **WAITING/BLOCKED**: Thread waiting for resource or I/O
5. **TERMINATED**: Thread completed execution

### State Transitions:
```
NEW → RUNNABLE (start())
RUNNABLE → RUNNING (CPU allocated)
RUNNING → WAITING (wait()/sleep())
RUNNING → BLOCKED (waiting for lock)
WAITING/BLOCKED → RUNNABLE (condition met)
RUNNABLE → TERMINATED (run() completes)
```

**Interview Tip:** A thread can move between RUNNABLE ↔ WAITING ↔ BLOCKED multiple times before terminating. Use `Thread.getState()` to check current state.
</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">2. Creating Threads in Java</summary>

There are 3 ways to create threads in Java:

### Way 1: Extend Thread Class
```java
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread running: " + getName());
    }
}

// Usage
Thread t1 = new MyThread();
t1.start(); // Don't call run() directly!
```

### Way 2: Implement Runnable Interface
```java
class MyRunnable implements Runnable {
    public void run() {
        System.out.println("Runnable running!");
    }
}

// Usage
Thread t2 = new Thread(new MyRunnable());
t2.start();
```

### Way 3: Lambda Expression (Java 8+) - Recommended ✅
```java
Thread t3 = new Thread(() -> {
    System.out.println("Lambda thread running! 🚀");
});
t3.start();
```

### Production-Ready: ExecutorService
```java
ExecutorService pool = Executors.newFixedThreadPool(4);
pool.submit(() -> System.out.println("Pool thread running!"));
pool.shutdown();
```

**Interview Tip:** Prefer Runnable over extending Thread (composition over inheritance). Use ExecutorService for production as it manages thread lifecycle automatically.
</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">3. Thread vs Process</summary>

| Aspect | Thread | Process |
|--------|--------|---------|
| Memory | Shares with other threads | Separate memory space |
| Creation | Lightweight, fast | Heavyweight, slow |
| Communication | Easy (shared memory) | Needs IPC (pipes, sockets) |
| Crash Impact | Affects other threads | Isolated |
| Examples | HTTP request handlers | Chrome browser tabs |

**Interview Tip:** Threads are lightweight and share memory, making them ideal for concurrent tasks within the same application. Processes provide isolation but are expensive to create.
</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">4. Synchronization & Thread Safety</summary>

### Race Condition
When two threads modify shared data simultaneously, the final result depends on timing.

**Example:**
```java
class Counter {
    private int count = 0;

    public void increment() {
        count++; // Not thread-safe!
    }
}
```

### Synchronization Solution
```java
class Counter {
    private int count = 0;

    public synchronized void increment() {
        count++; // Now thread-safe
    }
}
```

### Key Concepts:
- **Mutex/Lock**: Only one thread can hold the lock at a time
- **Deadlock**: Thread A waits for B's lock, B waits for A's lock
- **Volatile**: Ensures variable visibility across threads
- **Thread Pool**: Pre-created threads for better performance

**Interview Tip:** Use `synchronized` for mutual exclusion, `volatile` for visibility. Avoid nested locks to prevent deadlocks. Prefer concurrent collections over synchronized collections.
</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">5. Common Multi-threading Interview Questions</summary>

**Q: What is the difference between sleep() and wait()?**
- `sleep()` pauses execution for specified time
- `wait()` releases lock and waits for notify()

**Q: What is a daemon thread?**
- Background threads that don't prevent JVM shutdown
- Example: Garbage collector

**Q: How to stop a thread?**
- Don't use `stop()` (deprecated)
- Use boolean flag or interrupt()

**Q: What is ThreadLocal?**
- Variables local to each thread
- Each thread gets its own copy

**Interview Tip:** Know the difference between `synchronized` methods vs blocks. Understand when to use `ReentrantLock` over `synchronized`. Be familiar with concurrent collections like `ConcurrentHashMap`.
</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">🚀 Advanced Java Concepts - CompletableFuture</summary>

CompletableFuture is a class in Java (introduced in Java 8) used for asynchronous programming. It allows you to run tasks in the background and handle their results without blocking the main thread.

It is part of the java.util.concurrent package.

### 1️⃣ What is CompletableFuture?

CompletableFuture is used to:

- Run tasks asynchronously
- Combine multiple asynchronous operations
- Handle results when tasks complete
- Avoid blocking threads

It is an improved version of Future.

### 2️⃣ Why CompletableFuture is Needed

The older Future interface had limitations:

| Future Problems | CompletableFuture Solution |
|-----------------|---------------------------|
| Cannot manually complete result | Can complete manually |
| No chaining of tasks | Supports chaining |
| Blocking get() | Non-blocking callbacks |
| No combining multiple futures | Supports combining |

### 3️⃣ Simple Example
```java
import java.util.concurrent.CompletableFuture;

public class Example {
    public static void main(String[] args) {
        CompletableFuture<String> future =
                CompletableFuture.supplyAsync(() -> "Hello World");

        System.out.println(future.join());
    }
}
```

**Output:**
```
Hello World
```

`supplyAsync()` runs the task in another thread.

### 4️⃣ Creating CompletableFuture
#### 1. runAsync (no return value)
```java
CompletableFuture.runAsync(() -> {
    System.out.println("Running async task");
});
```

#### 2. supplyAsync (returns value)
```java
CompletableFuture<String> future =
        CompletableFuture.supplyAsync(() -> "Java");
```

### 5️⃣ Chaining Tasks

You can perform multiple asynchronous operations.

```java
CompletableFuture.supplyAsync(() -> "Hello")
        .thenApply(result -> result + " Java")
        .thenAccept(System.out::println);
```

**Output:**
```
Hello Java
```

### 6️⃣ Combining Multiple Futures

**Example:**
```java
CompletableFuture<Integer> future1 =
        CompletableFuture.supplyAsync(() -> 10);

CompletableFuture<Integer> future2 =
        CompletableFuture.supplyAsync(() -> 20);

CompletableFuture<Integer> result =
        future1.thenCombine(future2, (a, b) -> a + b);

System.out.println(result.join());
```

**Output:**
```
30
```

### 7️⃣ Handling Exceptions
```java
CompletableFuture.supplyAsync(() -> 10 / 0)
        .exceptionally(ex -> {
            System.out.println("Error occurred");
            return 0;
        });
```

### 8️⃣ Important Methods
| Method | Purpose |
|--------|---------|
| runAsync() | Run task without return |
| supplyAsync() | Run task with return |
| thenApply() | Transform result |
| thenAccept() | Consume result |
| thenCombine() | Combine two futures |
| exceptionally() | Handle errors |
| join() | Get result |

### 9️⃣ Real Example (API Calls)

In backend systems (like Spring Boot services), CompletableFuture can fetch multiple APIs simultaneously.

**Example:**
- Fetch user details
- Fetch orders
- Fetch payments

All in parallel, making the API much faster.

### 🔟 Interview One-Line Answer

CompletableFuture is a Java class used for asynchronous programming that allows tasks to run in parallel, supports chaining, combining futures, and handling results without blocking threads.

**Interview Tip:** If you want, I can also explain a very common Java interview question: Difference between Future vs CompletableFuture vs ExecutorService (asked in many backend interviews).
</details>

</details>
