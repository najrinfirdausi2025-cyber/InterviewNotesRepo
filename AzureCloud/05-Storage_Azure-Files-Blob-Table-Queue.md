## 1️⃣ What is Azure Storage?

__Microsoft Azure Storage is a scalable, durable, highly available cloud storage service used to store:__

- Files / pdf/ docs 
- Images / videos / Audio
- Logs
- Database-like NoSQL data
- Disks for VMs
- Backups

__Think of it as AWS S3 + EBS + DynamoDB + File Server combined in one ecosystem.__

# Azure Storage Account --- Feature Summary

## 10 Key Points

1.  **Non-relational storage support**\
    A storage account can store unstructured data (PDF, video, image,
    audio) without fixed schema --- unlike relational databases
    (rows/columns).

2.  **Multi-media unified storage**\
    One single Microsoft Azure Storage Account can hold mixed file types
    together in the same container.

3.  **Region placement matters (performance + cost)**\
    Storage should be created in the same region as the application
    (VM/WebApp) to reduce latency and cross-region traffic charges.

4.  **Account types (Standard vs Premium)**

    -   General Purpose v2 (Standard) → supports blobs, files, tables,
        queues\
    -   Premium → high-speed SSD, mainly blobs & files only

5.  **Redundancy options (data durability)**

    -   LRS → 3 copies in same datacenter\
    -   ZRS → 3 copies in different zones\
    -   GRS → 6 copies across regions\
    -   RA-GRS → secondary region read access


- `Locally redundant storage LRS` − Copy of the data is created in the same region where storage account is created. There are 3 copies of each request made against the data that resides on separate domains.

- `Zone-redundant storage (available for blobs only) ZRS` − Copy of the data is created on separate facilities either in the same region or across two regions. The advantage is that even if there is failure on one facility, the data still can be retained. Three copies of data are created. One more advantage is that data can be read from a secondary location.

- `Geo-redundant storage GRS` − `Copy is created in a different region which means data is retained even if there is a failure in the complete region. The numbers of copies of data created are 6 in this case.

- `Read-access geo-redundant storage RA-GRS` − This option allows reading of data from a secondary location when data on the primary location is not available. The number of copies created is 6. The main advantage here is that availability of data can be maximized.
  
6.  **Security configuration**

    -   HTTPS-only access recommended\
    -   Key-based authentication default\
    -   Moving toward Microsoft Entra ID authentication\
    -   Optional anonymous access

7.  **Access tiers (cost optimization)**

    -   Hot → frequent read/write\
    -   Cool → rare access (backup/logs) cheaper storage but costly
        retrieval

8.  **Networking control**

    -   Public endpoint enabled by default\
    -   Can restrict to private network / selected VNets to prevent key
        leakage exposure

9.  **Data protection features**

    -   Soft delete (recover deleted files)\
    -   Versioning (keep all file versions)\
    -   Change feed (track modifications)\
    -   Immutability (cannot modify/delete once written)

10. **Encryption & key management**

-   Encryption enabled by default\
-   Microsoft-managed keys or customer-managed keys\
-   Optional double encryption (software + hardware disk encryption)

--------------------

## Storage Account Structure

<img width="1705" height="1033" alt="image" src="https://github.com/user-attachments/assets/e23459cf-999f-486d-9622-610410cd3241" />
<img width="1346" height="1112" alt="image" src="https://github.com/user-attachments/assets/23de385a-08de-424f-93da-5a71c2bd7ddb" />
<img width="1192" height="1092" alt="image" src="https://github.com/user-attachments/assets/772036a9-d0c7-45c4-acdd-ae62dfb23a32" />
<img width="1345" height="1133" alt="image" src="https://github.com/user-attachments/assets/2ea01daf-b3c9-4ae8-b659-3fe180142c9a" />
<img width="983" height="1117" alt="image" src="https://github.com/user-attachments/assets/d0b2b7f5-2c08-4fc5-912d-d5ce58681e1b" />
<img width="1261" height="809" alt="image" src="https://github.com/user-attachments/assets/e0a6eb8c-af9a-4a2d-b448-e6175634a34a" />
<img width="1345" height="1133" alt="image" src="https://github.com/user-attachments/assets/a517b3aa-ac65-494e-9b27-47f5eed56d1f" />
<img width="1806" height="766" alt="image" src="https://github.com/user-attachments/assets/e72b0677-dda9-453a-90e2-4a20666e0f8f" />
<img width="1643" height="954" alt="image" src="https://github.com/user-attachments/assets/9ad418fd-d92f-45c5-9dbd-dd3b8d1ef5da" />


## Azure Storage Types

```json
1>  Blob Storage (Object Storage)
1>  File Storage
3>  Table Storage
4>  Queue Storage
5>  Disk Storage


