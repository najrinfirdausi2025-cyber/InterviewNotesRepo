# 🌱 Java Spring Framework – Interview‑Ready Notes

what are top 50 interview question on java spring 

---
🌱 Spring Core & Basics

- What is Spring Framework? 
- What are the advantages of Spring?
- What problems does Spring solve?
- What is Inversion of Control (IoC)?
- What is Dependency Injection (DI)?
- Difference between IoC and DI?
- What are Spring Beans?
- What are the types of Spring Bean scopes?
- What is Spring Container?
- Difference between BeanFactory and ApplicationContext?
- What are the types of Dependency Injection?
- Which DI is recommended and why?
- What is @Autowired?
- Difference between @Component, @Service, @Repository, @Controller?
- What is @Qualifier?
- What is @Primary?
- What is Spring Java-based configuration?
- Difference between XML and Annotation configuration?
- What is @Configuration?
- What is @Bean?
- What is Spring Bean lifecycle?
- What are init and destroy methods?
- What is @PostConstruct and @PreDestroy?
- What is lazy initialization?
- What is eager initialization?


---

## 1. What is Spring Framework?

- Spring is a **lightweight, open‑source Java framework** for building **enterprise‑level applications**
- It provides features such as **Dependency Injection(DI)**, **Inversion of Control(IOC)**, to manage the object cration & lifecycle by framework itself, 
- It also provides  **Aspect-Oriented Programming(AOP)** , declarative **transaction management** , **logging**, **security**, and seamless integration with ORM frameworks like **Hibernate** for efficient database operations.
- Spring offers a rich ecosystem of modules (Spring MVC, Spring JDBC, Spring Data, Spring ORM, and Spring Security ) for end-to-end rapid App development and serves as the foundation for Spring Boot.


### Key Problems Spring Solves
- Tight coupling between classes
- Complex object creation, boilerplate codes
- Reduces repetitive code in JDBC, transactions, and configuration.
- Difficult testing with mocks and dependency injection.
- Spring solves complexity, tight coupling, and boilerplate in enterprise Java applications.

---

## 2. Advantages of Spring

- ♻️ __Lightweight Opensource and modular:__ – you use only what you need, reducing application complexity.
- 🔁 __Loose coupling with Dependency Injection (DI) & Inversion of Control mechanism:__ – improves code maintainability, testing, and flexibility.
- 🧪 __Powerful transaction management:__ – supports declarative transactions across databases and ORM , Messaging , Security and tools like Hibernate.
- ♻️ __AOP support:__ – cleanly handles cross-cutting concerns such as logging, security, and auditing.
- 🔌 __Easy integration:__ – works seamlessly with Hibernate, JPA, JDBC, REST, messaging, and other frameworks.
- 🔁 __Spring Boot support:__ – enables **Rapid** end-to-end App development development with minimal configuration.
- 🧪 __Easy unit & integration testing:__  Mocking object supported with dependency injection
- ♻️ __Strong community and ecosystem:__  excellent documentation, tools, and long-term support.

---

## 3. Inversion of Control (IoC)

- Inversion of Control (IoC) is a design principle , where Spring container takes control of object creation and dependency management instead of the application code.
- That is  👉 Instead of the developer creating objects using **new** operator, Spring creates, manages, and injects them. 
- Developer does **not use `new` keyword** directly
- Spring container manages object lifecycle, object creation and dependency management is transferred from the program to the Spring container.

### Traditional Approach (Without IoC)

```java
Engine engine = new PetrolEngine();
Car car = new Car(engine);

// Developer controls object creation
// Tight coupling between classes
```

### With Spring IoC
```java
@Component
class PetrolEngine implements Engine {}

@Component
class Car {
    @Autowired
    Engine engine;
}

// Spring container creates objects
// Spring manages dependencies automatically
```
### IoC Containers

- **BeanFactory** – basic container
- **ApplicationContext** – advanced (recommended)

---

## 4. Dependency Injection (DI)
- `Dependency Injection` is a `design pattern` in which an object does not create its own dependencies.
- Instead, the Spring Framework creates and provides the required dependent objects and injects them at runtime, rather than the class creating them itself.
- 👉 This promotes loose coupling, easy testing, and better maintainability.

