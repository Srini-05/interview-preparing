# Backend - Spring Boot

> **Note:** Interview Tips are highlighted in <span style="color: #007acc;">blue</span> for easy identification.
> **Accordion Feature:** Each question can be made collapsible by wrapping in `<details><summary>Question Title</summary> content </details>`.

## Spring Boot Interview Questions

<details><summary>1. What is Dependency Injection?</summary>

Dependency Injection (DI) is a design pattern where the dependencies of a class are provided from outside instead of the class creating them itself. This promotes loose coupling and makes code more testable and maintainable.

### Why DI is Important?
- **Loose Coupling**: Classes don't create their dependencies, making them independent
- **Testability**: Easy to inject mock objects for unit testing
- **Maintainability**: Changes to dependencies don't affect the dependent class
- **Reusability**: Same dependency can be reused across different classes

### Types of Dependency Injection:
1. **Constructor Injection** (Recommended)
2. **Setter Injection**
3. **Field Injection**

### In Spring Framework:
The IoC (Inversion of Control) container manages the lifecycle of beans and injects dependencies. Spring uses ApplicationContext as the IoC container.

Example:
```java
@Service
class UserService {
    private final UserRepository repo;

    // Constructor Injection - Preferred approach
    @Autowired  // Optional in Spring 4.3+
    UserService(UserRepository repo) {
        this.repo = repo;
    }
}

// Setter Injection
@Service
class OrderService {
    private OrderRepository repo;

    @Autowired
    public void setOrderRepository(OrderRepository repo) {
        this.repo = repo;
    }
}

// Field Injection (Not recommended for production)
@Service
class ProductService {
    @Autowired
    private ProductRepository repo;
}
```

### Interview Explanation:
"When I explain Dependency Injection in interviews, I compare it to how we get food delivered instead of growing our own vegetables. In software, instead of a class creating its dependencies (like new UserRepository()), the dependencies are 'injected' from outside by the framework. This makes the code more modular, easier to test (you can inject mocks), and follows the Single Responsibility Principle. Spring Boot makes this even easier with auto-configuration and component scanning."

**Interview Tip:** DI promotes loose coupling. Constructor injection is preferred over field injection because it makes dependencies explicit and prevents null pointer exceptions.

</details>

<details><summary>2. What is Auto-Configuration in Spring Boot?</summary>

Spring Boot automatically configures beans based on the dependencies present in the classpath. This eliminates the need for manual bean configuration and reduces boilerplate code.

### How It Works Internally?
1. **@SpringBootApplication** combines three annotations:
   - **@Configuration**: Marks the class as a source of bean definitions
   - **@EnableAutoConfiguration**: Enables auto-configuration
   - **@ComponentScan**: Scans for Spring components

2. **Auto-Configuration Process**:
   - Scans classpath for JAR files and classes
   - Loads auto-configuration classes from `META-INF/spring.factories`
   - Applies conditional configurations based on classpath and existing beans

3. **Conditional Annotations**:
   - `@ConditionalOnClass`: Only if class is present
   - `@ConditionalOnMissingBean`: Only if bean doesn't exist
   - `@ConditionalOnProperty`: Based on property values

Example: Adding `spring-boot-starter-data-jpa` automatically configures:
- DataSource bean
- EntityManagerFactory
- TransactionManager
- JPA repositories

### Real-World Example:
```java
@SpringBootApplication  // This enables auto-configuration
public class MyApplication {
    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
}

// With spring-boot-starter-web, you get:
// - Embedded Tomcat server
// - DispatcherServlet
// - JSON converters (Jackson)
// - Error pages
// - And much more...
```

### Interview Explanation:
"Auto-configuration is Spring Boot's magic that automatically sets up your application based on what dependencies you add. For example, when you add spring-boot-starter-data-jpa, Spring Boot automatically creates DataSource, EntityManager, and repository beans without you writing any configuration. It works by scanning the classpath and applying conditional configurations. This reduces development time from days to minutes, but you can always override the defaults when needed."

**Interview Tip:** Auto-configuration reduces boilerplate. Use @ConditionalOnProperty for custom configs. Mention that you can exclude specific auto-configurations with @SpringBootApplication(exclude = {...}).

</details>

<details><summary>3. Global Exception Handling</summary>

Instead of writing try-catch blocks in every controller method, Spring Boot allows centralized exception handling using @ControllerAdvice. This provides consistent error responses and better maintainability.

### Key Annotations:
- **@ControllerAdvice**: Global exception handler for controllers
- **@RestControllerAdvice**: Same as @ControllerAdvice + @ResponseBody
- **@ExceptionHandler**: Handles specific exception types

