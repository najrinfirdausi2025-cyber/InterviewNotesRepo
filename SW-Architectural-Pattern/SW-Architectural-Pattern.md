## Model-View-Controller (MVC):

* __Web Applications__
- The Model-View-Controller (MVC) framework is an architectural/design pattern that separates an application into three main logical components `Model`, `View`, and `Controller`.
- Each architectural component is built to handle specific development aspects of an application. It isolates the business logic and presentation layer from each other.
- MVC is commonly used in web applications where the model represents the data (e.g., user information), the view represents the presentation layer (e.g., HTML pages), and the controller handles user input (e.g., HTTP requests).

__Features of MVC:__
- It provides a clear separation of business logic, UI logic, and input logic.
- It offers full control over your HTML and URLs which makes it easy to design web application architecture.
- It is a powerful URL-mapping component using which we can build applications that have comprehensible and searchable URLs.
- It supports Test Driven Development (TDD).


<img width="850" height="508" alt="image" src="https://github.com/user-attachments/assets/fc04d0d7-89cf-4087-9fa5-596f8b186efa" />

<img width="767" height="456" alt="image" src="https://github.com/user-attachments/assets/d8af322e-b9f9-4b97-82da-dfffc8c5ca88" />



# MVC Design Pattern – Full Stack Banking Application (Spring Boot + React + Azure)

---

## 1. MVC Concept (Interview Definition)

**MVC (Model–View–Controller)** separates application responsibilities into three layers:

| Layer | Responsibility |
|------|------|
| Model | Business data, rules, and database interaction |
| View | User Interface shown to users |
| Controller | Handles request and coordinates Model + View |

**Purpose:** Improves scalability, maintainability, and loose coupling.

---

## 2. Mapping Project Components to MVC

Your project actually contains **two MVC architectures**:

1. Backend MVC → Spring Boot (Server)
2. Frontend MVC-like → React SPA (Client)

---

# BACKEND MVC (Spring Boot)

## Controller Layer (Request Entry Point)
Handles HTTP requests coming from React frontend.

```java
@RestController
@RequestMapping("/api/accounts")
public class AccountController {

    @PostMapping("/transfer")
    public ResponseEntity<?> transfer(@Valid @RequestBody TransferRequest dto){
        transferService.transferMoney(dto);
        return ResponseEntity.ok("Transfer Successful");
    }
}
```

### 👉 Interview Explanation:

`Controller receives HTTP request, validates input DTO, calls Service layer and returns JSON response.`

**Responsibilities:**
- Accept API requests
- Validate input DTO
- Authenticate user
- Call service layer
- Return JSON response

**Examples: Your Controllers:**
- AccountController
- TransactionController
- AuthController
- AuditController

➡ This is the **C -> Controller in MVC**

---

## Service Layer (Business Logic – Part of Model)
Contains banking rules and transaction processing.

```java
@Transactional
public void transferMoney(TransferRequest dto){

    Account from = accountRepo.findById(dto.getFromId())
            .orElseThrow(() -> new AccountNotFoundException());

    Account to = accountRepo.findById(dto.getToId())
            .orElseThrow(() -> new AccountNotFoundException());

    if(from.getBalance() < dto.getAmount())
        throw new InsufficientBalanceException();

    from.debit(dto.getAmount());
    to.credit(dto.getAmount());

    transactionRepo.save(new Transaction(...));
}
```

### 👉 Interview Explanation:
`Service layer contains actual banking rules like balance validation, atomic transaction, and business operations.`

**Responsibilities:**
- Business validations
- Transaction management (ACID)
- Audit logging
- Email notification triggers

---

## Model Layer (Domain + Persistence)
Includes:

| Component | Role |
|------|------|
| Entities | Database tables mapping |
| Repository | Database queries |
| DTO | API data objects |
| Validation | Data integrity |
| AOP | Error models |
| Transaction Logs | Business state |

### Entity Example
```java
@Entity
public class Account {
   private Long id;
   private String owner;
   private BigDecimal balance;
}
```

### Repository
```java
public interface AccountRepository extends JpaRepository<Account, Long> {}
```

➡ This is the **M --> Model in MVC**

---

## Database
MySQL / PostgreSQL tables:
- accounts
- transactions
- users
- audit_logs