### Types of Dependency Injection 

- Constructor Injection ✅ (Best practice)
- Setter Injection
- Field Injection (Not recommended for testing)


### Problem without Dependency Injection (Tight Coupling)

### Example – Constructor Injection

```java
class Engine {
    public void start() {
        System.out.println("Engine started");
    }
}

class Car {
    private Engine engine = new Engine(); // tightly coupled

    public void drive() {
        engine.start();
        System.out.println("Car is running");
    }
}

```
❌ Problems:

- Car is tightly coupled to Engine
- Difficult to replace Engine or test Car

### How Dependency Injection (Loose Coupling) solve it ?

### Step 1: Create Interface
```java
public interface Engine {
    void start();
}
```
### Step 2: Implement Interface
```java
@Component
public class PetrolEngine implements Engine {
    public void start() {
        System.out.println("Petrol Engine started");
    }
}
```
### Step 3: Inject Dependency using Constructor Injection (Recommended)
```java
@Component
public class Car {

    private final Engine engine;

    @Autowired
    public Car(Engine engine) {
        this.engine = engine;
    }

    public void drive() {
        engine.start();
        System.out.println("Car is running");
    }
}
```
### Advantages of DI

- Loose coupling between classes
- Easy unit testing (mock dependencies)
- Better code maintainability
- Easy to switch implementations



---

## What are Spring Modules?

- **#1 Core Container** – Provides IoC and Dependency Injection.
- **#2 AOP Module** – Handles cross-cutting concerns like logging and security.
- **#3 Data Access Module** – Simplifies JDBC, ORM (Hibernate/JPA), and transactions
- **#4 Web Module** – Used to build web and REST applications (Spring MVC, WebFlux).
- **#5 Security & Test Modules** – Provides authentication, authorization, and testing support.

```sql
+--------------------------------------------------+
|                 Spring Framework                 |
+--------------------------------------------------+
|  Core Container                                  |
|  - Core | Beans | Context | SpEL                 |
+--------------------------------------------------+
|  AOP & Aspects                                   |
|  - Spring AOP | Spring Aspects                   |
+--------------------------------------------------+
|  Data Access / Integration                       |
|  - JDBC | ORM (Hibernate/JPA) | Transactions     |
+--------------------------------------------------+
|  Web                                            |
|  - Spring MVC | Spring Web | WebFlux             |
+--------------------------------------------------+
|  Security & Testing                              |
|  - Spring Security | Spring Test                 |
+--------------------------------------------------+
```
<img width="729" height="385" alt="image" src="https://github.com/user-attachments/assets/ad64013d-30df-480d-ac38-55726c440f5d" />

---
### Difference between IoC and DI ?
 
-  **IoC says who creates objects, DI says how they are provided.**
-  IoC is a principle where Spring controls object creation, and DI is the technique Spring uses to inject dependencies into those objects.
  <img width="1581" height="623" alt="image" src="https://github.com/user-attachments/assets/46ad7fd5-ea45-48a3-9673-30688e4d475a" />

---
## What are Spring Beans ? 
- A Spring Bean is a **Java object** - whose entire lifecycle (create → configure → inject → destroy) is managed by the Spring Framework IoC container.
- Beans are created based on configuration metadata (XML, annotations, or Java config)

### [1] Using XML (legacy)
```xml
<bean id="userService" class="com.example.UserService"/>
```
### [2] Using Annotations (most common)
```java
@Component
public class UserService {
}
```
### [3] Using Java Configuration
```java
@Configuration
public class AppConfig {

    @Bean
    public UserService userService() {
        return new UserService();
    }
}
```

- Beans support Dependency Injection (DI)
- They promote loose coupling and easy testing

---

## What are the types of Spring Bean scopes?
- `Bean Scope` defines `how many instances` of a Spring Bean are created and `how long` they live within the Spring container.

### Types of Bean Scopes

- `singleton` (default) – one instance per Spring container
- `prototype` – new instance every time it’s requested
- `request` – one instance per HTTP request
- `session` – one instance per HTTP session
- `application` – one instance per ServletContext
- `websocket` – one instance per WebSocket session