### Benefits:
- **Centralized Error Handling**: All exceptions handled in one place
- **Consistent API Responses**: Uniform error format across the application
- **Separation of Concerns**: Business logic separated from error handling
- **Better User Experience**: Meaningful error messages

### Complete Implementation:
```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    // Handle specific exceptions
    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity<ErrorResponse> handleNotFound(ResourceNotFoundException e) {
        ErrorResponse error = new ErrorResponse(
            HttpStatus.NOT_FOUND.value(),
            "Resource not found",
            e.getMessage(),
            LocalDateTime.now()
        );
        return new ResponseEntity<>(error, HttpStatus.NOT_FOUND);
    }

    // Handle validation errors
    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseEntity<ErrorResponse> handleValidation(MethodArgumentNotValidException e) {
        Map<String, String> errors = new HashMap<>();
        e.getBindingResult().getFieldErrors().forEach(error ->
            errors.put(error.getField(), error.getDefaultMessage())
        );

        ErrorResponse error = new ErrorResponse(
            HttpStatus.BAD_REQUEST.value(),
            "Validation failed",
            errors.toString(),
            LocalDateTime.now()
        );
        return new ResponseEntity<>(error, HttpStatus.BAD_REQUEST);
    }

    // Handle generic exceptions
    @ExceptionHandler(Exception.class)
    public ResponseEntity<ErrorResponse> handleGeneric(Exception e) {
        ErrorResponse error = new ErrorResponse(
            HttpStatus.INTERNAL_SERVER_ERROR.value(),
            "Internal server error",
            "An unexpected error occurred",
            LocalDateTime.now()
        );
        return new ResponseEntity<>(error, HttpStatus.INTERNAL_SERVER_ERROR);
    }
}

// Error response DTO
public class ErrorResponse {
    private int statusCode;
    private String title;
    private String message;
    private LocalDateTime timestamp;

    // constructors, getters, setters
}
```

### Custom Exceptions:
```java
// Custom exception
public class ResourceNotFoundException extends RuntimeException {
    public ResourceNotFoundException(String message) {
        super(message);
    }
}

// Usage in service
@Service
public class UserService {
    public User getUser(Long id) {
        return userRepository.findById(id)
            .orElseThrow(() -> new ResourceNotFoundException("User not found with id: " + id));
    }
}
```

### Interview Explanation:
"In a real-world application, you don't want try-catch blocks scattered throughout your controllers. Global exception handling with @ControllerAdvice allows you to centralize error handling, ensuring consistent error responses. For example, instead of returning different error formats from different controllers, you can have a single place that converts all exceptions to a standard JSON error response. This is especially important for REST APIs where clients expect consistent error formats."

**Interview Tip:** Centralizes error handling, improves maintainability. Always return meaningful error messages, not stack traces in production.

</details>

<details><summary>4. How do you validate request body in Spring Boot?</summary>

Spring Boot uses Bean Validation (JSR-380) with Hibernate Validator to validate request data. Validation ensures data integrity and provides meaningful error messages to clients.

### Key Annotations:
- **@Valid**: Triggers validation on the annotated object
- **@NotNull**: Field cannot be null
- **@NotEmpty**: Collection/string cannot be null or empty
- **@NotBlank**: String cannot be null, empty, or whitespace
- **@Size(min, max)**: Size constraints for strings, collections, arrays
- **@Email**: Valid email format
- **@Min/@Max**: Numeric constraints
- **@Pattern**: Regex validation

### Complete Implementation:
```java
// DTO with validation annotations
public class UserDTO {
    @NotNull(message = "Name cannot be null")
    @Size(min = 2, max = 50, message = "Name must be between 2 and 50 characters")
    private String name;

    @NotBlank(message = "Email is required")
    @Email(message = "Email should be valid")
    private String email;

    @NotNull(message = "Age cannot be null")
    @Min(value = 18, message = "Age must be at least 18")
    @Max(value = 100, message = "Age cannot exceed 100")
    private Integer age;

    @Pattern(regexp = "^\\+?[1-9]\\d{1,14}$", message = "Invalid phone number")
    private String phoneNumber;

    // Nested validation
    @Valid
    @NotNull(message = "Address is required")
    private AddressDTO address;

    // getters, setters
}

public class AddressDTO {
    @NotBlank(message = "Street is required")
    private String street;

    @NotBlank(message = "City is required")
    private String city;

    @Pattern(regexp = "\\d{5}", message = "ZIP code must be 5 digits")
    private String zipCode;
}

// Controller usage
@RestController
@RequestMapping("/api/users")
@Validated  // For method-level validation
public class UserController {

    @PostMapping
    public ResponseEntity<User> createUser(@Valid @RequestBody UserDTO userDTO) {
        User user = userService.createUser(userDTO);
        return ResponseEntity.status(HttpStatus.CREATED).body(user);
    }

    // Method-level validation
    @GetMapping("/search")
    public ResponseEntity<List<User>> searchUsers(
            @RequestParam @NotBlank @Size(min = 2) String name) {
        List<User> users = userService.findByName(name);
        return ResponseEntity.ok(users);
    }
}
```

