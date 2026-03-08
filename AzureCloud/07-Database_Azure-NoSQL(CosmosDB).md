<img width="1853" height="465" alt="image" src="https://github.com/user-attachments/assets/6b49437e-72dc-477b-8b7b-f6f8895e30c9" />
<img width="1853" height="465" alt="image" src="https://github.com/user-attachments/assets/d153cf71-c222-4d51-8857-a4dabdbfb4c0" />
<img width="1602" height="1050" alt="image" src="https://github.com/user-attachments/assets/5f9d7acd-c13a-4c86-a3ef-09b9632ab6dc" />
<img width="1907" height="1042" alt="image" src="https://github.com/user-attachments/assets/a6caad2e-48ca-4c96-953c-ea148c1e3b36" />
<img width="1907" height="1042" alt="image" src="https://github.com/user-attachments/assets/08979bf2-d86b-4bc5-a670-5c4bd69fe5b0" />
<img width="1907" height="1042" alt="image" src="https://github.com/user-attachments/assets/b1409bdc-3d81-44d6-8e15-c62d728b573a" />
<img width="1907" height="1042" alt="image" src="https://github.com/user-attachments/assets/5b4952eb-430c-4929-85b3-13204dda69dc" />
<img width="1907" height="1042" alt="image" src="https://github.com/user-attachments/assets/704f6bff-fe87-4fcc-90db-c192f443f732" />
<img width="1907" height="1042" alt="image" src="https://github.com/user-attachments/assets/696dbc2f-5f51-4e92-a744-49c56d531590" />
<img width="1907" height="1042" alt="image" src="https://github.com/user-attachments/assets/628e136c-043c-4f55-b935-7be4766ef809" />
<img width="1920" height="831" alt="image" src="https://github.com/user-attachments/assets/607aba51-4543-4d52-9c28-f91ae08ec4c5" />
<img width="1920" height="979" alt="image" src="https://github.com/user-attachments/assets/4acba490-c8e5-421b-ab8a-29e0a1c4ba96" />
<img width="1867" height="805" alt="image" src="https://github.com/user-attachments/assets/66b3f171-afcd-4ab6-b8c3-b0719bb5f8a4" />
<img width="1867" height="955" alt="image" src="https://github.com/user-attachments/assets/1735deaf-c43f-4769-afbc-3cf9ad1d0da4" />
<img width="1867" height="955" alt="image" src="https://github.com/user-attachments/assets/a82be608-8765-41de-910d-7b0dd63244e3" />

## COSMOSDB -LAB

<img width="1857" height="956" alt="image" src="https://github.com/user-attachments/assets/cc8fdcbb-cdf0-43a1-a2ed-542952295eae" />
<img width="1376" height="897" alt="image" src="https://github.com/user-attachments/assets/520703e6-0a39-4aa4-8c10-faa68ae25d54" />
<img width="1840" height="1106" alt="image" src="https://github.com/user-attachments/assets/f24d7d9c-adee-4e36-8eba-aab5e6b79d92" />
<img width="1412" height="1067" alt="image" src="https://github.com/user-attachments/assets/f5779332-668d-4555-a23e-ad17f33b1332" />
<img width="1742" height="656" alt="image" src="https://github.com/user-attachments/assets/112ebaf7-57eb-4d47-b82a-6d5f14768511" />
<img width="1743" height="1076" alt="image" src="https://github.com/user-attachments/assets/1bbb6725-6bc8-49fe-8214-03eabb3b5955" />
<img width="1686" height="1094" alt="image" src="https://github.com/user-attachments/assets/42d855db-42ea-472e-93c1-c33a1e597702" />
<img width="1831" height="818" alt="image" src="https://github.com/user-attachments/assets/44a9873d-452d-4008-ad6b-37108d96e35d" />
<img width="1804" height="1026" alt="image" src="https://github.com/user-attachments/assets/61d68ec1-c369-4ab9-96fc-c839c4b9d9e9" />
<img width="1762" height="761" alt="image" src="https://github.com/user-attachments/assets/d55c1085-59b5-4753-b8bf-0f47ac09f010" />
<img width="1856" height="760" alt="image" src="https://github.com/user-attachments/assets/1f1d7fe5-a34b-4d40-84ec-33d949f17d9a" />
<img width="1717" height="968" alt="image" src="https://github.com/user-attachments/assets/6649cac2-3299-4f52-a921-17d705986f2e" />
<img width="1804" height="1026" alt="image" src="https://github.com/user-attachments/assets/a229dd68-006c-487c-90c3-7a5f803cf3d6" />
<img width="1804" height="1026" alt="image" src="https://github.com/user-attachments/assets/c2cbf665-519f-4586-9d60-e430acf35f9d" />
<img width="1804" height="1026" alt="image" src="https://github.com/user-attachments/assets/e151177c-faab-41b0-b6a9-9a8e5f8394b4" />
<img width="1804" height="1026" alt="image" src="https://github.com/user-attachments/assets/8ee53a37-b4a8-4c13-a290-a876b87985e9" />


