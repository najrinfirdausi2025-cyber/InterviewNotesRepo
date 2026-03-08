# 🔹 What is Azure Functions?

Azure Functions is a serverless compute service in Microsoft Microsoft Azure that lets you run event-driven code without managing infrastructure.

👉 You write the code → Azure manages:
- Infrastructure
- Scaling
- Patching
- Runtime

<img width="1583" height="835" alt="image" src="https://github.com/user-attachments/assets/7d54710d-ac6b-42b5-b93c-51139bb514aa" />


### Key Characteristics

- Serverless
- Event-driven
- Auto-scaling
- Pay-per-execution (Consumption plan)
- Multi-language support

---

### Supported Languages

- C# (.NET)
- Java
- Python
- JavaScript (Node.js)
- TypeScript
- PowerShell
- Custom handlers (Go, Rust, etc.)

---

## Core Concepts

### 1. Triggers (How function starts)

A function must have **exactly one trigger**.

Common triggers:

- HTTP Trigger
- Timer Trigger
- Blob Storage Trigger
- Queue Storage Trigger
- Service Bus Trigger
- Event Hub Trigger
- Cosmos DB Trigger

Example:

- Upload file to Blob → Function runs
- Message in Queue → Function runs
- HTTP request → Function runs


### 2. Bindings (Input / Output)

Bindings simplify integration with Azure services.

Types:

- Input Binding
- Output Binding

Example:

- HTTP trigger → Process data → Write to Blob storage (output binding)

No need to manually write SDK boilerplate code.

---

## Hosting Plans

### 1. Consumption Plan

- Fully serverless
- Auto-scale
- Pay per execution
- Cold start possible

Best for:

- Infrequent workloads
- Event-driven APIs

### 2. Premium Plan

- Pre-warmed instances
- No cold start
- VNET support
- Predictable performance

Best for:

- Production APIs
- High-performance workloads


### 3. Dedicated Plan (App Service Plan)

Runs inside Azure App Service.

- Fixed VM cost
- Manual scaling
- Useful if App Service already exists

---

## Scaling Behavior

Azure automatically scales based on:

- Queue length
- Event Hub partitions
- HTTP traffic

Scaling type:

- Horizontal scaling (adds instances)

---

## Execution Timeout

Consumption Plan:

- Default: 5 minutes
- Maximum: 10 minutes

Premium/Dedicated:

- Configurable
- Can be unlimited

---

## Cold Start

Cold start happens when:

- No recent traffic
- Instance deallocated
- New request triggers instance startup

How to reduce:

- Use Premium Plan
- Use pre-warmed instances
- Implement keep-alive pings

---

## Durable Functions

Extension of Azure Functions for:

- Long-running workflows
- State management
- Orchestration
- Fan-out / Fan-in patterns

Common patterns:

- Function chaining
- Parallel execution
- Async HTTP APIs
- Human interaction workflows

---

## Security

Security options:

- Function Keys
- Host Keys
- Azure AD Authentication
- Managed Identity
- IP restrictions

Best practice:

Use **Managed Identity** instead of storing secrets.

---

## Monitoring & Logging

Integrated with:

- Azure Monitor
- Application Insights

You can monitor:

- Execution time
- Failures
- Dependencies
- Live metrics

---

## Deployment Options

- Azure Portal
- Azure CLI
- GitHub Actions
- Azure DevOps
- VS Code
- Zip deployment
- Docker container

---

## Integration with Azure Services

Common integrations:

- Azure Storage
- Azure Service Bus
- Azure Event Hub
- Azure Cosmos DB
- Azure Logic Apps
- Azure API Management

---

## Function App vs Function

### Function App

Container for multiple functions.

Shares:

- Runtime
- Configuration
- Scaling behavior

### Function

Individual execution unit.

---

## Local Development

Tools:

- Azure Functions Core Tools
- VS Code extension

Run locally:

```bash
func start
```

---

## When Should You Use Azure Functions?

Use when:

- Event-driven workloads
- Lightweight APIs
- Background jobs
- Real-time file processing
- IoT event handling
- Microservices glue logic

Avoid when:

- Heavy long-running CPU workloads
- Large monolithic applications

---

## Azure Functions vs Logic Apps

| Feature | Azure Functions | Logic Apps |
|--------|----------------|------------|
| Code-based | Yes | No (Low-code) |
| Developer Control | High | Medium |
| Complex workflows | Durable Functions | Built-in designer |
| Primary use case | Dev-centric | Business automation |

---

## Azure Functions vs Web App

| Feature | Azure Functions | Web App |
|--------|----------------|---------|
| Serverless | Yes | No |
| Event-driven | Yes | Not mandatory |
| Auto-scaling | Automatic | Manual / rule-based |
| Billing | Execution-based | VM-based |

---

## Advanced Interview Topics

You should know:

- Idempotency in event processing
- Retry policies
- Poison queue handling
- Dead-letter queues
- Dependency Injection in .NET Functions
- VNET integration
- Private endpoints
- Deployment slots
- CI/CD best practices

---

## Sample Interview Questions

1. What is cold start and how do you reduce it?
2. Difference between Durable Functions and normal Functions?
3. How does scaling work for Queue trigger?
4. How do you secure an HTTP-triggered function?
5. Difference between Premium and Consumption plans?
6. How do you implement retry logic?
7. How do you debug locally?
8. How do you securely connect to a private database?