### Custom Validation:
```java
// Custom annotation
@Target({ElementType.FIELD})
@Retention(RetentionPolicy.RUNTIME)
@Constraint(validatedBy = StrongPasswordValidator.class)
public @interface StrongPassword {
    String message() default "Password must contain at least 8 characters, one uppercase, one lowercase, and one digit";
    Class<?>[] groups() default {};
    Class<? extends Payload>[] payload() default {};
}

// Validator implementation
public class StrongPasswordValidator implements ConstraintValidator<StrongPassword, String> {
    @Override
    public boolean isValid(String password, ConstraintValidatorContext context) {
        if (password == null) return false;
        return password.length() >= 8 &&
               password.matches(".*[A-Z].*") &&
               password.matches(".*[a-z].*") &&
               password.matches(".*\\d.*");
    }
}
```

### Interview Explanation:
"Request validation is crucial for API security and data integrity. In Spring Boot, I use JSR-380 annotations like @NotNull, @Size, @Email on DTOs, and @Valid in controllers to trigger validation. When validation fails, Spring throws MethodArgumentNotValidException, which I handle in @ControllerAdvice to return meaningful error messages. For complex business rules, I create custom validation annotations. This prevents invalid data from entering the system and provides clear feedback to API consumers."

**Interview Tip:** Validation happens before controller logic. Handle validation errors in @ControllerAdvice. Use @Validated for method-level validation.

</details>

<details><summary>5. JPA (Java Persistence API)</summary>

JPA is a specification for Object-Relational Mapping (ORM) that allows Java objects to be mapped to database tables. It provides a standard way to perform database operations without writing SQL.

### Key Concepts:
- **Entity**: Java class mapped to database table
- **EntityManager**: Interface for CRUD operations
- **JPQL**: Java Persistence Query Language (object-oriented SQL)
- **Criteria API**: Type-safe query construction
- **Persistence Context**: Cache of entity instances

### Entity Mapping:
```java
@Entity
@Table(name = "users")
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(name = "first_name", nullable = false, length = 50)
    private String firstName;

    @Column(name = "last_name", nullable = false, length = 50)
    private String lastName;

    @Column(unique = true, nullable = false)
    private String email;

    @Enumerated(EnumType.STRING)
    private UserStatus status;

    @Temporal(TemporalType.TIMESTAMP)
    @Column(name = "created_at")
    private Date createdAt;

    @OneToMany(mappedBy = "user", cascade = CascadeType.ALL, fetch = FetchType.LAZY)
    private List<Order> orders = new ArrayList<>();

    // Relationships
    @ManyToOne(fetch = FetchType.LAZY)
    @JoinColumn(name = "department_id")
    private Department department;

    // Lifecycle callbacks
    @PrePersist
    public void prePersist() {
        createdAt = new Date();
    }

    // constructors, getters, setters
}
```

### Repository Layer:
```java
@Repository
public interface UserRepository extends JpaRepository<User, Long> {

    // Derived queries
    List<User> findByLastName(String lastName);
    List<User> findByEmailContaining(String email);
    List<User> findByStatusAndDepartment(UserStatus status, Department department);

    // Custom queries with JPQL
    @Query("SELECT u FROM User u WHERE u.createdAt > :date")
    List<User> findUsersCreatedAfter(@Param("date") Date date);

    // Native SQL queries
    @Query(value = "SELECT * FROM users WHERE email LIKE %:email%", nativeQuery = true)
    List<User> findByEmailNative(@Param("email") String email);

    // Custom methods with @Query
    @Query("SELECT u FROM User u LEFT JOIN FETCH u.orders WHERE u.id = :id")
    Optional<User> findByIdWithOrders(@Param("id") Long id);

    // Modifying queries
    @Modifying
    @Query("UPDATE User u SET u.status = :status WHERE u.id = :id")
    int updateUserStatus(@Param("id") Long id, @Param("status") UserStatus status);
}
```

