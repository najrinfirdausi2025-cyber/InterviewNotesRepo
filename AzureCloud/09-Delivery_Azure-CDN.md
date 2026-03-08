# AZURE CDN : Content Delivery Network:
- A content delivery network (CDN) - A software service by the azure cloud platforms - can be seen as a widely dispersed collection of servers responsible for boosting performance of delivering high-bandwidth web content to users.
- In Azure CDN, cached content is held on edge servers in point-of-presence (POP) locations strategically positioned near end users to reduce latency.
- This approach offers developers a means to furnish users with data-rich content faster by caching it at strategically located physical nodes around the world.
- Azure has is CDN servers in more than 70 cities around the world. It helps you reduce the load times of your websites, mobile apps, streaming media, or games.
- The CDN saves the bandwidth, increases the latency and speed responsiveness.
  
<img width="675" height="270" alt="image" src="https://github.com/user-attachments/assets/e086c833-2927-4cc9-829b-ef8b8cafbaf5" />
<img width="1006" height="557" alt="image" src="https://github.com/user-attachments/assets/16bb7368-f0f2-4aec-b1aa-1b7f80bad19c" />
<img width="800" height="455" alt="image" src="https://github.com/user-attachments/assets/54dfb82f-4960-4be9-91a2-cb50bcde15b3" />


- Let's say If your website is hosted on a **US server**, users from London must request data across the Atlantic Ocean → higher **latency**, increased **bandwidth usage**, and slower response time.

- A **Content Delivery Network (CDN)** solves this problem using the **caching principle**.

- A CDN consists of:
  - **Origin Server** → The main server where original content is stored.
  - **Edge Servers / Points of Presence (POP)** → Distributed servers located in multiple geographic regions worldwide.

- When a user from London makes a request:
  - The request is routed to the **nearest POP**.
  - If the content is not cached, the POP fetches it from the **Origin server**.
  - The POP then **caches** the content locally for future use.

- For subsequent requests from users in the same region:
  - Content is served directly from the **POP cache**.
  - Long-distance (inter-continent) data transfer is avoided.

- Benefits:
  - ✅ Faster content delivery  
  - ✅ Reduced latency  
  - ✅ Lower bandwidth consumption  
  - ✅ Reduced load on the origin server  

- **Time to Live (TTL)**:
  - Defines how long content remains cached in the POP.
  - Typically around **7 days** (configurable).
  - After TTL expires, fresh content is fetched from the Origin upon the next request.
 

## How and why a CDN is used
Typical uses for a CDN include:

- __`Delivering static resources for client applications:`__
  
Often from a website. These resources can be images, style sheets, documents, files, client-side scripts, HTML pages, HTML fragments,
or any other content that the server does not need to modify for each request.
The application can create items at runtime and make them available to the CDN (for example, by creating a list of current news headlines), but it does not do so for each request.

- `Delivering public static and shared content to devices:` Such as mobile phones and tablet computers. The application itself is a web service that offers an API to clients running on the various devices. The CDN can also deliver static datasets (via the web service) for the clients to use, perhaps to generate the client UI. For example, the CDN could be used to distribute JSON or XML documents.

- `Serving entire websites:` that consist of only public static content to clients, without requiring any dedicated compute resources.

- `Streaming video files to the client on demand:` Video benefits from the low latency and reliable connectivity available from the globally located datacenters that offer CDN connections. Microsoft Azure Media Services integrates with Azure Content Delivery Network to deliver content directly to the CDN for further distribution. For more information, see Streaming endpoints overview.

- `Generally improving the experience for users:` Especially those located far from the datacenter hosting the application. These users might otherwise suffer higher latency. A large proportion of the total size of the content in a web application is often static, and using the CDN can help to maintain performance and overall user experience while eliminating the requirement to deploy the application to multiple datacenters. For a list of Azure Content Delivery Network node locations, see Azure CDN POP Locations.

- `Supporting IoT (Internet of Things) solutions:` The huge numbers of devices and appliances involved in an IoT solution could easily overwhelm an application if it had to distribute firmware updates directly to each device.


- `Coping with peaks and surges in demand without requiring the application to scale:` avoiding the consequent increase in running costs. For example, when an update to an operating system is released for a hardware device such as a specific model of router, or for a consumer device such as a smart TV, there's a huge peak in demand as it is downloaded by millions of users and devices over a short period.



<img width="1521" height="929" alt="image" src="https://github.com/user-attachments/assets/e02c7c12-a5d0-4a0f-a216-6d7addf9edf8" />
<img width="1725" height="1000" alt="image" src="https://github.com/user-attachments/assets/2fb8302c-f733-42af-82d6-40d355dcdb7d" />
<img width="1725" height="1000" alt="image" src="https://github.com/user-attachments/assets/c30fb82e-0c45-4211-a9e5-c57fc1a92ab1" />
<img width="1725" height="1000" alt="image" src="https://github.com/user-attachments/assets/d97b1842-b875-4a9f-81a9-082fe5f83ede" />
<img width="1903" height="943" alt="image" src="https://github.com/user-attachments/assets/b44b94f2-a42c-4631-9dde-0c478234b1d2" />
<img width="1725" height="1000" alt="image" src="https://github.com/user-attachments/assets/e0373e55-010b-41bb-829d-60fcffd24774" />
<img width="1816" height="992" alt="image" src="https://github.com/user-attachments/assets/628348e2-2c92-4b43-966f-635d0bf012fc" />
<img width="1915" height="937" alt="image" src="https://github.com/user-attachments/assets/2f6fcf2a-3583-48f9-97e1-8cd88ef18cc3" />

## Test: Open Google chrome tab developer mode --> Network section --> Disable cache

<img width="1918" height="1024" alt="image" src="https://github.com/user-attachments/assets/6c7068b8-5fa8-491a-849d-e7773916ed68" />
<img width="1918" height="1024" alt="image" src="https://github.com/user-attachments/assets/d0a30b73-d624-4b75-b7f3-1209af51dbfa" />
<img width="1918" height="1024" alt="image" src="https://github.com/user-attachments/assets/b37d4c99-763c-47f5-801e-c088bc3f7ade" />
<img width="1918" height="1024" alt="image" src="https://github.com/user-attachments/assets/ff497fe4-dbc7-4e9d-bea9-e858ebedcdfd" />





