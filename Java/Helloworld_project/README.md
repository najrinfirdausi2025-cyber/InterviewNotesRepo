## This My Hello World Project 
- Ref: https://github.com/in28minutes/deploy-spring-boot-to-azure
  

## Setup Azure CLI:

```bash
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
```bash
$ az --version
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
```


```bash
az login --use-device-code
To sign in, use a web browser to open the page https://microsoft.com/devicelogin and enter the code I7DBYCUC9 to authenticate.

```

<img width="1425" height="786" alt="image" src="https://github.com/user-attachments/assets/9af24a63-ec27-4e5a-9ed9-be66a7cb08f5" />

```bash
az account show
{
  "environmentName": "AzureCloud",
  "homeTenantId": "049c681e-8862-4679-80f0-02ec174c200b",
  "id": "d8489a1f-c93d-42ee-8068-72ae05f9915b",
  "isDefault": true,
  "managedByTenants": [],
  "name": "Azure subscription 1",
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

## Set up Eclipise Development IDE

```bash
sudo snap install eclipse --classic
sudo apt install default-jre
sudo apt install maven
```

```bash
mkdir javaproject
cd javaproject/
~/javaproject$ git clone https://github.com/in28minutes/deploy-spring-boot-to-azure.git
~/javaproject$ cd deploy-spring-boot-to-azure/
~/javaproject/deploy-spring-boot-to-azure$ ls -l
total 44
drwxrwxr-x 3 azahask domainusers  4096 Feb 13 23:27 01-hello-world-rest-api
drwxrwxr-x 3 azahask domainusers  4096 Feb 13 23:27 02-todo-web-application-h2
drwxrwxr-x 3 azahask domainusers  4096 Feb 13 23:27 03-todo-web-application-mysql
drwxrwxr-x 4 azahask domainusers  4096 Feb 13 23:27 04-spring-boot-react-full-stack-h2
drwxrwxr-x 3 azahask domainusers  4096 Feb 13 23:27 05-todo-rest-api-h2-containerized
drwxrwxr-x 4 azahask domainusers  4096 Feb 13 23:27 06-todo-rest-api-mysql-containerized
drwxrwxr-x 3 azahask domainusers  4096 Feb 13 23:27 07-hello-world-rest-api
-rw-rw-r-- 1 azahask domainusers 15849 Feb 13 23:27 README.md
```
# Eclipise --> File --> import ---> maven --> existing maven projects
<img width="1808" height="954" alt="image" src="https://github.com/user-attachments/assets/ccea0b68-0efa-4086-a18f-9c84bdc61f16" />
<img width="1856" height="1146" alt="image" src="https://github.com/user-attachments/assets/3e8d315d-ee4a-495e-9f14-ed6713591d49" />

### __Maven plugin config:__
- groupId: com.microsoft.azure
- artifactId: azure-webapp-maven-plugin
- version: 2.13.0

### __Azure cloud config:__
- resourceGroup: helloworldnajrin-rg
- appName: helloworldnajrin
  
- pricingTier: B1
- region: westeurope
- server.port=80

### __Runtime config:__
- os:  Linux
- javaVersion: 17
- webContainer: Java SE
  
```xml
      <plugin> 
        <groupId>com.microsoft.azure</groupId>  
        <artifactId>azure-webapp-maven-plugin</artifactId>  
        <version>2.13.0</version>
          <configuration>
              <schemaVersion>V2</schemaVersion>
              <resourceGroup>helloworldnajrin-rg</resourceGroup>
              <appName>helloworldnajrin</appName>
              <pricingTier>B1</pricingTier>
              <region>westeurope</region>
              <appSettings>
                  <property>
                      <name>JAVA_OPTS</name>
                      <value>-Dserver.port=80</value>
                  </property>
              </appSettings>
              <runtime>
                  <os>Linux</os>
                  <javaVersion>Java 17</javaVersion>
                  <webContainer>Java SE</webContainer>
              </runtime>
              <deployment>
                  <resources>
                      <resource>
                          <directory>${project.basedir}/target</directory>
                          <includes>
                              <include>*.jar</include>
                          </includes>
                      </resource>
                  </resources>
              </deployment>
          </configuration>
      </plugin>
```

## By default spring does not add swagger API docs , you need to enable it
- Modern Springdoc — recommended - Spring Boot 3+
- Add dependency:
```xml
<dependency>
    <groupId>org.springdoc</groupId>
    <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
    <version>2.5.0</version>
</dependency>
```
- open src/main/resources/application.properties
- Add below lines:

```java
logging.level.org.springframework = debug

server.port=${PORT:8080}
server.forward-headers-strategy=framework
```

`pom.xml--> rightClick---> Run as mavenbuild`
<img width="1808" height="954" alt="image" src="https://github.com/user-attachments/assets/263310e3-b33d-4f3b-9e29-4fa3227a88fd" />

```bash

mvn azure-webapp:config
[INFO] Scanning for projects...
[INFO] 
[INFO] ------< com.in28minutes.rest.webservices:01-hello-world-rest-api >------
[INFO] Building hello-world-rest-api 0.0.1-SNAPSHOT
[INFO] --------------------------------[ jar ]---------------------------------
[INFO] 
[INFO] --- azure-webapp-maven-plugin:2.13.0:config (default-cli) @ 01-hello-world-rest-api ---
Please choose which part to config [Application]:
* 1: Application
  2: Runtime
  3: DeploymentSlot
Enter your choice: 1
Define value for appName [helloworldnajrin]: 
Define value for resourceGroup [helloworldnajrin-rg]: 
Define value for region [westeurope]: 
Define value for pricingTier [B1]:
   1: D1
   2: B3
   3: P1v2
   4: P1v3
   5: P2v2
   6: P2v3
   7: P3v2
   8: P3v3
*  9: B1
  10: B2
  11: F1
  12: S1
  13: S2
  14: S3
  15: EP3
  16: EP2
  17: EP1
  18: Y1
  19: FC1
Enter your choice: 
Please confirm webapp properties
AppName : helloworldnajrin
ResourceGroup : helloworldnajrin-rg
Region : westeurope
PricingTier : B1
OS : Linux
Java Version: Java 17
Web server stack: Java SE
Deploy to slot : false
Confirm (Y/N) [Y]: Y
[INFO] Saving configuration to pom.
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  19.085 s
[INFO] Finished at: 2026-02-14T15:25:25+05:30
[INFO] ------------------------------------------------------------------------
```
```bash
01-hello-world-rest-api$ mvn azure-webapp:config
[INFO] Scanning for projects...
[INFO] 
[INFO] ------< com.in28minutes.rest.webservices:01-hello-world-rest-api >------
[INFO] Building hello-world-rest-api 0.0.1-SNAPSHOT
[INFO] --------------------------------[ jar ]---------------------------------
[INFO] 
[INFO] --- azure-webapp-maven-plugin:2.13.0:config (default-cli) @ 01-hello-world-rest-api ---
Please choose which part to config [Application]:
* 1: Application
  2: Runtime
  3: DeploymentSlot
Enter your choice: 2
[WARNING] The plugin may not work if you change the os of an existing webapp.
Define value for OS [Linux]:
  1: Windows
* 2: Linux
  3: Docker
Enter your choice: 
Define value for javaVersion [Java 17]:
* 1: Java 17
  2: Java 11
  3: Java 8
Enter your choice: 
[INFO] Skip web container selection for "jar" project.
Please confirm webapp properties
AppName : helloworldnajrin
ResourceGroup : helloworldnajrin-rg
Region : westeurope
PricingTier : B1
OS : Linux
Java Version: Java 17
Web server stack: Java SE
Deploy to slot : false
Confirm (Y/N) [Y]: Y
[INFO] Saving configuration to pom.
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  14.606 s
[INFO] Finished at: 2026-02-14T15:26:09+05:30
[INFO] ------------------------------------------------------------------------
```

```bash

01-hello-world-rest-api$ mvn clean package

01-hello-world-rest-api$ az appservice plan list --output table
AsyncScalingEnabled    ElasticScaleEnabled    FreeOfferExpirationTime     HyperV    IsSpot    IsXenon    Kind    Location     MaximumElasticWorkerCount    MaximumNumberOfWorkers    Name                   NumberOfSites    NumberOfWorkers    PerSiteScaling    Reserved    ResourceGroup        Status    TargetWorkerCount    TargetWorkerSizeId    ZoneRedundant
---------------------  ---------------------  --------------------------  --------  --------  ---------  ------  -----------  ---------------------------  ------------------------  ---------------------  ---------------  -----------------  ----------------  ----------  -------------------  --------  -------------------  --------------------  ---------------
False                  False                  2026-03-16T09:14:49.166666  False     False     False      linux   West Europe  1                            3                         asp-helloworldnajrin   1                1                  False             True        helloworldnajrin-rg  Ready     0                    0                     False



mvn azure-webapp:deploy

```

```bash
01-hello-world-rest-api$ mvn azure-webapp:deploy
[INFO] Scanning for projects...
[INFO] 
[INFO] ------< com.in28minutes.rest.webservices:01-hello-world-rest-api >------
[INFO] Building hello-world-rest-api 0.0.1-SNAPSHOT
[INFO] --------------------------------[ jar ]---------------------------------
[INFO] 
[INFO] --- azure-webapp-maven-plugin:2.13.0:deploy (default-cli) @ 01-hello-world-rest-api ---
Gtk-Message: 14:59:53.413: Failed to load module "appmenu-gtk-module"
[INFO] Auth type: AZURE_CLI
[INFO] Username: azahar.sk.2025@gmail.com
[INFO] Subscription: Azure subscription 1(d8489a1f-c93d-42ee-8068-72ae05f9915b)
[INFO] Start creating Web App(helloworldnajrin)...
[INFO] Web App(helloworldnajrin) is successfully created
[INFO] Trying to deploy external resources to helloworldnajrin...
[INFO] Successfully deployed the resources to helloworldnajrin
[INFO] Trying to deploy artifact to helloworldnajrin...
[INFO] Deploying (/lhome/azahask/javaproject/deploy-spring-boot-to-azure/01-hello-world-rest-api/target/hello-world-rest-api.jar)[jar]  ...

[INFO] Application url: https://helloworldnajrin.azurewebsites.net                                  
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  05:03 min
[INFO] Finished at: 2026-02-14T15:04:51+05:30
[INFO] ------------------------------------------------------------------------
```

## REST EndPOints available in src code:
<img width="1483" height="609" alt="image" src="https://github.com/user-attachments/assets/6ee6ed32-9a25-4e51-873b-c636d5c81114" />
<img width="696" height="95" alt="image" src="https://github.com/user-attachments/assets/d32e1e87-f61c-46fb-9163-7e15d9834ae7" />
<img width="623" height="199" alt="image" src="https://github.com/user-attachments/assets/98370267-72df-4d62-b2da-2edf7f252865" />
<img width="880" height="177" alt="image" src="https://github.com/user-attachments/assets/7e3b83e0-66b7-4415-82c4-e4abba3db1ac" />

## Azure
```
GET https://helloworldnajrin.azurewebsites.net/hello-world-bean
```

<img width="1845" height="952" alt="image" src="https://github.com/user-attachments/assets/2a9e813b-9ee9-4687-8e6b-eb302abc5419" />
<img width="1810" height="578" alt="image" src="https://github.com/user-attachments/assets/e17b8016-15be-4ef4-8f8d-88645cb94dff" />
<img width="1816" height="1112" alt="image" src="https://github.com/user-attachments/assets/d5b50780-54ec-4519-8d85-acd725a10096" />
<img width="1812" height="1062" alt="image" src="https://github.com/user-attachments/assets/0cd46a80-af0d-4845-aa6b-58618fc164c7" />
<img width="1809" height="977" alt="image" src="https://github.com/user-attachments/assets/b3bef271-bed2-405e-a1bb-4c7ac623ea71" />
<img width="1820" height="1118" alt="image" src="https://github.com/user-attachments/assets/8968e8e1-9943-4248-bb56-e2c5c6f775ac" />
<img width="1775" height="885" alt="image" src="https://github.com/user-attachments/assets/e1358e53-3a9d-442f-9ab9-b665db242c52" />
<img width="1812" height="1038" alt="image" src="https://github.com/user-attachments/assets/297a5db2-2b8a-49bd-90e0-467552c73ad9" />

## Kudu console
<img width="1812" height="1062" alt="image" src="https://github.com/user-attachments/assets/3fa65ec4-3b16-4513-9508-057af555052b" />
<img width="1812" height="1062" alt="image" src="https://github.com/user-attachments/assets/78253085-e61d-4f5f-a2dc-db9c08439f82" />
<img width="1740" height="723" alt="image" src="https://github.com/user-attachments/assets/f2d59ec5-5b76-4ad7-81f8-7ce37991573f" />
<img width="1812" height="1062" alt="image" src="https://github.com/user-attachments/assets/824e55b2-58e0-4559-8c0b-fd268bbc12c5" />

## Docker log
<img width="1855" height="323" alt="image" src="https://github.com/user-attachments/assets/b56158f0-298a-4df6-9f76-3379808c46e1" />

## log in local PC
```bash
$   az webapp log tail --name helloworldnajrin --resource-group helloworldnajrin-rg
```
<img width="1746" height="856" alt="image" src="https://github.com/user-attachments/assets/2b229a0c-53fd-4e12-aa56-f8c4b484183f" />



## Modify src c deply new updated version
```bash
mvn clean install -DskipTests  OR mvn clean package -DskipTests
mvn azure-webapp:deploy
```
<img width="727" height="178" alt="image" src="https://github.com/user-attachments/assets/d080c04a-ce2a-4679-a882-4efd42080648" />



###############################################################################################################################

## Docker
```bash
$ sudo apt-get install  ./mysql-apt-config_0.8.36-1_all.deb
$ sudo apt-get update
$ sudo apt-get install mysql-shell


$ sudo snap install docker
$ sudo docker pull mysql:latest

$ sudo docker run --detach --env MYSQL_ROOT_PASSWORD=dummypassword --env MYSQL_USER=todos-user --env MYSQL_PASSWORD=dummytodos --env MYSQL_DATABASE=todos --name mysql --publish 3306:3306 mysql:5.7

// sudo docker container list
$ sudo docker ps
CONTAINER ID   IMAGE       COMMAND                  CREATED          STATUS          PORTS                                                    NAMES
1658f475bb32   mysql:5.7   "docker-entrypoint.s…"   39 seconds ago   Up 38 seconds   0.0.0.0:3306->3306/tcp, [::]:3306->3306/tcp, 33060/tcp   mysql

```
## PORT:
<img width="720" height="544" alt="image" src="https://github.com/user-attachments/assets/ca1dde49-28ad-4215-b539-fa800f57391f" />


```sql
// command: \connect todos-user@localhost:3306

Mistu@ubuntu:~$ mysqlsh
MySQL Shell 8.4.8

Copyright (c) 2016, 2026, Oracle and/or its affiliates.
Oracle is a registered trademark of Oracle Corporation and/or its affiliates.
Other names may be trademarks of their respective owners.

Type '\help' or '\?' for help; '\quit' to exit.
 MySQL  SQL >  \connect todos-user@localhost:3306
Creating a session to 'todos-user@localhost:3306'
Please provide the password for 'todos-user@localhost:3306': **********
Save password for 'todos-user@localhost:3306'? [Y]es/[N]o/Ne[v]er (default No): v
Fetching global names for auto-completion... Press ^C to stop.
Error during auto-completion cache update: Access denied; you need (at least one of) the PROCESS privilege(s) for this operation
Your MySQL connection id is 3
Server version: 5.7.44 MySQL Community Server (GPL)
No default schema selected; type \use <schema> to set one.
 MySQL  localhost:3306 ssl  SQL > \show databases
Unknown report: databases
```

- `OR`
## Test the connection
```bash
$ mysql -h 127.0.0.1 -P 3306 -u todos-user -p
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 10
Server version: 5.7.44 MySQL Community Server (GPL)

Copyright (c) 2000, 2026, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> 
```

<img width="1249" height="702" alt="Screenshot-12" src="https://github.com/user-attachments/assets/9a673c93-d3b1-45d7-8cbd-aeb740edecdf" />

- `Run this file as Java App`

<img width="1202" height="491" alt="2026-02-14_22-06" src="https://github.com/user-attachments/assets/4cfa25f3-44d5-4b8d-af94-4d8239d08ddb" />

## Test:
<img width="954" height="418" alt="2026-02-14_22-16" src="https://github.com/user-attachments/assets/861d6b7c-517c-4255-8067-dd067b99821b" />

```sql
User: in28minutes
Password: dummy
```
<img width="1159" height="418" alt="2026-02-14_22-26" src="https://github.com/user-attachments/assets/a933cb74-fab0-47e0-97be-04810b5cadf5" />
<img width="1277" height="467" alt="2026-02-14_22-29" src="https://github.com/user-attachments/assets/e4033bed-076a-461a-8659-f867b88e651f" />
<img width="1260" height="647" alt="2026-02-14_22-40" src="https://github.com/user-attachments/assets/92c7ad7c-a8f6-4a0d-a223-9956cad159fe" />

## Create SQL Server

<img width="1268" height="683" alt="2026-02-14_23-06" src="https://github.com/user-attachments/assets/41985fa1-5378-4c78-84e7-9628741ec753" />
<img width="1163" height="704" alt="sql" src="https://github.com/user-attachments/assets/e47dc665-b1d1-4f06-a128-580be20a5009" />

```bash
// Azure SQL server details
Admin: todouser
Password: Najrin@123
```

<img width="1166" height="687" alt="sql2" src="https://github.com/user-attachments/assets/f689b6c8-eea7-4fb6-a7b9-afa0245f4469" />
<img width="1270" height="608" alt="todo1" src="https://github.com/user-attachments/assets/d7994563-8366-45eb-9d17-5e6f8771b51e" />
<img width="1298" height="667" alt="sql-server" src="https://github.com/user-attachments/assets/b43d4941-6d7b-4736-ba9f-e5afefa7cf99" />

## Edit src/main/resources/application.properties
```java

#spring.datasource.url=jdbc:mysql://${RDS_HOSTNAME:localhost}:${RDS_PORT:3306}/${RDS_DB_NAME:todos}?serverTimezone=UTC
#spring.datasource.username=${RDS_USERNAME:todouser}
#spring.datasource.password=${RDS_PASSWORD:dummytodos}

RDS_HOSTNAME: todoapp-sql-server-najrin.database.windows.net
RDS_PORT:3306
RDS_DB_NAME:todos
RDS_USERNAME:todouser
RDS_PASSWORD:Najrin@123
```
<img width="1286" height="676" alt="DB-CONFIG" src="https://github.com/user-attachments/assets/d128042c-35be-48fd-9601-640319c48953" />
<img width="943" height="608" alt="db2" src="https://github.com/user-attachments/assets/f7d6c89d-09da-4e51-a2d9-0985db93f2b5" />
<img width="1295" height="655" alt="DB-N" src="https://github.com/user-attachments/assets/52ce1892-0c97-459d-bc40-bcc11ffdd2f1" />
<img width="1295" height="655" alt="DB-N" src="https://github.com/user-attachments/assets/53881686-9ac3-48c7-8417-a5e141e10bc7" />


```bash
// Azure Database for MySQL by Microsoft

Subscription : Azure subscription 1
Resource group : todo-azure-app
Server name: todoapp-sql-server-najrin

Administrator login: todouser
Location: South India
Availability zone: No preference
High availability: Disabled

MySQL version
8.0
Workload type
Dev/Test
Compute + storage
Burstable, B1ms, 1 vCores, 2 GiB RAM, 20 GiB storage, Auto scale IOPS
Backup redundancy
Locally-redundant
Zonal Resiliency
No
```

<img width="1287" height="686" alt="Firewall" src="https://github.com/user-attachments/assets/42218e09-eb09-4220-a350-0d6cc82a5e41" />
- Restart mySQL server

## Cloud shell
```bash
 mysql --host todoapp-sql-server-najrin.mysql.database.azure.com --user todouser -p
```
<img width="1294" height="667" alt="shell" src="https://github.com/user-attachments/assets/733c50ad-8c83-4f43-8f29-b558656ad9d2" />

```sql
MySQL [(none)]> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.023 sec)

MySQL [(none)]> CREATE DATABASE todos;
Query OK, 1 row affected (0.040 sec)

MySQL [(none)]> USE todos;
Database changed
MySQL [todos]> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
| todos              |
+--------------------+
5 rows in set (0.022 sec)

MySQL [todos]>
```

## Check  DB has any row?
<img width="1211" height="660" alt="sql-q1" src="https://github.com/user-attachments/assets/b3eeec33-8cf7-4a7a-a411-2cd33bbcc6a0" />

## Restart App service 