### Service Layer with Transactions:
```java
@Service
@Transactional(readOnly = true)
public class UserService {

    private final UserRepository userRepository;

    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    public List<User> getAllUsers() {
        return userRepository.findAll();
    }

    @Transactional
    public User createUser(UserDTO userDTO) {
        User user = new User();
        user.setFirstName(userDTO.getFirstName());
        user.setLastName(userDTO.getLastName());
        user.setEmail(userDTO.getEmail());
        return userRepository.save(user);
    }

    @Transactional
    public User updateUser(Long id, UserDTO userDTO) {
        User user = userRepository.findById(id)
            .orElseThrow(() -> new ResourceNotFoundException("User not found"));

        user.setFirstName(userDTO.getFirstName());
        user.setLastName(userDTO.getLastName());
        return userRepository.save(user);
    }
}
```

### Interview Explanation:
"JPA is the standard for ORM in Java. It maps Java objects to database tables, eliminating the need to write raw SQL for basic CRUD operations. I use entities with annotations like @Entity, @Table, @Column to define mappings. For complex queries, I use JPQL which is object-oriented. Spring Data JPA provides JpaRepository which gives me findBy, save, delete methods out of the box. The key is understanding lazy vs eager loading, and when to use @Transactional for data consistency."

**Interview Tip:** JPA abstracts database operations. Use @Query for custom queries. Be aware of N+1 query problem with lazy loading.

</details>

<details><summary>6. ResponseEntity</summary>

ResponseEntity is a powerful class in Spring that allows complete control over HTTP responses, including status codes, headers, and body. It's essential for building robust REST APIs.

### Why Use ResponseEntity?
- **Full HTTP Control**: Set status codes, headers, and body
- **Type Safety**: Generic type for response body
- **Flexibility**: Handle different response scenarios
- **REST Compliance**: Proper HTTP semantics

### Common Usage Patterns:
```java
@RestController
@RequestMapping("/api/users")
public class UserController {

    @GetMapping("/{id}")
    public ResponseEntity<User> getUser(@PathVariable Long id) {
        Optional<User> user = userService.findById(id);

        if (user.isPresent()) {
            return ResponseEntity.ok(user.get());
        } else {
            return ResponseEntity.notFound().build();
        }
    }

    @PostMapping
    public ResponseEntity<User> createUser(@Valid @RequestBody UserDTO userDTO) {
        User createdUser = userService.createUser(userDTO);

        // Return 201 Created with Location header
        URI location = ServletUriComponentsBuilder
            .fromCurrentRequest()
            .path("/{id}")
            .buildAndExpand(createdUser.getId())
            .toUri();

        return ResponseEntity.created(location).body(createdUser);
    }

    @PutMapping("/{id}")
    public ResponseEntity<User> updateUser(@PathVariable Long id, @Valid @RequestBody UserDTO userDTO) {
        try {
            User updatedUser = userService.updateUser(id, userDTO);
            return ResponseEntity.ok(updatedUser);
        } catch (ResourceNotFoundException e) {
            return ResponseEntity.notFound().build();
        }
    }

    @DeleteMapping("/{id}")
    public ResponseEntity<Void> deleteUser(@PathVariable Long id) {
        try {
            userService.deleteUser(id);
            return ResponseEntity.noContent().build(); // 204 No Content
        } catch (ResourceNotFoundException e) {
            return ResponseEntity.notFound().build();
        }
    }

    @GetMapping
    public ResponseEntity<List<User>> getUsers(
            @RequestParam(defaultValue = "0") int page,
            @RequestParam(defaultValue = "10") int size) {

        Page<User> userPage = userService.getUsers(PageRequest.of(page, size));

        return ResponseEntity.ok()
            .header("X-Total-Count", String.valueOf(userPage.getTotalElements()))
            .header("X-Total-Pages", String.valueOf(userPage.getTotalPages()))
            .body(userPage.getContent());
    }
}
```

### Static Factory Methods:
```java
// Success responses
ResponseEntity.ok()                    // 200 OK
ResponseEntity.ok(body)               // 200 OK with body
ResponseEntity.created(uri)           // 201 Created
ResponseEntity.accepted()             // 202 Accepted
ResponseEntity.noContent()            // 204 No Content

// Error responses
ResponseEntity.badRequest()           // 400 Bad Request
ResponseEntity.notFound()             // 404 Not Found
ResponseEntity.status(409).build()    // 409 Conflict

// Custom responses
ResponseEntity.status(HttpStatus.TOO_MANY_REQUESTS)
    .header("Retry-After", "60")
    .body("Rate limit exceeded");
```

### Advanced Usage with Headers:
```java
@GetMapping("/download/{fileId}")
public ResponseEntity<byte[]> downloadFile(@PathVariable String fileId) {
    byte[] fileContent = fileService.getFileContent(fileId);
    String fileName = fileService.getFileName(fileId);

    HttpHeaders headers = new HttpHeaders();
    headers.setContentType(MediaType.APPLICATION_OCTET_STREAM);
    headers.setContentDispositionFormData("attachment", fileName);
    headers.setContentLength(fileContent.length);

    return ResponseEntity.ok()
        .headers(headers)
        .body(fileContent);
}
```