## Use ARM Templates to Manage Cosmos DB automation for 100s cosmos DB

- ARM Templates allow you to define Cosmos DB accounts, databases, containers, throughput (RU/s), indexing policies, consistency levels in JSON.
- Ensures identical environments across Dev, QA, Prod.
- Prevents manual configuration errors from Azure Portal.


__cosmos-template.json__
```json
{
  "type": "Microsoft.DocumentDB/databaseAccounts",
  "apiVersion": "2023-04-15",
  "name": "cosmosdb-prod",
  "location": "Central India",
  "properties": {
    "databaseAccountOfferType": "Standard",
    "consistencyPolicy": {
      "defaultConsistencyLevel": "Session"
    }
  }
}
```
- Using ARM templates integrate with: Azure DevOps,GitHub Actions, Azure CLI
- Enables automated provisioning during deployment pipelines.
- Useful for multi-tenant SaaS or dynamic environment creation.
```
az deployment group create \
  --resource-group rg-prod \
  --template-file cosmos-template.json
```

### Use parameters to dynamically configure:

- Throughput (RU/s)
- Autoscale vs Manual
- Region replication
- Backup policy

-------------------

## Azure Cosmos DB Security – 5 Point Summary

### 1️⃣ Network Access Control (Public vs Private)

- Cosmos DB can have a publicly accessible endpoint (URL).
- Access can be restricted by selecting **Selected Networks** instead of **All Networks**.
- You can move the database from public internet access into a **Virtual Network (VNet)**.
- This limits which networks can reach the Cosmos DB account.


### 2️⃣ Firewall & IP Whitelisting

- When "Selected Networks" is enabled:
  - Specific IP addresses or IP ranges can be whitelisted.
  - On-premises networks can be allowed.
  - Only Azure services can be permitted.
- Firewall rules control inbound traffic to the database.

### 3️⃣ Access Keys (Primary & Secondary)

- Cosmos DB provides:
  - Primary Key (full access)
  - Secondary Key (full access)
- Anyone with the database URL + key has complete control.
- These keys must be kept secure and not shared publicly.

### 4️⃣ Read-Only Keys for Safer Access

- Cosmos DB provides Read-Only Keys.
- Ideal for applications that only need to read data.
- Prevents accidental modifications or deletions.
- Safer than exposing full-access keys.

### 5️⃣ Key Regeneration for Security Recovery

- If a key is compromised, it can be regenerated.
- Regenerating a key immediately invalidates the old key.
- Applications using the old key will lose access until updated.
- Enables quick security recovery without deleting the database.



### 🎯 Cosmos DB security Interview Summary

Cosmos DB security is enforced through network isolation (VNet and firewall rules), secure key-based authentication (primary, secondary, and read-only keys), and the ability to regenerate keys to mitigate security risks.
