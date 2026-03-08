## What is Azure CLI?

Azure CLI (az) is a cross-platform command line tool used to manage Azure resources from terminal (Linux, macOS, Windows).

__👉 Alternative to:__

- Azure Portal (GUI)
- PowerShell
- REST API

__Key Point (Interview):__
- Azure CLI is mainly used for automation, DevOps pipelines, scripting and remote server management.


----------------------------------------------------------------------------------------------

# Azure CLI Commands — One-Line Interview Answers

## Account & Login
- `az version` → Shows installed Azure CLI version and dependency details.
- `az login` → Authenticates user to Azure account via browser/device login.
- `az account list -o table` → Lists all subscriptions in a readable table format.
- `az account set --subscription "Azure-subscription-1"` → Sets the active subscription for subsequent commands.
- `az account show` → Displays current active subscription and tenant details.

---

## Resource Group
- `az group create --name Todo-Webapp-prod-rg --location centralindia` → Creates a logical container to organize all Azure resources in a region.
- `az group list -o table` → Lists all resource groups in the subscription.
- `az group delete --name Todo-Webapp-prod-rg` → Deletes the resource group and all contained resources.

---

## Networking
- `az network vnet create --resource-group Todo-Webapp-prod-rg --name todo-vnet --subnet-name todo-subnet` → Creates a virtual network and subnet for private communication between resources.
- `az network vnet list -o table` → Lists all virtual networks.
- `az network public-ip create --resource-group Todo-Webapp-prod-rg --name todo-ip` → Creates a public IP address.
- `az network nsg create --resource-group Todo-Webapp-prod-rg --name todo-nsg` → Creates a Network Security Group (firewall rules).
- `az network nsg rule create --resource-group Todo-Webapp-prod-rg --nsg-name todo-nsg --name AllowSSH --protocol Tcp --priority 1000 --destination-port-range 22 --access Allow` → Opens SSH port 22.

---

## Storage
- `az storage account create --name todostorageprod12345 --resource-group Todo-Webapp-prod-rg --location centralindia --sku Standard_LRS` → Creates a storage account for blobs/files/queues with locally redundant storage.
- `az storage account list -o table` → Lists storage accounts.
- `az storage container create --name uploads --account-name todostorageprod12345` → Creates a blob container inside storage account.
- `az storage blob upload --account-name todostorageprod12345 --container-name uploads --name file.txt --file file.txt` → Uploads file to blob storage.

---

## Database (Azure SQL)
- `az sql server create --name todo-sql-server-prod --resource-group Todo-Webapp-prod-rg --location centralindia --admin-user sqladmin --admin-password StrongPass@123` → Creates a logical SQL Server instance to host databases.
- `az sql db create --resource-group Todo-Webapp-prod-rg --server todo-sql-server-prod --name todo-db --service-objective S0` → Creates a SQL database with S0 performance tier.
- `az sql db list --server todo-sql-server-prod -o table` → Lists databases inside SQL server.
- `az sql server firewall-rule create --resource-group Todo-Webapp-prod-rg --server todo-sql-server-prod --name AllowAzure --start-ip-address 0.0.0.0 --end-ip-address 0.0.0.0` → Allows Azure services to access SQL Server through firewall.

---

## Virtual Machine (Backend API)
- `az vm create --resource-group Todo-Webapp-prod-rg --name todo-backend-vm --image Ubuntu2204 --admin-username azureuser --generate-ssh-keys --vnet-name todo-vnet --subnet todo-subnet` → Creates Linux VM inside VNet with SSH access.
- `az vm list -o table` → Lists all virtual machines.
- `az vm start --name todo-backend-vm --resource-group Todo-Webapp-prod-rg` → Starts the VM.
- `az vm stop --name todo-backend-vm --resource-group Todo-Webapp-prod-rg` → Stops the VM.
- `az vm restart --name todo-backend-vm --resource-group Todo-Webapp-prod-rg` → Restarts the VM.
- `az vm deallocate --name todo-backend-vm --resource-group Todo-Webapp-prod-rg` → Stops VM and releases billing compute charges.
- `az vm delete --name todo-backend-vm --resource-group Todo-Webapp-prod-rg` → Deletes the virtual machine.
- `az vm open-port --port 8080 --resource-group Todo-Webapp-prod-rg --name todo-backend-vm` → Opens application port in VM firewall.
- `az vm run-command invoke --command-id RunShellScript --name todo-backend-vm --resource-group Todo-Webapp-prod-rg --scripts "sudo apt update"` → Executes remote command inside VM.
- `az vm show --name todo-backend-vm --resource-group Todo-Webapp-prod-rg -d -o table` → Shows VM public IP and status.