### Interview Explanation:
"ResponseEntity gives you complete control over HTTP responses. Instead of just returning objects (which Spring converts to JSON with 200 OK), you can set specific status codes, add headers, and handle different scenarios properly. For example, when creating a resource, you return 201 Created with a Location header pointing to the new resource. When deleting, you return 204 No Content. This is crucial for REST API design and proper HTTP semantics."

**Interview Tip:** Use for custom responses, not just returning objects. Always use appropriate HTTP status codes and headers.

</details>

<details><summary>7. Types of Exceptions (from GlobalExceptionHandler)</summary>

- 403 Forbidden: AccessDeniedException
- 404 Not Found: UsernameNotFoundException, ResourceNotFoundException
- 400 Bad Request: ExecutionException, InterruptedException, MethodArgumentNotValidException, etc.
- 405 Method Not Allowed: HttpRequestMethodNotSupportedException
- 500 Internal Server Error: Exception (generic)

**Interview Tip:** Map exceptions to appropriate HTTP status codes for REST APIs.

</details>

<details><summary>8. Spring Boot Topics</summary>

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

</details>

<details><summary>9. Spring Boot Annotations</summary>

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

</details>

<details><summary>10. RequestParam, PathVariable, RequestBody, ResponseBody</summary>

| Annotation     | Used For              | Example URL          | Example Usage |
|----------------|-----------------------|----------------------|---------------|
| @RequestParam | Query parameters     | /greet?name=Srini   | @GetMapping("/greet") public String greet(@RequestParam String name) |
| @PathVariable | URL path variables    | /users/101          | @GetMapping("/users/{id}") public String getUser(@PathVariable int id) |
| @RequestBody  | JSON body to object   | /createUser (POST)  | @PostMapping("/createUser") public String createUser(@RequestBody User user) |
| @ResponseBody | Return value as response | /welcome           | @GetMapping("/welcome") @ResponseBody public String welcome() |

**Interview Tip:** @RequestParam for optional params, @PathVariable for required path parts.

</details>

<details><summary>11. @Autowired vs Constructor Injection</summary>

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

</details>

<details><summary>12. Spring Profiles</summary>

Spring Profiles allow you to have different configurations for different environments (dev, test, prod).

Use @Profile annotation on beans or @ConditionalOnProperty.

Example:
```java
@Configuration
@Profile("dev")
class DevConfig {
    @Bean
    DataSource dataSource() {
        return new H2DataSource(); // in-memory DB for dev
    }
}

@Configuration
@Profile("prod")
class ProdConfig {
    @Bean
    DataSource dataSource() {
        return new MySQLDataSource(); // production DB
    }
}
```

**Interview Tip:** Use profiles to manage environment-specific configurations. Activate with spring.profiles.active=dev.

</details>

<details><summary>13. Spring Boot Actuator</summary>

Spring Boot Actuator provides production-ready features like health checks, metrics, and monitoring.

Key endpoints:
- /actuator/health - Application health status
- /actuator/info - Application info
- /actuator/metrics - Application metrics
- /actuator/env - Environment properties

Enable in application.properties:
```properties
management.endpoints.web.exposure.include=health,info,metrics
```

**Interview Tip:** Actuator helps monitor application health and performance in production.

</details>

<details><summary>14. Spring Security Basics</summary>

Spring Security provides comprehensive security services for Java applications, including authentication, authorization, and protection against common attacks. It's the de facto standard for securing Spring applications.

### Core Concepts:
- **Authentication**: Verifying user identity (who you are)
- **Authorization**: Checking permissions (what you can do)
- **Principal**: Currently authenticated user
- **GrantedAuthority**: Permissions/roles assigned to user
- **SecurityContext**: Holds authentication information

### Basic Configuration:
```java
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Autowired
    private UserDetailsService userDetailsService;

    @Autowired
    private PasswordEncoder passwordEncoder;

    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
        auth.userDetailsService(userDetailsService)
            .passwordEncoder(passwordEncoder);
    }

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.csrf().disable()
            .authorizeRequests()

            // Public endpoints
            .antMatchers("/api/auth/**").permitAll()
            .antMatchers("/h2-console/**").permitAll()

            // Role-based access
            .antMatchers("/api/admin/**").hasRole("ADMIN")
            .antMatchers("/api/user/**").hasAnyRole("USER", "ADMIN")
            .antMatchers(HttpMethod.GET, "/api/products/**").permitAll()
            .antMatchers(HttpMethod.POST, "/api/products/**").hasRole("ADMIN")

            // All other requests need authentication
            .anyRequest().authenticated()

            .and()
            .sessionManagement().sessionCreationPolicy(SessionCreationPolicy.STATELESS)
            .and()
            .addFilterBefore(jwtAuthenticationFilter(), UsernamePasswordAuthenticationFilter.class);
    }

    @Bean
    public PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }
}
```