---

## View Layer (Backend Perspective)

- Spring Boot is REST based → returns JSON (returns JSON response instead of HTML UI.)
- So the backend "View" is actually JSON Response
 
```json
{
  "status": "SUCCESS",
  "transactionId": 78321,
  "balance": 4500
}
```

---

# FRONTEND MVC (React SPA)

React acts as the **real user interface-UI View**.

| React Component | MVC Role |
|------|------|
| React Pages | View |
| Axios API Calls | Controller (Client Side) |
| State (Redux/useState) | Model (UI State) |

Example:

```javascript
const transferMoney = async () => {
  await axios.post("/api/accounts/transfer", data, {
     headers: { Authorization: `Bearer ${token}` }
  });
}
```

---

# 3. End-to-End Flow (Fund Transfer Example)

## Step 1 — User Action (View)
User clicks **Transfer Money** in React UI.

React sends: React Form → sends HTTP request

```
POST /api/accounts/transfer
```

---

## Step 2 — Controller (Spring Boot)
`AccountController` receives request:
- Validates DTO
- Verifies JWT authentication
- Calls service

---

## Step 3 — Service (Business Logic)
TransferService performs:
1. Fetch accounts from DB
2. Balance validation / Check balance
3. Debit & credit
4. Insert transaction record / Create transaction record
5. Write audit log
6. Send email notification

---

## Step 4 — Model (Repository + Database)
Repositories interact with DB:

```
AccountRepository → SELECT account
TransactionRepository → INSERT transaction
AuditRepository → INSERT audit log
```

-Transactional safety ensured using `@Transactional`.
-👉 Ensures ACID banking safety

---

## Step 5 — Response (View)
Controller returns JSON response.
React updates UI.

---

# 4. Security in MVC

- Spring Security + JWT
- Security acts as a cross‑cutting concern.

Flow:
1. React sends JWT token
2. Security filter validates user
3. Controller executes

---

- So security runs before Controller

# 5. AOP Exception Handling

If this project uses AOP for exception handling.
Instead of try‑catch blocks everywhere:

```java
@ExceptionHandler(AccountNotFoundException.class)
```

- AOP intercepts controller and returns standardized error response.

---

# 6. Complete Architecture Diagram

```
React UI (View)
      ↓ HTTP
Spring Controller (Controller)
      ↓
Service Layer (Business Rules)
      ↓
Repository (Model)
      ↓
Database
```

Cross‑Cutting Concerns:
- Spring Security + JWT
- Logging & Auditing
- AOP Exception Handler
- Caching (Redis)
- Monitoring
- Email Notification

---

# 7. 30‑Second Interview Answer

- The application follows MVC architecture where React acts as the View layer providing UI screens.
- Spring Boot Controllers act as the Controller layer handling REST requests.
- The Model layer consists of JPA Entities, Repositories, and database tables storing accounts and transactions.
- When a user performs a fund transfer, the request flows from React → Controller → Service → Repository → Database, and the response returns as JSON to update UI.
- Security, logging, and exception handling are implemented as cross-cutting concerns using Spring Security and AOP.

-----


* __GUI Applications__ - GUI frameworks often utilize MVC to separate the graphical interface (view) from the application logic (controller) and data model.

* __Game Development__ - In game development, MVC can be applied to separate game state management (model) from rendering (view) and player input (controller).

