## 🌐 1. Azure App Service (Web Apps) — MAIN HOSTING LAYER:

- `Platform-as-a-Service` to host - No OS level management.

- Azure Web Apps is a PaaS service that allows developers to deploy and run web applications and APIs without managing infrastructure, offering built-in scaling, security, monitoring, and CI/CD integration.
- It comes with pre-installed latest java-runtime eco-system, e.g Preconfigured tomcat , Nginx, Automatic scalling and Automatic load balancer
- Azure automatically provides: OS updates, security patches, JVM installation, all required web server configuration.

__Feature Examples__
- E-commerce site traffic increases → Azure automatically adds instances.
- Traffic automatically distributed across instances (No need for Nginx / HAProxy configuration)
- Monitoring matrics & App service Logging
- Azure automatically provides HTTPS certificate for www.mycompany.com

__Real Use Case:__

```json

Frontend → React/Angular → Azure Web App instance1 → frontend.azurewebsites.net
Backend → Azure Web App (Spring Boot API) instasnce2 → api.azurewebsites.net 

// Supported Language:

- Java Spring Boot
- Node / React
- .NET
- Python 
```

- Users never see servers — only HTTPS endpoints.
- Enterprise Java Application like Banking / ERP system running WAR on Tomcat
- Multiple micro-services : -  deployed independently on azure AppService instance, Instead of buying server or VPS → deploy in minutes

```json

  user-service
  order-service
  payment-service

```

<img width="2000" height="1500" alt="image" src="https://github.com/user-attachments/assets/c332f225-4290-4767-a17f-532020563068" />

<img width="1839" height="1020" alt="image" src="https://github.com/user-attachments/assets/5faa8473-e27a-43bf-9028-baf034b86dc5" />
<img width="1833" height="851" alt="image" src="https://github.com/user-attachments/assets/acf21586-00df-43f0-8130-71545116a037" />
<img width="1858" height="945" alt="image" src="https://github.com/user-attachments/assets/0d437b94-ee09-45ae-9404-5020aa529aaa" />
<img width="1858" height="945" alt="image" src="https://github.com/user-attachments/assets/42f2cc4c-1253-4d21-84c9-6ae99ab43590" />
<img width="1748" height="1095" alt="image" src="https://github.com/user-attachments/assets/bf65cb7d-a352-4498-a916-25f709f4448f" />

### Select App Service Pricing Plan:
<img width="1849" height="1115" alt="image" src="https://github.com/user-attachments/assets/bda6b23c-2d07-41f2-bc50-f6932cd72c3f" />
<img width="1402" height="494" alt="image" src="https://github.com/user-attachments/assets/71c9862a-5ee8-403a-9f43-e8fd401abfe4" />
<img width="1630" height="1092" alt="image" src="https://github.com/user-attachments/assets/98ffaeb9-3ecd-41da-a9a9-cce468a3d62d" />
<img width="1550" height="736" alt="image" src="https://github.com/user-attachments/assets/b4e96141-80d8-4f23-8d55-2165969181d2" />

### Enable Monitoring performance matrices service
<img width="1649" height="1012" alt="image" src="https://github.com/user-attachments/assets/024acae0-e026-4482-b4c5-0f1ca55fcd1b" />

<img width="1856" height="1121" alt="image" src="https://github.com/user-attachments/assets/c041fae9-cea3-4d05-85ac-49764ea95b60" />

### Scalling:
<img width="1813" height="1147" alt="image" src="https://github.com/user-attachments/assets/f73be425-e45c-4682-9224-25809f2de58e" />
<img width="1876" height="1079" alt="image" src="https://github.com/user-attachments/assets/843524e4-e93c-4dfa-b99d-b9893f070db0" />



### Created Webapp services

<img width="1876" height="859" alt="image" src="https://github.com/user-attachments/assets/e077ac61-e697-4e14-81a0-153b314137ea" />
<img width="1824" height="1105" alt="image" src="https://github.com/user-attachments/assets/96ef7c47-eb3e-4199-ab15-0564d3dc4b5a" />