### JWT Authentication Implementation:
```java
@Component
public class JwtAuthenticationFilter extends OncePerRequestFilter {

    @Autowired
    private JwtUtil jwtUtil;

    @Autowired
    private UserDetailsService userDetailsService;

    @Override
    protected void doFilterInternal(HttpServletRequest request,
                                    HttpServletResponse response,
                                    FilterChain filterChain) throws ServletException, IOException {

        final String authHeader = request.getHeader("Authorization");
        final String jwt;
        final String userEmail;

        if (authHeader == null || !authHeader.startsWith("Bearer ")) {
            filterChain.doFilter(request, response);
            return;
        }

        jwt = authHeader.substring(7);
        userEmail = jwtUtil.extractUsername(jwt);

        if (userEmail != null && SecurityContextHolder.getContext().getAuthentication() == null) {
            UserDetails userDetails = userDetailsService.loadUserByUsername(userEmail);

            if (jwtUtil.isTokenValid(jwt, userDetails)) {
                UsernamePasswordAuthenticationToken authToken =
                    new UsernamePasswordAuthenticationToken(userDetails, null, userDetails.getAuthorities());
                authToken.setDetails(new WebAuthenticationDetailsSource().buildDetails(request));
                SecurityContextHolder.getContext().setAuthentication(authToken);
            }
        }

        filterChain.doFilter(request, response);
    }
}
```

### UserDetails and UserDetailsService:
```java
@Entity
public class User implements UserDetails {
    @Id
    @GeneratedValue
    private Long id;

    @Column(unique = true)
    private String email;

    private String password;

    @Enumerated(EnumType.STRING)
    private Role role;

    private boolean enabled = true;

    @Override
    public Collection<? extends GrantedAuthority> getAuthorities() {
        return List.of(new SimpleGrantedAuthority("ROLE_" + role.name()));
    }

    @Override
    public String getUsername() {
        return email;
    }

    @Override
    public boolean isAccountNonExpired() {
        return true;
    }

    @Override
    public boolean isAccountNonLocked() {
        return true;
    }

    @Override
    public boolean isCredentialsNonExpired() {
        return true;
    }

    @Override
    public boolean isEnabled() {
        return enabled;
    }
}

@Service
public class UserDetailsServiceImpl implements UserDetailsService {

    @Autowired
    private UserRepository userRepository;

    @Override
    public UserDetails loadUserByUsername(String email) throws UsernameNotFoundException {
        User user = userRepository.findByEmail(email)
            .orElseThrow(() -> new UsernameNotFoundException("User not found"));

        return user;
    }
}
```

### Method-Level Security:
```java
@Service
public class ProductService {

    @PreAuthorize("hasRole('ADMIN')")
    public Product createProduct(ProductDTO productDTO) {
        // Only admins can create products
        return productRepository.save(new Product(productDTO));
    }

    @PostAuthorize("returnObject.owner == authentication.name or hasRole('ADMIN')")
    public Product getProduct(Long id) {
        // Users can see their own products or admins can see all
        return productRepository.findById(id).orElse(null);
    }

    @PreFilter("filterObject.owner == authentication.name")
    public List<Product> getMyProducts(List<Product> products) {
        // Filter the input list to only user's products
        return products;
    }
}
```

### Interview Explanation:
"Spring Security handles authentication and authorization in Spring applications. I configure it by extending WebSecurityConfigurerAdapter and overriding configure methods. For JWT authentication, I create a filter that extracts the token from Authorization header, validates it, and sets the authentication in SecurityContext. I use @PreAuthorize for method-level security and configure URL-based security in the HttpSecurity config. The key is understanding the difference between authentication (who you are) and authorization (what you can do)."

**Interview Tip:** Spring Security secures applications with minimal configuration. Use @PreAuthorize for method-level security. Always use BCrypt for password encoding.

</details>

<details><summary>15. REST API Design Best Practices</summary>

### HTTP Methods
- GET: Retrieve data
- POST: Create new resource
- PUT: Update existing resource
- DELETE: Remove resource
- PATCH: Partial update

### Status Codes
- 200 OK: Success
- 201 Created: Resource created
- 400 Bad Request: Invalid input
- 401 Unauthorized: Authentication required
- 403 Forbidden: Access denied
- 404 Not Found: Resource not found
- 500 Internal Server Error: Server error