### prototype: type Bean scopes – new instance every time it’s requested
```java

@Component
@Scope("prototype")
public class PaymentService {
}

@Autowired
PaymentService p1;

@Autowired
PaymentService p2;

// A new instance is created EVERY time PaymentService is requested
// p1 → one PaymentService object
// p2 → another PaymentService object
// p1 != p2  ( Both are different objects as Bean scope creation type: prototype)

 
// The lifecycle lasts only until the client code releases the reference, i.e- Until the client code is done with it
// Spring IOC container manages it only up to dependency injection. After that, the bean’s lifecycle is managed by the client, not Spring.
```
### Singleton Bean scope - only one isntance allowed
```java
@Component
public class OrderService {

    @Autowired
    private PaymentService p1;

    @Autowired
    private PaymentService p2;

    // Here both P1 and P2 are same objects as Bean scope creation type: singleton by default - only one isntance allowed
}
```
### Request scope
- Request scope creates a single bean instance per one HTTP request, shared within that request and destroyed once the request completes.

```java

@Component
@RequestScope
public class PaymentService {
}


@RestController
public class OrderController {

    @Autowired
    private PaymentService p1;

    @Autowired
    private PaymentService p2;

    @GetMapping("/pay")
    public String pay() {
        return String.valueOf(p1 == p2);  //true  ✔ Same request → same bean instance
    }
}
```
- Same HTTP request → same PaymentService instance
- Different HTTP request → new instance
- Previous Bean instance is → destroyed after request completion


### Importance of Bean Scope

- Controls object creation and memory usage
- Helps manage stateful vs stateless beans
- Improves performance and scalability
- Prevents thread-safety issues

---
### Bean Lifecycle (1-liner)

- __Instantiate → Populate properties → Initialize → Ready → Destroy__

---

## What is Spring Container?

- The **Spring Container** is responsible for **creating, configuring, and managing the lifecycle** of **Spring Beans and injecting dependencies**.
- `Spring Container` = `Bean Factory` + `Dependency Injection` + `Lifecycle Management`


<img width="1658" height="660" alt="image" src="https://github.com/user-attachments/assets/ede6c3bd-8bf4-4b70-b326-d25c409dcec6" />

### Responsibilities of Spring Container

- Creates Spring Beans
- Injects dependencies (DI)
- Manages bean lifecycle
- Handles bean scopes (singleton, prototype, request, etc.)
- Manages configuration metadata

### Types of Spring Containers

- `BeanFactory` – basic container (lazy initialization)
- `ApplicationContext` – advanced container (most commonly used)

### BeanFactory (Basic Spring Container)
- `BeanFactory` is a basic `Spring container` that uses `lazy initialization` and creates `beans/bean objects` only when they are requested.

__Key Characteristics:__

- Basic IoC container
- Supports Dependency Injection
- Uses lazy initialization (beans are created only when requested)
- Lightweight and memory-efficient
- No advanced enterprise features by default
  
__Lazy Initialization Explained:__

- Beans are NOT created at application startup
- A bean is created only when getBean() is called

```java
// Beans
public class PaymentService {
    public PaymentService() {
        System.out.println("PaymentService created");
    }
}

BeanFactory factory = new ClassPathXmlApplicationContext("beans.xml");
PaymentService service = factory.getBean(PaymentService.class);  // PaymentService created
```


### Example using ApplicationContext:
- `ApplicationContext` is an advanced Spring container that extend BeanFactory , It support creates, configures, and manages Spring beans.
- It provides dependency injection, lifecycle management, and enterprise features like `AOP`, `events`, and `internationalization`.
- By default, it eagerly initializes singleton beans at application startup.
- `ApplicationContext` is almost always preferred/recommanded over `BeanFactory`

```java
//Bean => Creates PaymentService

@Component
public class PaymentService {
    public String pay() {
        return "Payment Successful";
    }
}

// Controller / Client => Creates OrderController

@RestController
public class OrderController {

    @Autowired
    private PaymentService paymentService;

    @GetMapping("/pay")
    public String pay() {
        return paymentService.pay();  // Injects PaymentService into OrderController
    }
}

// Manages their ( PaymentService & OrderController) lifecycle
```

---