* ![image](https://github.com/user-attachments/assets/07d6d4d7-d1c7-4fd3-a2e1-d232627ae5af)





------------------------------------------------------------



## Layered Architecture:

* __Enterprise Applications__ - Layered architecture is commonly used in enterprise applications to separate presentation layer, business logic layer, and data access layer, facilitating modularity and maintainability.

* __Web Services__ - Web services often adopt a layered architecture with separate layers for handling HTTP requests, processing business logic, and accessing databases or external services.

* __Embedded Systems__ - Layered architecture can be applied in embedded systems to separate device drivers, application logic, and user interfaces, promoting scalability and reusability.

![image](https://github.com/user-attachments/assets/6039d842-89a4-45df-91e9-9b971202422e)


## Service-Oriented Architecture (SOA):

* __Distributed Systems__ - SOA is used in distributed systems to design applications as a collection of loosely coupled services that communicate over a network, enabling interoperability and flexibility.

* __Cloud Computing__ - Cloud-based applications often adopt SOA to leverage cloud services and APIs, allowing components to be developed and deployed independently.

* __Microservices__ - SOA principles are applied in microservices architecture to build and deploy small, independent services that can be developed, tested, and scaled individually.

* ![image](https://github.com/user-attachments/assets/5c8c3298-b95a-49e3-b2aa-0e753ec50747)




## Event-Driven Architecture (EDA):

* __User Interfaces__ - EDA is commonly used in user interfaces to handle user interactions (events) asynchronously, allowing components to react to events and update the UI dynamically.

* __Messaging Systems__ - Messaging systems utilize EDA to propagate messages (events) between components, enabling decoupling and scalability.

* __Real-time Systems__ - EDA is applied in real-time systems (e.g., financial trading platforms, gaming servers) to process events and react within strict time constraints.

* ![image](https://github.com/user-attachments/assets/2228adf4-4284-42d8-8fda-c6189f780b1b)




## Microservices Architecture:

* __E-commerce Platforms__ - Microservices architecture is used in e-commerce platforms to build scalable and resilient systems composed of small, independent services (e.g., product catalog, payment processing, user authentication).

* __Content Management Systems__ - Content management systems can benefit from microservices architecture by separating content creation, storage, and presentation into individual services.

* __Social Media Platforms__ - Social media platforms leverage microservices architecture to handle various functionalities such as user profiles, news feeds, messaging, and analytics as separate services.



## Domain-Driven Design (DDD):

* __Financial Systems__ - DDD is applied in financial systems to model complex domain concepts (e.g., accounts, transactions, portfolios) and align software design with business requirements.

* __Healthcare Applications__ - Healthcare applications can benefit from DDD by modeling domain entities (e.g., patients, medical records, treatments) and defining domain-specific business rules and workflows.

* __Supply Chain Management__ - DDD is used in supply chain management systems to model the domain entities (e.g., products, orders, suppliers) and encapsulate domain logic within the domain layer.


## Hexagonal Architecture (Ports and Adapters):

* __Web Applications__ - Hexagonal architecture is used in web applications to separate core business logic from external concerns (e.g., HTTP requests, database access), facilitating testability and maintainability.
 
* __Internet of Things (IoT) Devices__ - IoT devices can benefit from hexagonal architecture by isolating device-specific functionality (e.g., sensor data processing, communication protocols) from the application logic.

* __Financial Trading Systems__ - Hexagonal architecture is applied in financial trading systems to separate trading algorithms and strategies from market data feeds and execution platforms.


## Component-Based Architecture:
* __Gaming Engines__ - Gaming engines often utilize component-based architecture to represent game entities (e.g., characters, objects, environments) as reusable components that can be composed and configured dynamically.
  
* __Enterprise Resource Planning (ERP) Systems__ - ERP systems can benefit from component-based architecture by building modular components (e.g., inventory management, human resources, accounting) that can be integrated and customized.
  
* __Multimedia Applications__ - Multimedia applications (e.g., audio/video editing software, image processing tools) leverage component-based architecture to build reusable components for processing and manipulating multimedia data.


## Pipes and Filters Architecture:
* __Data Processing Pipelines__ - Pipes and filters architecture is used in data processing pipelines to transform and process data through a series of interconnected filters (e.g., data validation, normalization, enrichment).
  
* __Compiler Design__ - Compiler architectures often adopt pipes and filters architecture to parse, analyze, and transform source code through a sequence of lexical, syntactic, and semantic analysis stages.

* __Industrial Automation__ - Pipes and filters architecture is applied in industrial automation systems to process and filter sensor data streams, detect anomalies, and trigger control actions.

  

## Repository Pattern:
* __Database Abstraction Layer__ - Repository pattern is commonly used as a database abstraction layer to encapsulate database access logic and provide a clean and consistent interface for data manipulation.
  
* __File Management Systems__ - Repository pattern can be applied in file management systems to abstract file system operations (e.g., reading, writing, deleting files) and provide a unified interface for interacting with files and directories.
  
* __Caching Layers__ - Repository pattern is used in caching layers to abstract data retrieval and caching strategies, allowing applications to transparently cache data from different sources (e.g., databases, web services) and improve performance.