---

## App Service (Web App Hosting)
- `az appservice plan create --name todo-backend-plan --resource-group Todo-Webapp-prod-rg --sku B1 --is-linux` → Creates Linux App Service hosting plan.
- `az webapp create --resource-group Todo-Webapp-prod-rg --plan todo-backend-plan --name todo-backend-api-12345 --runtime "JAVA|17-java17"` → Creates Java 17 web application.
- `az webapp list -o table` → Lists all web apps.
- `az webapp restart --name todo-backend-api-12345 --resource-group Todo-Webapp-prod-rg` → Restarts the web app.

---

## Application Configuration
- `az webapp config appsettings set --resource-group Todo-Webapp-prod-rg --name todo-backend-api-12345 --settings WEBSITES_PORT=8080` → Sets application listening port.
- `az webapp config appsettings set ... SPRING_DATASOURCE_URL/USERNAME/PASSWORD` → Adds environment variables for database connection.
- `az webapp config appsettings list --name todo-backend-api-12345 --resource-group Todo-Webapp-prod-rg` → Lists all app settings.

---

## Logs & Monitoring
- `az webapp log tail --name todo-backend-api-12345 --resource-group Todo-Webapp-prod-rg` → Streams live application logs.
- `az monitor metrics list --resource todo-backend-api-12345 --metric CpuPercentage` → Shows CPU usage metrics.
- `az monitor activity-log list --resource-group Todo-Webapp-prod-rg` → Shows audit activity logs.

---

## Deployment
- `az webapp deploy --resource-group Todo-Webapp-prod-rg --name todo-backend-api-12345 --src-path target/todo-0.0.1-SNAPSHOT.jar --type jar` → Deploys Spring Boot JAR file to Azure web app.
- `az webapp up --name todo-backend-api-quickstart --runtime "JAVA:17"` → Quickly creates and deploys a web app in one command.

----------------------------------------------------------------------

## Why Azure CLI used in DevOps?

- CMD line Automation script recipes
- Infrastructure as Code (IAC)
- GitLab and github CI/CD pipelines
- Docker/Kubernetes deployments
- Remote server management


## What Azure WebApp service Automatically Handles (Important to Say in Interview)

When backend runs on App Service, Azure provides:

- 1) `Auto Scaling` - Automatically adds instances when traffic increases.
- 2) `Load Balancer` - No nginx or HAProxy setup required.
- 3) `Free SSL Certificate` -https://yourapi.azurewebsites.net
- 4) `Process Monitoring (Auto-Heal)` - If Spring Boot crashes → Azure restarts it.
- 5) `Logging & Monitoring` - Application logs
    - HTTP logs
    - Metrics
    - Live
    - log
    - stream

- 6) `Zero-Downtime Deployment` - New version deploy → old version stays running until ready.


## What You Must Do on VM (Pain Points)

If backend is on VM, you must: manual server administration.

```json
Install Java
Install Maven
Configure firewall
Setup reverse proxy
Setup HTTPS
Setup auto restart (systemd)
Setup logging
Setup scaling
Setup load balancer
Handle OS updates
```

- __`VM`__ = __`You manage server`__
- __`App Service`__ = __`Azure manages server`__

👉 That’s why companies avoid VMs for web apps.

## Interview Answer (Perfect)

- I had deployed the Spring Boot backend on Azure App Service instead of a Virtual Machine because App Service is a PaaS offering. Azure automatically manages runtime, scaling, SSL, monitoring and crash recovery.
- This reduces operational overhead and supports CI/CD pipelines, whereas a VM would require manual server administration.

## Then When VM is Actually Used (Trick Question) ?

Use VM only when:

- Custom OS needed
- Special drivers required
- Legacy monolith apps
- Low-level network control needed
- Not for typical REST APIs.


------------------------------------------------------------------------------------------------------------

## Install Azure CLI (Linux – Ubuntu):