##  Difference between `BeanFactory` and `ApplicationContext`?

### Spring offers two main container abstractions:
    - 1. BeanFactory
    - 2. ApplicationContext
- These are interfaces, not concrete classes and they represent two different levels of container capability.
- Below is the hierarchy of the BeanFactory(I) and ApplicationContext(I) with some of their implementation classes.

<img width="800" height="324" alt="image" src="https://github.com/user-attachments/assets/ae89dd05-299f-499a-a4bb-489ded964aec" />

### BeanFactory :
- BeanFactory, defined in `org.springframework.beans.factory`, - is the `basic/root IoC container interface` in Spring.
- `XmlBeanFactory` implements `BeanFactory` (deprecated)
- It provides core functionalities such as bean creation and dependency injection.

__Key Characteristics:__
- Beans are created only when requested (on demand)
- This behavior is known as lazy initialization
- Suitable for lightweight or memory-constrained applications But Rarely used in  Real-world-Apps , mostly theoretical.

### ApplicationContext:
- `ApplicationContext`, defined in `org.springframework.context`, -- is an `Advanced container interface` that `extends BeanFactory` and provides additional `enterprise-level features`.
- `ClassPathXmlApplicationContext`, `FileSystemXmlApplicationContext`, etc, `implement ApplicationContext`
  
__Key Features:__

- Eager initialization (at startup, by default)
- Annotation-based configuration
- Advance feature like `Event` handling ,`Internationalization (i18n)`, `AOP` etc fully supported which are used in most Real-world-Apps

---

## What are the types of Dependency Injections in java spring ?
- Spring supports the 3 types of Dependency Injection
  
```
1. Constructor Injection ( Recommended ✅ )
2. Setter Injection
3. Field Injection (Not Recommended ❌)
```

###  `Constructor Injection ` => Dependencies are provided through the constructor.
```java
@Component
public class OrderService {

    private final PaymentService paymentService;

    @Autowired
    public OrderService(PaymentService paymentService) {
        this.paymentService = paymentService;   // Makes dependencies mandatory , Avoids NullPointerException
    }
}
```
### `Setter Injection` ( Recommended ✅ ) => Dependencies are injected using setter methods.

```java
@Component
public class OrderService {

    private PaymentService paymentService;

    @Autowired
    public void setPaymentService(PaymentService paymentService) {
        this.paymentService = paymentService;
    }

// Optional dependencies - Runtime reconfiguration via set Method
}
```
### `Field Injection`  (Not Recommended ❌) = > Dependencies are injected directly into fields. 

```java
@Component
public class OrderService {

    @Autowired
    private PaymentService paymentService;
}


// Hidden dependencies
// Breaks immutability
```
## Why is constructor injection preferred?
- 👉 Because it ensures mandatory dependencies, promotes immutability, and improves testability.

---

## When to Use What?
- __`Constructor Injection:`__ When we use Constructor Injection, dependency when a dependency is mandatory, immutable, Easy to Test.
- __`Setter Injection:`__ Setter method dependency is used when the dependency is optional or requires late initialization, Medium to Test
- __`Field Injection:`__ Field injection dependency is used for small projects, but not for production code, Difficult to Test.

```sql
Constructor Injection     → Mandatory & safe
Setter Injection          → Optional & flexible
Field Injection           → Simple but risky
```


## What is @Autowired?

- __`@Autowired`__ is a `Spring annotation` used for enabling automatic dependency injection, by instructing Spring to inject a required bean into a class.
- It tells the Spring container to find a matching bean and inject it into the required field, constructor, or setter.

## What if multiple beans of the same type exist ?
- When multiple beans of the same type exist, Spring throws __`NoUniqueBeanDefinitionException`__, which can be resolved using `@Qualifier`, `@Primary`, or bean name matching.

```java

// Explicit selection service (Selected using @Qualifier)

@Component("cardPaymentService")
public class CardPaymentService implements PaymentService {
    public String pay() {
        return "Paid using Card";
    }
}



// Something Else (Not injected unless asked)-ignored unless referenced

@Component("netBankingPaymentService")
public class NetBankingPaymentService implements PaymentService {
    public String pay() {
        return "Paid using Net Banking";
    }
}


// Default implementation / Primary Service

@Primary
@Component("upiPaymentService")
public class UpiPaymentService implements PaymentService {
    public String pay() {
        return "Paid using UPI";
    }
}

```
### Case 1: No @Qualifier → @Primary is injected