### Best Practices
- Use nouns for endpoints (/users, /orders)
- Use plural nouns
- Use HTTP status codes properly
- Version your APIs (/v1/users)
- Use HATEOAS for discoverability

**Interview Tip:** Follow REST conventions for maintainable APIs. Use proper HTTP methods and status codes.

</details>

<details><summary>16. Spring Boot Testing</summary>

Spring Boot provides comprehensive testing support with various testing slices and utilities. Testing is crucial for maintaining code quality and preventing regressions.

### Testing Pyramid:
1. **Unit Tests** (Bottom layer - most numerous)
2. **Integration Tests** (Middle layer)
3. **End-to-End Tests** (Top layer - fewest)

### Unit Testing:
```java
@SpringBootTest
class UserServiceTest {

    @Autowired
    private UserService userService;

    @MockBean
    private UserRepository userRepository;

    @Test
    void createUser_ShouldReturnSavedUser() {
        // Arrange
        UserDTO userDTO = new UserDTO("John", "Doe", "john@example.com");
        User savedUser = new User(1L, "John", "Doe", "john@example.com");

        when(userRepository.save(any(User.class))).thenReturn(savedUser);

        // Act
        User result = userService.createUser(userDTO);

        // Assert
        assertNotNull(result);
        assertEquals("John", result.getFirstName());
        assertEquals("Doe", result.getLastName());
        verify(userRepository).save(any(User.class));
    }

    @Test
    void getUserById_UserExists_ShouldReturnUser() {
        // Arrange
        User user = new User(1L, "John", "Doe", "john@example.com");
        when(userRepository.findById(1L)).thenReturn(Optional.of(user));

        // Act
        Optional<User> result = userService.getUserById(1L);

        // Assert
        assertTrue(result.isPresent());
        assertEquals("John", result.get().getFirstName());
    }

    @Test
    void getUserById_UserNotFound_ShouldThrowException() {
        // Arrange
        when(userRepository.findById(1L)).thenReturn(Optional.empty());

        // Act & Assert
        assertThrows(ResourceNotFoundException.class, () -> {
            userService.getUserById(1L);
        });
    }
}
```

### Integration Testing:
```java
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
class UserControllerIntegrationTest {

    @Autowired
    private TestRestTemplate restTemplate;

    @Autowired
    private UserRepository userRepository;

    @BeforeEach
    void setUp() {
        userRepository.deleteAll();
    }

    @Test
    void createUser_ShouldReturnCreatedUser() {
        // Arrange
        UserDTO userDTO = new UserDTO("Jane", "Smith", "jane@example.com");

        // Act
        ResponseEntity<User> response = restTemplate.postForEntity("/api/users", userDTO, User.class);

        // Assert
        assertEquals(HttpStatus.CREATED, response.getStatus());
        assertNotNull(response.getBody());
        assertEquals("Jane", response.getBody().getFirstName());
        assertNotNull(response.getBody().getId());
    }

    @Test
    void getUser_UserExists_ShouldReturnUser() {
        // Arrange
        User savedUser = userRepository.save(new User(null, "Bob", "Wilson", "bob@example.com"));

        // Act
        ResponseEntity<User> response = restTemplate.getForEntity("/api/users/" + savedUser.getId(), User.class);

        // Assert
        assertEquals(HttpStatus.OK, response.getStatus());
        assertNotNull(response.getBody());
        assertEquals("Bob", response.getBody().getFirstName());
    }

    @Test
    void getUser_UserNotFound_ShouldReturn404() {
        // Act
        ResponseEntity<String> response = restTemplate.getForEntity("/api/users/999", String.class);

        // Assert
        assertEquals(HttpStatus.NOT_FOUND, response.getStatus());
    }
}
```

### Testing Slices (Focused Testing):
```java
// Test only web layer
@WebMvcTest(UserController.class)
class UserControllerTest {

    @Autowired
    private MockMvc mockMvc;

    @MockBean
    private UserService userService;

    @Test
    void getUser_ShouldReturnUser() throws Exception {
        User user = new User(1L, "John", "Doe", "john@example.com");
        when(userService.getUserById(1L)).thenReturn(Optional.of(user));

        mockMvc.perform(get("/api/users/1"))
            .andExpect(status().isOk())
            .andExpect(jsonPath("$.firstName").value("John"))
            .andExpect(jsonPath("$.email").value("john@example.com"));
    }
}

// Test only data layer
@DataJpaTest
class UserRepositoryTest {

    @Autowired
    private UserRepository userRepository;

    @Test
    void saveUser_ShouldPersistUser() {
        User user = new User(null, "Alice", "Brown", "alice@example.com");
        User savedUser = userRepository.save(user);

        assertNotNull(savedUser.getId());
        assertEquals("Alice", savedUser.getFirstName());
    }

    @Test
    void findByEmail_ShouldReturnUser() {
        User user = userRepository.save(new User(null, "Charlie", "Davis", "charlie@example.com"));
        Optional<User> found = userRepository.findByEmail("charlie@example.com");

        assertTrue(found.isPresent());
        assertEquals("Charlie", found.get().getFirstName());
    }
}
```