Storage Account
├── Blob Containers
├── File Shares
├── Tables
└── Queues
```

----------------------------------------

### 🧱 Blob Storage (Object Storage)
Used to store unstructured data:
- Profile pictures
- PDFs
- Videos
- ML datasets
- Logs
- Backups

**Blob Types**
| Type | Use Case |
|------|------|
| Block Blob | Images, files, uploads |
| Append Blob | Logging systems |
| Page Blob | Virtual machine disks |

**Example**
React → Backend API → Blob → CDN
---


## Creating blob:
<img width="1844" height="1015" alt="image" src="https://github.com/user-attachments/assets/7acd6d35-4ba9-4cf9-924a-71acf06a9fa4" />
<img width="1846" height="773" alt="image" src="https://github.com/user-attachments/assets/dbdd168b-da6e-453a-aa5a-50f7db7652ed" />
<img width="1837" height="852" alt="image" src="https://github.com/user-attachments/assets/6d61289d-7f03-42a2-bd5a-ca241eb0b82c" />

<img width="1934" height="1084" alt="image" src="https://github.com/user-attachments/assets/06062eea-6e26-449d-83c4-61406cc8bbf8" />

### Generate SAS token
<img width="1781" height="1091" alt="image" src="https://github.com/user-attachments/assets/14e37274-4ab0-4106-828d-28f94c8d7043" />
<img width="1852" height="994" alt="image" src="https://github.com/user-attachments/assets/e0d348cd-2d2a-46dd-a775-61372025e092" />
<img width="1860" height="1102" alt="image" src="https://github.com/user-attachments/assets/11795068-6ada-4c8a-ab05-57daccc89772" />

```
https://appnewstorage.blob.core.windows.net/blob1/MVC.md?sp=r&st=2026-02-21T19:20:40Z&se=2026-02-22T03:35:40Z&sv=2024-11-04&sr=b&sig=TPqt7yHORGXOMJ%2FBcUxyHmQYHwSCvzxveKe3xXSd7%2FI%3D
```
---------------------

### 📁 File Storage
Cloud SMB file share: \\\\companyshare\\documents

Use cases:
- Legacy apps
- Shared folders
- Lift-and-shift migration


<img width="1755" height="774" alt="image" src="https://github.com/user-attachments/assets/c129f621-1d2f-4dfa-9c39-ca414d9caf58" />
<img width="1431" height="700" alt="image" src="https://github.com/user-attachments/assets/1a3db12d-8ca9-4040-a321-d37f1fe3d79c" />
<img width="962" height="1090" alt="image" src="https://github.com/user-attachments/assets/3097b2b1-9153-4783-8a76-2c9af1867ce7" />
<img width="1776" height="855" alt="image" src="https://github.com/user-attachments/assets/da17358c-cf69-4665-9aab-695f2e5e323f" />
<img width="1781" height="1091" alt="image" src="https://github.com/user-attachments/assets/41e717fe-d29d-4711-96ad-4f34f64a5488" />
<img width="1781" height="1091" alt="image" src="https://github.com/user-attachments/assets/5b4a974c-2d92-4ba0-b6f8-1c5461e1962a" />
<img width="1843" height="956" alt="image" src="https://github.com/user-attachments/assets/505e3e99-2e11-4966-abfe-d26a69df9070" />
<img width="1853" height="985" alt="image" src="https://github.com/user-attachments/assets/5b4ca4e9-0200-4f37-8d0c-938274495553" />
<img width="1858" height="694" alt="image" src="https://github.com/user-attachments/assets/6aa277c8-e661-4f8e-beac-4e25d13d4e52" />
<img width="1851" height="949" alt="image" src="https://github.com/user-attachments/assets/ebdd802b-bac8-43ed-ae09-751f3a0dfd6b" />
<img width="1848" height="881" alt="image" src="https://github.com/user-attachments/assets/cceb8357-fce5-45a6-be06-1d36f054004c" />
<img width="1848" height="881" alt="image" src="https://github.com/user-attachments/assets/cde59b6d-cc94-4402-a1aa-fbeb99a7a04d" />
<img width="1848" height="881" alt="image" src="https://github.com/user-attachments/assets/1fd03040-e18d-43a0-9f68-f199e438727b" />

-------------------------------------

### 🧠 Table Storage
NoSQL Key-Value DB: 

Semi Structure data:
PartitionKey | RowKey | Properties

- Storing a table does not mean relational database here.
- Azure Storage can store just a table without any foreign keys or any other kind of relation.
- These tables are highly scalable and ideal for handling large amount of data. Tables can be stored and queried for large amount of data.

Used for:
- Sessions
- IoT telemetry
- Metadata
- Cache


<img width="1910" height="1082" alt="image" src="https://github.com/user-attachments/assets/bfe5ef4c-590d-434c-b50a-4ebbdb01b2fe" />
<img width="1910" height="1082" alt="image" src="https://github.com/user-attachments/assets/9f26be82-fe4a-4764-b9a5-0a41a8329be2" />

### why Azure Table Storage is not the same as a relational database ?

`💡 Summary: Table Storage looks like a table but is non-relational, semi-structured, and flexible, unlike SQL databases which are strictly structured with enforced relationships.`

__1. Semi-Structured Data__

- Table Storage stores entities with properties that can vary per row.
- Unlike relational tables, columns are not strictly enforced; some rows can have missing or extra properties.

__2. No Fixed Schema__

- You can add new properties to an entity at any time.
- No requirement that all rows have the same columns or data types.

__3. No Relational Constraints__

- Table Storage does not support foreign keys, joins, or referential integrity.
- Cannot enforce relationships between tables like in SQL.

__4. Primary Key is Simple__

- Each entity has a PartitionKey and RowKey for uniqueness.
- There is no complex indexing, constraints, or relational keys beyond this.

__5. Flexible but Limited Queries__
- Queries are performed on PartitionKey/RowKey or properties, but no complex relational operations like JOIN, GROUP BY, or transactions across multiple tables.

------------------------------------------

### 💾 Queue Storage
- Microsoft Azure provides two message queue services:

```json
        - 1> Azure Queue Storage
        - 2> Azure Service Bus (Service Bus Queue)