```java

@Component
public class OrderService {

    private final PaymentService paymentService;

   
    public OrderService(PaymentService paymentService) {
        this.paymentService = paymentService;
    }
}

 // ✔ Injected → UPI Payment Service
```
### Case 2: Explicit selection → @Qualifier overrides @Primary

```java
@Component
public class OrderService {

    private final PaymentService paymentService;

    public OrderService(
            @Qualifier("cardPaymentService") PaymentService paymentService) {
        this.paymentService = paymentService;
    }
}

// ✔ Injected → Card Payment Service
```
### Who wins ?
```
@Primary       → default choice
@Qualifier     → explicit choice (wins), override default choice
```





#############################################################
Allows correct behavior in web applications
---

```
### Bean Scopes

- `singleton` (default)
- `prototype`
- `request`
- `session`

```java
@Component
@Scope("prototype")
class UserService {}
```

---

## 6. Bean Life Cycle

### Bean Life Cycle Phases

1. Bean Instantiation
2. Dependency Injection
3. Initialization
4. Ready for use
5. Destruction

### Life Cycle Annotations

```java
@PostConstruct
public void init() {
    System.out.println("Bean initialized");
}

@PreDestroy
public void destroy() {
    System.out.println("Bean destroyed");
}
```

---

## 7. Spring Annotations (Very Important ⭐)

### Stereotype Annotations

- `@Component` – generic
- `@Service` – business logic
- `@Repository` – DAO layer
- `@Controller` – MVC controller
- `@RestController` – REST APIs

### Dependency Injection

- `@Autowired`
- `@Qualifier`
- `@Primary`

---

## 8. What is Spring Boot?

- Built on top of Spring Framework
- Eliminates XML configuration
- Provides **auto‑configuration**
- Comes with **embedded servers** (Tomcat)

### Benefits of Spring Boot

- Faster development
- Production‑ready features
- Minimal configuration

---

## 9. Spring Boot Application Structure

```java
@SpringBootApplication
public class DemoApplication {
    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }
}
```

### `@SpringBootApplication` Includes

- `@Configuration`
- `@EnableAutoConfiguration`
- `@ComponentScan`

---

## 10. REST Controller

- Used to build RESTful web services
- Returns JSON/XML response

```java
@RestController
@RequestMapping("/api")
public class HelloController {

    @GetMapping("/hello")
    public String hello() {
        return "Hello Spring";
    }
}
```

---

## 11. MVC vs REST

| MVC | REST |
|---|---|
| Returns View (HTML) | Returns Data (JSON) |
| `@Controller` | `@RestController` |
| Used for UI apps | Used for APIs |

---

## 12. application.properties

- Used for configuration
- Environment‑specific values

```properties
server.port=8081
spring.datasource.url=jdbc:mysql://localhost:3306/test
spring.datasource.username=root
spring.datasource.password=root
```

---

## 13. JPA & Hibernate

- Hibernate is an ORM framework
- JPA is a specification

### Entity Example

```java
@Entity
@Table(name = "users")
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;
}
```

### Repository

```java
public interface UserRepository extends JpaRepository<User, Long> {}
```

---

## 14. Common Interview Questions

- Difference between `@Component` and `@Service`?
- Why constructor injection is preferred?
- What is auto‑configuration?
- Difference between JPA and Hibernate?
- What is embedded server in Spring Boot?

---

## 15. Quick Interview Tips

- Prefer **constructor injection**
- Avoid field injection in production
- Know annotations clearly
- Explain concepts with examples

---

✅ **End of Notes** – Ready to push as `JavaSpringNotes.md` to GitHub 🚀




# Spring Data JPA and Hibernate

## What is Spring Data JPA

How to use Spring Data JPA

Create Coupon Service Data Access Layer

Create Product Service Data Access Layer

What are the different Entity Object States

Wha are various JPA Associations

What is Cascading

What is Lazy Loading

What are two levels of caching

How to configure Second Level Cache