```bash
$ curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash



// OR Manually :

sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates curl gnupg lsb-release

sudo mkdir -p /etc/apt/keyrings
curl -sLS https://packages.microsoft.com/keys/microsoft.asc |
  gpg --dearmor | sudo tee /etc/apt/keyrings/microsoft.gpg > /dev/null
sudo chmod go+r /etc/apt/keyrings/microsoft.gpg

AZ_DIST=$(lsb_release -cs)
echo "Types: deb
URIs: https://packages.microsoft.com/repos/azure-cli/
Suites: ${AZ_DIST}
Components: main
Architectures: $(dpkg --print-architecture)
Signed-by: /etc/apt/keyrings/microsoft.gpg" | sudo tee /etc/apt/sources.list.d/azure-cli.sources

sudo apt-get update
sudo apt-get install azure-cli
```

## Check installation: or Version check:
```json
$ az version

//output:
{
  "azure-cli": "2.83.0",
  "azure-cli-core": "2.83.0",
  "azure-cli-telemetry": "1.1.0",
  "extensions": {}
}


$ az --version

//output:

azure-cli                         2.83.0
core                              2.83.0
telemetry                          1.1.0

Dependencies:
msal                            1.35.0b1
azure-mgmt-resource               23.3.0

Python location '/opt/az/bin/python3'
Config directory '/lhome/azahask/.azure'
Extensions directory '/lhome/azahask/.azure/cliextensions'

Python (Linux) 3.13.11 (main, Jan 27 2026, 07:21:51) [GCC 11.4.0]

Legal docs and information: aka.ms/AzureCliLegal


Your CLI is up-to-date

```

## 3) Login to Azure
```json
$ az login
```
➡ Opens browser → login → returns subscription list

```json
[
  {
    "cloudName": "AzureCloud",
    "tenantId": "4f2a-xxxx-xxxx",
    "id": "1234-5678-9012",
    "isDefault": true,
    "name": "Pay-As-You-Go",
    "state": "Enabled",
    "user": {
      "name": "user@gmail.com",
      "type": "user"
    }
  }
]
```

## Login from Server:
```json
$ az login --use-device-code

To sign in, use a web browser to open the page https://microsoft.com/devicelogin and enter the code I7DBYCUC9 to authenticate.

```
- ➡ Opens browser ➡ Open __https://microsoft.com/devicelogin__ , provide credntial
- <img width="1425" height="786" alt="image" src="https://github.com/user-attachments/assets/c55b61c4-fb9a-45c0-930d-d6b5494965a8" />


## Account & Subscription

### List subscriptions
```json
$ az account list -o table

Output:

Name             CloudName    State    IsDefault
---------------  ----------   ------   ---------
Pay-As-You-Go    AzureCloud   Enabled  True
Azure-subscription-1  AzureCloud   d8489a1f-c93d-42ee-8068-72ae05f9915b  049c681e-8862-4679-80f0-02ec174c200b  Enabled  True

```

## Set subscription
```json
$ az account set --subscription "Azure-subscription-1"
```

## SHow Login Account details:
```json
$ az account show

//Output:
{
  "environmentName": "AzureCloud",
  "homeTenantId": "049c681e-8862-4679-80f0-02ec174c200b",
  "id": "d8489a1f-c93d-42ee-8068-72ae05f9915b",
  "isDefault": true,
  "managedByTenants": [],
  "name": "Azure-subscription-1",
  "state": "Enabled",
  "tenantDefaultDomain": "azaharsk2025gmail.onmicrosoft.com",
  "tenantDisplayName": "Default Directory",
  "tenantId": "049c681e-8862-4679-80f0-02ec174c200b",
  "user": {
    "name": "azahar.sk.2025@gmail.com",
    "type": "user"
  }
}
```

## Where used (Interview Tip):
-  Azure CLI commands are Used inside VM, SSH, CI/CD servers.



## What is a Resource Group in Azure?

_ A Resource Group in Microsoft Azure is a logical container (Grouping of releated resources) that holds related cloud resources such as:

- Virtual Machines
- Storage Accounts
- Databases
- Web Apps
- Networking components

- A resource group is used to manage, monitor, and deploy related Azure resources together as a single unit.
- Instead of managing 50 resources separately, you manage them together.


__Key Benefits of using Resource Group:__