## Open VSCOde in project dir

```json
mkdir Fastapi-demo
cd Fastapi-demo
code .

// Open VSCODE terminal

python3 -m venv venv
source venv/bin/activate

pip install fastapi uvicorn[standard] 
pip freeze > requirements.txt

touch app.py

```
`app.py`

```python
from fastapi import FastAPI
import uvicorn 

app = FastAPI()

@app.get("/")
def home():
    return {"message": "FastAPI running on Azure WebApp 🚀"}

@app.get("/health")
def health():
    return {"status": "healthy"}
```

- Ref: https://github.com/AzaharSK/Fastapi-demo.git

<img width="1778" height="918" alt="image" src="https://github.com/user-attachments/assets/73a6ccae-e74e-4384-8fea-6d3fbb94d7cf" />



```bash
git clone https://github.com/AzaharSK/Fastapi-demo.git

/fastapi-azure/Fastapi-demo$ git status
On branch main
Your branch is up to date with 'origin/main'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	app.py
	requirements.txt

nothing added to commit but untracked files present (use "git add" to track)
(venv) Fastapi-demo$ 
(venv) Fastapi-demo$ git add .
(venv) Fastapi-demo$ git commit -m "added app & dependecies"
[main 8092529] added app & dependecies
 2 files changed, 24 insertions(+)
 create mode 100644 app.py
 create mode 100644 requirements.txt

Fastapi-demo$ git push 
Username for 'https://github.com': AzaharSK
Password for 'https://AzaharSK@github.com': 
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 32 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 657 bytes | 657.00 KiB/s, done.
Total 4 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/AzaharSK/Fastapi-demo.git
   8240749..8092529  main -> main

```

## Run Localy First:
<img width="1811" height="983" alt="image" src="https://github.com/user-attachments/assets/147d2683-9424-4642-bb40-0c37128c1fba" />
<img width="1796" height="193" alt="image" src="https://github.com/user-attachments/assets/b2802787-0f48-4b66-9781-26af36634c6b" />


## Deploy it in Azure Web App service using github repo:
<img width="1841" height="519" alt="image" src="https://github.com/user-attachments/assets/1b3482bc-5b07-4f90-80d8-9dd6ee2e7c76" />
<img width="1677" height="1070" alt="image" src="https://github.com/user-attachments/assets/0482a978-17e5-42b3-a17a-61bad8017ddf" />
<img width="1237" height="1105" alt="image" src="https://github.com/user-attachments/assets/9922c3ee-679e-4110-8711-c3a57f9bcd29" />
<img width="1521" height="1139" alt="image" src="https://github.com/user-attachments/assets/b56cb094-dbd5-4cda-a35d-4ae1cf476778" />

<img width="1778" height="918" alt="image" src="https://github.com/user-attachments/assets/53e19bd6-51cf-4cef-96fb-770f064f0127" />
<img width="1542" height="1000" alt="image" src="https://github.com/user-attachments/assets/638a5c7d-f26b-489e-85e6-3e8fa857b683" />

<img width="1604" height="685" alt="image" src="https://github.com/user-attachments/assets/6b4a389e-1684-487d-9335-3873d2e9e2ff" />
<img width="1367" height="1104" alt="image" src="https://github.com/user-attachments/assets/52f9d7d4-8670-4180-b6be-ac464a2386c8" />
<img width="1533" height="1041" alt="image" src="https://github.com/user-attachments/assets/4445888e-5e8d-45ab-ace7-7549e2c4abae" />
<img width="1693" height="1057" alt="image" src="https://github.com/user-attachments/assets/5dd6c8e4-bb9d-4b5f-a84c-3aaa3316c103" />
<img width="1693" height="1057" alt="image" src="https://github.com/user-attachments/assets/b1565332-2d81-4970-95e5-1a19d07f4d25" />

`SAVE`

## USE Python 3.11 (recomanded)
<img width="1352" height="846" alt="image" src="https://github.com/user-attachments/assets/006e8e85-e64c-4c06-92e4-2eaac3478d9f" />