```

This note mainly focuses on Azure Queue Storage.

__Azure Queue Storage is a cloud-based message queue service used to store large numbers of messages.__

It enables:
    - A sender to send messages
    - A receiver (client/worker) to receive and process messages
    - Asynchronous communication between application components/services

### 🔹 How It Works (Basic Flow)

- Sender places a message in the queue.
    - Where Each message includes attributes such as:
       ```json
          - Message ID
          - Insertion time
          - Expiry time (TTL – Time to Live)
          - Dequeue count
        ```
    
    - Maximum message size Limit: 64 KB
    - A queue can handle millions of messages (older references mention 20,000 per request batch limit, not total).
    - Data is automatically replicated depending on storage redundancy (LRS, GRS, etc.) -Azure Storage provides redundancy at the storage account level.
    
    
- Message stays in the queue until -- A worker processes and deletes it, OR It expires.

  ```json
          Messages can be stored for up to 7 days (older limitation; modern Azure allows configurable TTL).
          If not deleted within the TTL, the message is automatically removed.
  ```
- Worker retrieves the message - using a __peek-lock pattern (visibility timeout)__.
- After processing, worker deletes the message- If a worker fails to delete the message, it becomes __visible__ again.
- Azure Queue supports:

```json
    ✅ One sender → One receiver
    ✅ One sender → Many receivers
    ✅ Many senders → Many receivers
```

### Example:
User Upload → Queue → Worker → DB



### Used heavily in:

- Background job processing
- Microservices communication
- Task scheduling
- Order processing systems
- Video processing pipelines

### 🔹 Key Advantage – Decoupling

Message queues help in loosely coupling components.

Example:

- Frontend sends a task message.
- Backend worker processes it asynchronously.
- Frontend does not wait → improves performance & scalability.

This enables:

- Fault tolerance
- Scalability
- Asynchronous processing
- Better workflow management

### 🔹 Real-World Example

E-commerce Order Flow:

```json
1. User places order.

2. Order message sent to queue.

3. Worker:

    * Processes payment
    * Updates inventory
    * Sends confirmation email

4. Deletes message after completion.
```

### 🔹 Interview One-Line Definition
- Azure Queue Storage is a cloud-based messaging service that enables asynchronous communication between application components and services by storing and delivering messages reliably at scale.

<img width="1036" height="482" alt="image" src="https://github.com/user-attachments/assets/7eee7c23-0102-4dad-89b6-7d6e026d5af3" />


------------------------------

### 🖴 Disk Storage
VM disks:
- Standard HDD
- Standard SSD
- Premium SSD
- Ultra Disk

-------------------------------