- Lifecycle management (create/delete together) for example- Deleting a Resource Group deletes ALL resources inside it.
- Access control (RBAC permissions)
- Billing grouping
- Easy automation & deployment
- Environment separation (Dev / Test / Prod)

<img width="1769" height="973" alt="image" src="https://github.com/user-attachments/assets/82fa42bb-455f-43cd-bf4d-09a0c95a50b1" />


## 1️⃣ Create Resource Group:

```json
$ az group create \
  --name Todo-Webapp-prod-rg \
  --location centralindia


// Output:
{
  "id": "/subscriptions/d8489a1f-c93d-42ee-8068-72ae05f9915b/resourceGroups/Todo-Webapp-prod-rg",
  "location": "centralindia",
  "managedBy": null,
  "name": "Todo-Webapp-prod-rg",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null,
  "type": "Microsoft.Resources/resourceGroups"
}

```

<img width="944" height="387" alt="image" src="https://github.com/user-attachments/assets/77282828-6071-4160-baae-4ec7519cabcb" />





## 3️⃣ Create Virtual Network (Networking First)

```json
$ az network vnet create \
  --resource-group Todo-Webapp-prod-rg \
  --name todo-vnet \
  --subnet-name todo-subnet

// Output:
{
  "newVNet": {
    "name": "todo-vnet",
    "subnets": [
      { "name": "todo-subnet" }
    ]
  }
}


```

## 4️⃣ Create Storage Account (Images):

```json
az storage account create \
  --name todostorageprod12345 \
  --resource-group Todo-Webapp-prod-rg \
  --location centralindia \
  --sku Standard_LRS


//Output:

{
  "accessTier": "Hot",
  "allowBlobPublicAccess": false,
  "creationTime": "2026-02-19T08:41:22.123456+00:00",
  "enableHttpsTrafficOnly": true,
  "id": "/subscriptions/1a2b3c4d-xxxx-xxxx/resourceGroups/Todo-Webapp-prod-rg/providers/Microsoft.Storage/storageAccounts/todostorageprod12345",
  "kind": "StorageV2",
  "location": "centralindia",
  "minimumTlsVersion": "TLS1_2",
  "name": "todostorageprod12345",
  "primaryEndpoints": {
    "blob": "https://todostorageprod12345.blob.core.windows.net/",
    "dfs": "https://todostorageprod12345.dfs.core.windows.net/",
    "file": "https://todostorageprod12345.file.core.windows.net/",
    "queue": "https://todostorageprod12345.queue.core.windows.net/",
    "table": "https://todostorageprod12345.table.core.windows.net/"
  },
  "primaryLocation": "centralindia",
  "provisioningState": "Succeeded",
  "resourceGroup": "Todo-Webapp-prod-rg",
  "sku": {
    "name": "Standard_LRS",
    "tier": "Standard"
  },
  "statusOfPrimary": "available",
  "type": "Microsoft.Storage/storageAccounts"
}

```

<img width="942" height="555" alt="image" src="https://github.com/user-attachments/assets/d4f0ce21-eb2c-4412-9606-96ffe8f38497" />

## 5️⃣ Create SQL Database (Store Data):

### Create SQL Server

```json
$ az sql server create \
  --name todo-sql-server-prod \
  --resource-group Todo-Webapp-prod-rg \
  --location centralindia \
  --admin-user sqladmin \
  --admin-password StrongPass@123

{
  "administratorLogin": "sqladmin",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "todo-sql-server-prod.database.windows.net",
  "id": "/subscriptions/xxxx/resourceGroups/Todo-Webapp-prod-rg/providers/Microsoft.Sql/servers/todo-sql-server-prod",
  "kind": "v12.0",
  "location": "centralindia",
  "name": "todo-sql-server-prod",
  "publicNetworkAccess": "Enabled",
  "resourceGroup": "Todo-Webapp-prod-rg",
  "state": "Ready",
  "type": "Microsoft.Sql/servers",
  "version": "12.0"
}


```

<img width="859" height="402" alt="image" src="https://github.com/user-attachments/assets/e1240e30-7c9f-4dd0-92b3-92aad8fa78a8" />

### Create Database