<img width="998" height="333" alt="image" src="https://github.com/user-attachments/assets/0d277503-fc24-492c-8033-ce244325bd10" />

### Use health check
<img width="956" height="822" alt="image" src="https://github.com/user-attachments/assets/7e7579df-e1a3-4734-9757-4127e61a6886" />

<img width="1693" height="1057" alt="image" src="https://github.com/user-attachments/assets/18a838d6-4b5a-468e-b3f9-718e4dae1034" />
<img width="1624" height="776" alt="image" src="https://github.com/user-attachments/assets/5e5b3ae9-aa53-4a3e-8a05-97fe129be7ef" />


`SAVE`
<img width="1233" height="221" alt="image" src="https://github.com/user-attachments/assets/86f3eb43-3805-4b2d-94fb-bca4674fd48c" />


-------------------------------------------------------------

## Local VSCODE deployment
### VS code azure webapp
<img width="1675" height="1134" alt="image" src="https://github.com/user-attachments/assets/8fbb15f8-07b4-4dce-ae23-f702ab1989aa" />
<img width="1693" height="1057" alt="image" src="https://github.com/user-attachments/assets/7d50b881-9c1e-4f2d-8519-529141021ac2" />
<img width="1693" height="1057" alt="image" src="https://github.com/user-attachments/assets/6282aaf2-acdf-450a-ba19-7d8981b4a05e" />


## What is Deployment slot , Production & staging

- In Microsoft Azure App Service, a Deployment Slot is like a separate copy of your web app running inside the same App Service plan — but with its own URL (slightly different then production one), settings, and code version.

Think of it as:
- 👉 Multiple environments (Prod / Test / QA) inside one app.

```json
Users visit → Production version (Live App used by real users)  - URL: https://myapp.azurewebsites.net

Developers use → Staging version (Testing App - Safe testing environment before release) - URL https://myapp-staging.azurewebsites.net

But Both runs simultaneously.

```
- You deploy new code to Staging, test it, then instantly swap with Production.
- After testing:
  
```json
Swap <====> Staging becomes Production

Old Production becomes Staging
```

<img width="1003" height="276" alt="image" src="https://github.com/user-attachments/assets/fa8fb028-7339-43fa-8aeb-e06a4d5abd28" />


### Why slots are powerful ?

- Deployment slots enable zero-downtime deployment and instant rollback in Azure App Service.
- __Without slots:__ `Deploy → App restarts → Users see errors 😱`
- __With slots:__ `Deploy to staging → test → swap → zero downtime 😎`


### What happens during swap

__Azure swaps:__

- code
- containers
- environment variables (optional)
- connection strings (optional)

__But keeps:__

- hostname
- SSL
- traffic

So users never notice deployment.

### Real world example (FastAPI)

__You run a FastAPI API.__
- Deploy new version to staging
- QA tests endpoints
- Click Swap
- New API becomes live instantly

__Rollback ?__
- 👉 Swap again (2 seconds)


## Deployment slots are available for premium plans

<img width="1359" height="723" alt="image" src="https://github.com/user-attachments/assets/0da47a53-53bb-429e-bf80-eacbc473e390" />
<img width="1343" height="733" alt="image" src="https://github.com/user-attachments/assets/2e6d2302-e6f2-4f39-ba02-2653e6c07ead" />
<img width="1693" height="1057" alt="image" src="https://github.com/user-attachments/assets/6ab9616f-99b5-459c-9159-9b63a0cc476f" />
<img width="1900" height="963" alt="image" src="https://github.com/user-attachments/assets/9fb6796b-ad60-4c82-bd67-84873cc1e06f" /> 
<img width="1900" height="963" alt="image" src="https://github.com/user-attachments/assets/d771d641-b7ef-41fa-9a68-a1a55101fcf8" />
<img width="1388" height="805" alt="image" src="https://github.com/user-attachments/assets/d98f515e-29c1-49b5-89a8-e1059d3642ff" />
### Set 50 % Traffic to staging slot for testing

