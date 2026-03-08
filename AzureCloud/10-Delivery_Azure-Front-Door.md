# 🌍 Azure Front Door

---

## 🔹 What is Azure Front Door?

Azure Front Door is a **global Layer 7 (HTTP/HTTPS) load balancer** that provides:

- Global routing
- High availability
- Low latency
- SSL termination
- Web Application Firewall (WAF)
- CDN capabilities

It operates at the **application layer (Layer 7)**.

---

## 🔹 Why Use Azure Front Door?

- 🌍 Distribute traffic globally
- 🚀 Improve performance with edge routing
- 🔄 Automatic failover between regions
- 🔐 Secure applications with WAF
- 📉 Reduce latency using Microsoft global network

---

## 🔹 How It Works

```
User → Nearest Edge POP → Azure Front Door → Best Backend → Response
```

- 1. User request hits nearest Microsoft edge location.
- 2. Azure Front Door evaluates:
   - Health of backend
   - Latency
   - Routing rules
- 3. Routes traffic to the optimal backend.
- 4. If backend fails → automatic failover to healthy region.


---

## 🔹 Key Components

### 1️⃣ Frontend Host
Public endpoint (e.g., `https://myapp.azurefd.net`)

### 2️⃣ Backend Pool
Collection of backend services:
- App Services
- VMs
- AKS
- On-prem APIs

### 3️⃣ Routing Rules
Defines:
- Path-based routing
- Redirect rules
- Header-based routing

### 4️⃣ Health Probes
Continuously checks backend availability.

---

## 🔹 Core Features

### ✅ 1. Global Load Balancing
Routes users to nearest healthy backend.

### ✅ 2. Automatic Failover
If Region A fails → traffic moves to Region B automatically.

### ✅ 3. SSL Offloading
Handles HTTPS at edge.

### ✅ 4. Web Application Firewall (WAF)
Protects against:
- SQL Injection
- XSS
- OWASP Top 10

### ✅ 5. URL-based Routing
Example:
- `/api/*` → API backend
- `/images/*` → Storage backend

### ✅ 6. Session Affinity
Optional sticky sessions.

### ✅ 7. Caching (Optional)
Basic CDN-like caching capability.

---

## 🔹 Azure Front Door vs Azure Load Balancer

| Feature | Front Door | Load Balancer |
|----------|-------------|---------------|
| Layer | L7 (HTTP/HTTPS) | L4 (TCP/UDP) |
| Global | Yes | No (Regional) |
| WAF | Yes | No |
| Path-based routing | Yes | No |

---

## 🔹 Azure Front Door vs Azure CDN

| Feature | Front Door | CDN |
|----------|-------------|-----|
| Global load balancing | Yes | No |
| Dynamic routing | Yes | Limited |
| WAF | Yes | Limited |
| Static content optimization | Moderate | Excellent |

👉 CDN focuses on **static content caching**  
👉 Front Door focuses on **global application routing + security**

---

## 🔹 Azure Front Door vs Azure Application Gateway

| Feature | Front Door | Application Gateway |
|----------|-------------|--------------------|
| Scope | Global | Regional |
| WAF | Yes | Yes |
| Use Case | Multi-region apps | Single-region apps |

---

## 🔹 Real-World Architecture Example

Multi-region deployment:

- App deployed in:
  - East US
  - West Europe
  - Southeast Asia

Azure Front Door:
- Routes US users → East US
- Routes Europe users → West Europe
- If West Europe fails → auto-routes to East US

---

## 🔹 Interview Key Points

- Works at **Layer 7**
- Uses Microsoft global edge network
- Provides **low latency + high availability**
- Supports **automatic failover**
- Can integrate with:
  - Azure App Service
  - AKS
  - VM Scale Sets
- Supports custom domains + managed certificates

---

## 🔹 When to Use Azure Front Door?

Use it when:

- You have multi-region deployment
- You need global failover
- You want WAF at global edge
- You need path-based routing

---

## 🔹 When NOT to Use It?

Avoid if:

- You only have a single regional app
- You just need simple L4 load balancing
- You only need static content acceleration (CDN may be enough)

---

## 🔹 One-Line Interview Definition

> Azure Front Door is a global Layer 7 load balancer that provides intelligent traffic routing, high availability, security, and performance optimization for multi-region web applications.
<img width="1866" height="855" alt="image" src="https://github.com/user-attachments/assets/da5927ae-2853-45f0-b3b5-af646948de2a" />



### WebApp1 deployed @EAST-US
<img width="1869" height="906" alt="image" src="https://github.com/user-attachments/assets/7073816b-446e-41ea-978b-ad2fc65838ee" />
<img width="1891" height="297" alt="image" src="https://github.com/user-attachments/assets/2a2bb68f-ad87-4ba7-9c53-1d1c301628c8" />

### WebApp2 deployed @North-EU
<img width="1896" height="1023" alt="image" src="https://github.com/user-attachments/assets/89dbd8fb-15a6-4054-a9e2-91d688037588" />
<img width="1901" height="258" alt="image" src="https://github.com/user-attachments/assets/f53df4d1-4cf5-4266-9937-aa92b582ee1b" />


### Create Front Door
<img width="1901" height="665" alt="image" src="https://github.com/user-attachments/assets/4fdde78d-b8b0-411f-8ca9-90901281c0e5" />
<img width="1920" height="985" alt="image" src="https://github.com/user-attachments/assets/059d3429-104e-4494-a3ed-45160dc52ee7" />
<img width="1683" height="990" alt="image" src="https://github.com/user-attachments/assets/43d6ea4e-4fee-4bf9-87cc-b1bbee681755" />
<img width="1683" height="990" alt="image" src="https://github.com/user-attachments/assets/904e86a6-e310-4b41-9987-dd3640d328ea" />

### Add Endpoint / DNS
<img width="1920" height="985" alt="image" src="https://github.com/user-attachments/assets/0c062442-05b1-4a3c-ab9d-9b4c2fdf734d" />

### Add route
<img width="1920" height="985" alt="image" src="https://github.com/user-attachments/assets/3ffb5cb0-9a49-4e5e-820d-0d4502c817f5" />

### Add Origin: @EAST-US server URL, and @North-EU URL
<img width="1920" height="985" alt="image" src="https://github.com/user-attachments/assets/998654c5-dab0-4aab-adbf-6a6a605fbfa1" />
<img width="1920" height="985" alt="image" src="https://github.com/user-attachments/assets/8e18c1e4-5fbb-4e21-b6f0-3d0ab013d151" />


### Review + Create
<img width="1920" height="985" alt="image" src="https://github.com/user-attachments/assets/fc25ca50-a8ce-42b2-99b8-c1b7f1df9988" />
<img width="1920" height="985" alt="image" src="https://github.com/user-attachments/assets/3ca09bbf-272e-4cc7-bbf0-95cba6d480fb" />
<img width="1920" height="985" alt="image" src="https://github.com/user-attachments/assets/da25798c-4412-4116-8816-396663293f96" />
<img width="1853" height="456" alt="image" src="https://github.com/user-attachments/assets/302ab9f6-337b-415d-a0fa-b3f220be1895" />

### Test speed: Latency of North-Europe(151ms) faster then WestUS (303ms), as Requested User routed to North-Europe(151ms) as user leaves nearby
<img width="1910" height="1146" alt="image" src="https://github.com/user-attachments/assets/b17e8081-e405-4b3f-81ee-1a5e9e495c21" />
<img width="1910" height="1146" alt="image" src="https://github.com/user-attachments/assets/63a6d672-96ec-4a8b-8d11-b8503e79ebff" />