```json

$ az sql db create \
  --resource-group Todo-Webapp-prod-rg \
  --server todo-sql-server-prod \
  --name todo-db \
  --service-objective S0


// Sample Output:

{
  "collation": "SQL_Latin1_General_CP1_CI_AS",
  "creationDate": "2026-02-19T09:02:11.45Z",
  "currentServiceObjectiveName": "S0",
  "databaseId": "c7c6c2e5-xxxx-xxxx",
  "defaultSecondaryLocation": null,
  "earliestRestoreDate": "2026-02-19T09:12:11.45Z",
  "id": "/subscriptions/xxxx/resourceGroups/Todo-Webapp-prod-rg/providers/Microsoft.Sql/servers/todo-sql-server-prod/databases/todo-db",
  "location": "centralindia",
  "maxSizeBytes": 268435456000,
  "name": "todo-db",
  "requestedServiceObjectiveName": "S0",
  "resourceGroup": "Todo-Webapp-prod-rg",
  "status": "Online",
  "type": "Microsoft.Sql/servers/databases"
}

```

<img width="900" height="282" alt="image" src="https://github.com/user-attachments/assets/bde3f8fe-0398-44e5-b7b7-5c02a877ddba" />



__⭐ Interview One-Line Answer:__

- First I created a logical SQL Server which acts as a database host.
- Then I created a database inside that server using S0 pricing tier.
- The application connects using the fully qualified domain name and SQL authentication.


## 6️⃣ Create Backend VM (APIs):

```json
Create Backend VM (APIs)
az vm create \
  --resource-group Todo-Webapp-prod-rg \
  --name todo-backend-vm \
  --image Ubuntu2204 \
  --admin-username azureuser \
  --generate-ssh-keys \
  --vnet-name todo-vnet \
  --subnet todo-subnet

// Sample Output:

{
  "fqdns": "",
  "id": "/subscriptions/xxxx/resourceGroups/Todo-Webapp-prod-rg/providers/Microsoft.Compute/virtualMachines/todo-backend-vm",
  "location": "centralindia",
  "macAddress": "00-0D-3A-B1-2C-55",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "20.204.75.118",
  "resourceGroup": "Todo-Webapp-prod-rg",
  "zones": ""
}

```

- __After creation:__ `publicIpAddress:` 20.xx.xx.xx
- __Connect:__ ssh azureuser@20.xx.xx.xx


<img width="992" height="310" alt="image" src="https://github.com/user-attachments/assets/16a7717a-d570-4606-8914-73a30bf5b487" />


__⭐ Interview One-Line Answer:__

- I created an Ubuntu VM inside the application virtual network and subnet.
- Azure automatically provisioned networking, public IP and SSH keys.
- The backend REST APIs run inside this VM and communicate privately with database and storage using the private IP.


__When you run az vm create, Azure also automatically creates:__

- Network Interface (NIC)
- Public IP
- Network Security Group (NSG)
- OS Disk
- SSH Keys (in ~/.ssh)


-------------------------------------------------------------------------------------------

##  Perfect — now you have infra ready 🎯
Let’s deploy:

- __`Frontend:`__ React (Static site → App Service)
- __`Backend:`__ Spring Boot (Java → App Service or VM)

e.g- 

```json
User Browser
     ↓
React Frontend (Azure Web App)
     ↓ REST API
Spring Boot Backend (Azure Web App OR VM)
     ↓
Azure SQL Database
```

## 1️⃣ Deploy Backend — Spring Boot API (Java) in Azure WebApp service

### __Step 1: Build the JAR:__
- Inside your Spring Boot project:

```bash
mvn clean package

// Output: target/todo-0.0.1-SNAPSHOT.jar
```

### Step 2: Create Backend App Service Plan:
```json
$ az appservice plan create \
  --name todo-backend-plan \
  --resource-group Todo-Webapp-prod-rg \
  --sku B1 \
  --is-linux


// Sample Output:

{
  "id": "/subscriptions/xxxxxxxx/resourceGroups/Todo-Webapp-prod-rg/providers/Microsoft.Web/serverfarms/todo-backend-plan",
  "name": "todo-backend-plan",
  "type": "Microsoft.Web/serverfarms",
  "location": "Central India",
  "kind": "linux",
  "reserved": true,
  "status": "Ready",

  "sku": {
    "name": "B1",
    "tier": "Basic",
    "size": "B1",
    "capacity": 1
  },

  "numberOfWorkers": 1,
  "maximumNumberOfWorkers": 3,

  "perSiteScaling": false,
  "isSpot": false,
  "hyperV": false,

  "hostingEnvironmentProfile": null,

  "workerTierName": null,
  "targetWorkerCount": 0,
  "targetWorkerSizeId": 0
}
```