<img width="1920" height="691" alt="image" src="https://github.com/user-attachments/assets/9142e59f-87fb-41d3-aa13-292e8f6b768b" />

## Disable Session Affinity and reload browser to test:
<img width="1900" height="942" alt="image" src="https://github.com/user-attachments/assets/50bf4aa5-e1de-40af-965f-52559b88973a" />

## Swap:
<img width="1392" height="548" alt="image" src="https://github.com/user-attachments/assets/5075cef9-7f10-4885-bc73-5563c711cae0" />
<img width="1900" height="942" alt="image" src="https://github.com/user-attachments/assets/21da3291-5fe9-4cf3-a6ea-1c431c02fbe1" />



## Azure WebApp Environment Variables :

- In Microsoft Azure App Service you never hard-code DB credentials in code.
- You store them as Environment Variables (Application Settings) and read them in your app.
- `App Service → Settings → Environment variables → Application settings → + Add`

  
<img width="1353" height="759" alt="image" src="https://github.com/user-attachments/assets/1ae0f488-d1e8-4765-b4b3-9ea31c3b5ac9" />

```sql
DB_HOST  		myserver.database.windows.net
DB_NAME  		mydb
DB_USER			dbadmin
DB_PASSWORD		********
DB_PORT		1433

```
- Click `Save` → `Restart`
- ⚠️ Passwords here are encrypted automatically by Azure.


### Read them inside FastAPI (Python-dotenv module)
```bash
pip install python-dotenv
```

__config.py__

```python

import os

DB_HOST = os.getenv("DB_HOST")
DB_NAME = os.getenv("DB_NAME")
DB_USER = os.getenv("DB_USER")
DB_PASSWORD = os.getenv("DB_PASSWORD")
DB_PORT = os.getenv("DB_PORT", "1433")

Now use it:

from fastapi import FastAPI
import os

app = FastAPI()

@app.get("/dbinfo")
def dbinfo():
    return {
        "host": os.getenv("DB_HOST"),
        "port": os.getenv("DB_PORT")
    }
```


### Database connection example (PostgreSQL)

```python

import os
from sqlalchemy import create_engine

DATABASE_URL = f"postgresql://{os.getenv('DB_USER')}:{os.getenv('DB_PASSWORD')}@" \
               f"{os.getenv('DB_HOST')}:{os.getenv('DB_PORT')}/{os.getenv('DB_NAME')}"

engine = create_engine(DATABASE_URL)

```

### Local Test  development ( Use .env file)

__Create .env locally:__

```bash

DB_HOST=localhost
DB_NAME=testdb
DB_USER=postgres
DB_PASSWORD=1234
DB_PORT=5432
```

- __Azure ignores .env — but locally it loads.__

### Buy App service domain
<img width="1490" height="767" alt="image" src="https://github.com/user-attachments/assets/2c96954e-4580-4995-a177-cfca0644dca0" />



## Special Azure variables (very important): Azure automatically provides:

```

PORT     			Web server port (must use)
WEBSITE_HOSTNAME  	your public URL
WEBSITE_SITE_NAME   app name

```
At Start-up:
` uvicorn app:app --host 0.0.0.0 --port $PORT `

### Secure way (production best practice)

- Instead of storing password directly → use Azure Key Vault
- Flow: ` App Service → Managed Identity → Key Vault → Secret → App reads secret `
- (No passwords visible in portal)

<img width="1896" height="1058" alt="image" src="https://github.com/user-attachments/assets/e3558dad-2c95-4d62-a494-e7b3d90dc85e" />

<img width="1896" height="1058" alt="image" src="https://github.com/user-attachments/assets/b63eca15-c72b-4e87-ae47-e05d4ce3c930" />


## Interview explanation (short)

- Azure App Service stores sensitive configuration like DB credentials in Application Settings, which are exposed to the runtime as environment variables.
- The application reads them using os.getenv(), enabling secure configuration without hardcoding secrets.