### Mocking with Mockito:
```java
@ExtendWith(MockitoExtension.class)
class UserServiceUnitTest {

    @Mock
    private UserRepository userRepository;

    @Mock
    private EmailService emailService;

    @InjectMocks
    private UserService userService;

    @Test
    void createUser_ShouldSendWelcomeEmail() {
        // Arrange
        UserDTO userDTO = new UserDTO("Test", "User", "test@example.com");
        User savedUser = new User(1L, "Test", "User", "test@example.com");

        when(userRepository.save(any(User.class))).thenReturn(savedUser);
        doNothing().when(emailService).sendWelcomeEmail(anyString());

        // Act
        User result = userService.createUser(userDTO);

        // Assert
        assertNotNull(result);
        verify(userRepository).save(any(User.class));
        verify(emailService).sendWelcomeEmail("test@example.com");
    }
}
```

### Interview Explanation:
"Testing in Spring Boot follows the testing pyramid with unit tests at the base, integration tests in the middle, and e2e tests at the top. I use @SpringBootTest for full integration tests, @WebMvcTest for controller testing, and @DataJpaTest for repository testing. For unit tests, I mock dependencies with @MockBean or Mockito. The key is testing behavior, not implementation, and maintaining fast, reliable tests that give confidence in code changes."

**Interview Tip:** Use @SpringBootTest for integration tests, @WebMvcTest for controller tests, @DataJpaTest for repository tests. Focus on testing behavior over implementation.

</details>

<details><summary>17. Caching in Spring Boot</summary>

Spring Boot supports caching with annotations.

Enable caching:
```java
@SpringBootApplication
@EnableCaching
class Application { }
```

Cache methods:
```java
@Service
class UserService {
    @Cacheable("users")
    public User getUser(Long id) {
        return repository.findById(id).orElse(null);
    }

    @CacheEvict(value = "users", key = "#user.id")
    public User updateUser(User user) {
        return repository.save(user);
    }
}
```

Supported cache providers: EhCache, Redis, Caffeine, etc.

**Interview Tip:** Caching improves performance. Use @Cacheable for read operations, @CacheEvict for updates.

</details>

<details><summary>18. Spring Boot with Docker</summary>

Dockerize Spring Boot application with multi-stage build.

Dockerfile:
```dockerfile
# Build stage
FROM maven:3.8-openjdk-17 AS build
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean package -DskipTests

# Runtime stage
FROM openjdk:17-jre-slim
WORKDIR /app
COPY --from=build /app/target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
```

**Interview Tip:** Multi-stage builds reduce image size. Use JRE instead of JDK for runtime.

</details>

<details><summary>19. JWT Authentication in Spring Boot</summary>

JSON Web Tokens for stateless authentication.

Add dependency:
```xml
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt</artifactId>
    <version>0.9.1</version>
</dependency>
```

Generate JWT:
```java
@Component
class JwtUtil {
    public String generateToken(String username) {
        return Jwts.builder()
            .setSubject(username)
            .setIssuedAt(new Date())
            .setExpiration(new Date(System.currentTimeMillis() + 1000 * 60 * 60 * 10))
            .signWith(SignatureAlgorithm.HS256, secret)
            .compact();
    }

    public String extractUsername(String token) {
        return Jwts.parser().setSigningKey(secret).parseClaimsJws(token).getBody().getSubject();
    }
}
```

**Interview Tip:** JWT enables stateless authentication. Store secret securely, set reasonable expiration.

</details>

<details><summary>20. Spring Boot Microservices</summary>

Spring Boot with Spring Cloud for microservices.

Key components:
- Spring Cloud Config: Centralized configuration
- Spring Cloud Gateway: API Gateway
- Eureka: Service Discovery
- Spring Cloud Sleuth: Distributed tracing
- Resilience4j: Circuit breaker

Example service registration:
```java
@SpringBootApplication
@EnableEurekaClient
class UserServiceApplication {
    public static void main(String[] args) {
        SpringApplication.run(UserServiceApplication.class, args);
    }
}
```

**Interview Tip:** Microservices with Spring Boot enable scalable, maintainable systems. Use service discovery for inter-service communication.

</details>