- It creates an App Service Plan — the compute container that hosts your web apps, You can deploy multiple apps into one plan.
- `App Service Plan` = `Server (CPU + RAM)`
- `Web App` = `Application running inside the server`

<img width="946" height="641" alt="image" src="https://github.com/user-attachments/assets/0b0793e1-b93f-4e77-9976-10bf70c6576a" />

### Step 3: Create Backend Web App:
- Creates a Web App container where your Java backend will run.

```json

$ az webapp create \
  --resource-group Todo-Webapp-prod-rg \
  --plan todo-backend-plan \
  --name todo-backend-api-12345 \
  --runtime "JAVA|17-java17"

// Sample Output:

{
  "id": "/subscriptions/xxxx/resourceGroups/Todo-Webapp-prod-rg/providers/Microsoft.Web/sites/todo-backend-api-12345",
  "name": "todo-backend-api-12345",
  "type": "Microsoft.Web/sites",
  "kind": "app,linux",
  "location": "Central India",
  "state": "Running",

  "defaultHostName": "todo-backend-api-12345.azurewebsites.net",
  "httpsOnly": false,

  "serverFarmId": "/subscriptions/xxxx/resourceGroups/Todo-Webapp-prod-rg/providers/Microsoft.Web/serverfarms/todo-backend-plan",

  "siteConfig": {
    "linuxFxVersion": "JAVA|17-java17",
    "alwaysOn": false
  },

  "reserved": true,
  "enabled": true
}

```
- After deployment, Public URL Generated: https://todo-backend-api-12345.azurewebsites.net
- your API will be available like: https://todo-backend-api-12345.azurewebsites.net/api/todos

```
Resource Group
   └── App Service Plan (todo-backend-plan)
           └── Web App (todo-backend-api-12345)
```

### Step 4: Configure Reverse proxy & Spring Boot Port

- `Why Needed :` - Azure App Service does NOT directly expose your Java app to internet and Spring Boot runs on 8080 (HTTP web traffic Testing port)
- isntead
```
Internet
   ↓
Azure Front-End Load Balancer
   ↓
Reverse Proxy (nginx inside App Service)
   ↓
Your Spring Boot Application

```
SO Configure above
```json

$ az webapp config appsettings set \
  --resource-group Todo-Webapp-prod-rg \
  --name todo-backend-api-12345 \
  --settings WEBSITES_PORT=8080

//Sample Output:
[
  {
    "name": "WEBSITES_PORT",
    "slotSetting": false,
    "value": "8080"
  }
]

```
-  App must listen on the port Azure assigns, instead
-  Azure proxy forwards traffic like: https://todo-backend-api-12345.azurewebsites.net HTTP Port 80 ---------to---------> Internal Testing PORT:8080
- "My application listens on port 8080 — route traffic there."


###  Alternative Way to set PORT (Better Production Approach)

- Instead of forcing 8080, let Azure decide: Add in application.properties
```
server.port=${PORT:8080}
```

Now:

- Locally → runs on 8080
- Azure → runs on Azure provided PORT automatically


### Step 5: Add Database Connection:

- First-of-all , You should not hardcode/ put password in application.properties in Todo project sourcecod below like

```
spring.datasource.url=jdbc:sqlserver://todo-sql-server-prod.database.windows.net:1433;database=todo-db
spring.datasource.username=sqladmin
spring.datasource.password=StrongPass@123
```
__Problems:__
- Password committed to GitHub ❌
- Anyone cloning repo gets DB access ❌
- You must rebuild app for password change ❌
- Violates DevOps & security compliance ❌

__Correct Production Way__
```json
az webapp config appsettings set \
  --resource-group Todo-Webapp-prod-rg \
  --name todo-backend-api-12345 \
  --settings \
SPRING_DATASOURCE_URL="jdbc:sqlserver://todo-sql-server-prod.database.windows.net:1433;database=todo-db" \
SPRING_DATASOURCE_USERNAME="sqladmin" \
SPRING_DATASOURCE_PASSWORD="StrongPass@123"

```

OR

__USe App Settings environment variables:__ Azure injects values as environment variables into your running Java process.

- Spring Boot automatically maps below, So your app reads them without properties file.

```
SPRING_DATASOURCE_URL → spring.datasource.url
SPRING_DATASOURCE_USERNAME → spring.datasource.username
SPRING_DATASOURCE_PASSWORD → spring.datasource.password
```

Or

__Even Better :Industry Standard `Use Azure Key Vault` (never store password in app settings either)__

- Flow:
```json
Spring Boot → Managed Identity → Key Vault → SQL Password
```
- No password visible anywhere.

### Step 6: Create DB Firewall rul:

```json
$ az sql server firewall-rule create \
  --resource-group Todo-Webapp-prod-rg \
  --server todo-sql-server-prod \
  --name AllowAzure \
  --start-ip-address 0.0.0.0 \
  --end-ip-address 0.0.0.0
```


- Otherwise you get:
```
Cannot open server requested by the login
Client with IP address is not allowed
```

### step 7: 

```json
$ az webapp deploy \
  --resource-group Todo-Webapp-prod-rg \
  --name todo-backend-api-12345 \
  --src-path target/todo-0.0.1-SNAPSHOT.jar \
  --type jar


//Sample Output:

{
  "deploymentId": "c4c8a5d1-xxxx-xxxx-xxxx-2f4f3b2f7d1a",
  "status": 4,
  "status_text": "Deployment successful",
  "active": true,
  "received_time": "2026-02-19T09:42:21.231Z",
  "end_time": "2026-02-19T09:43:02.442Z",
  "log_url": "https://todo-backend-api-12345.scm.azurewebsites.net/api/deployments/c4c8a5d1/log"
}

```

- Your JAR is uploaded to the Kudu deployment engine inside Microsoft Azure App Service.

```json
CLI uploads JAR
     ↓
Kudu extracts & configures runtime
     ↓
Java container starts
     ↓
Spring Boot application runs
     ↓
Public HTTPS endpoint becomes active
```

  
### Step 8: Test API After success:
- https://todo-backend-api-12345.azurewebsites.net/api/todos

  
__⭐ Interview One-Line Answer:__

- I deployed the  backend Spring Boot API as separate App Services.
- The frontend communicates with backend via REST API, and backend connects to Azure SQL Database.
- This follows a scalable 3-tier architecture and avoids managing infrastructure manually.


## 2️⃣ Deploy Frontend — React App on Azure WebApp service


### Step 1: Configure Backend URL

- Create `.env` in React:
```ini
REACT_APP_API=https://todo-backend-api-12345.azurewebsites.net
```

### Step 2: Build React
```json
npm install
npm run build

//Output:Creates
build/
```

### Step 3: Create Frontend Web App

```json
$ az webapp create \
  --resource-group Todo-Webapp-prod-rg \
  --plan todo-prod-plan \
  --name todo-frontend-12345 \
  --runtime "NODE|18-lts"
```
### Step 4: Configure Static Site Hosting

```json
$ az webapp config set \
  --resource-group Todo-Webapp-prod-rg \
  --name todo-frontend-12345 \
  --startup-file "pm2 serve /home/site/wwwroot --no-daemon --spa"

```

### Step 5: Deploy React Build
```json
cd build
zip -r app.zip .

az webapp deploy \
  --resource-group Todo-Webapp-prod-rg \
  --name todo-frontend-12345 \
  --src-path app.zip \
  --type zip

```

-------------------------------------------------------------

## 🌍 Final Working URLs:

__`Frontend:`__
```json
https://todo-frontend-12345.azurewebsites.net
```

__`Backend API:`__

```json
https://todo-backend-api-12345.azurewebsites.net/api/todos
```

---------------------------------------------------
```
__⭐ Interview One-Line Answer:__

- I deployed a 3-tier architecture on Azure.
- `az webapp deploy` uploads the built application artifact to Azure App Service and triggers a runtime restart so the new version becomes live without managing infrastructure.
- The React frontend is hosted on App Service, which calls a Spring Boot REST API hosted on another App Service. 
- The backend connects securely to Azure SQL Database for persistence. This design is scalable, stateless and cloud-native, allowing independent scaling of frontend and backend.

