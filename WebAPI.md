- Ref: https://www.youtube.com/watch?v=XStpo9VlzCI&t=3404s
- Ref : https://www.youtube.com/watch?v=c4Ry8B1nTZU&t=3211s

# Web API :

A __Web API__ is an interface that allows applications to communicate and exchange data over the web using standard protocols such as HTTP or HTTPS. It exposes a set of endpoints (URLs) that clients can call to perform operations or retrieve data.

- Data is usually transferred in JSON or XML format.
- It enables integration between different platforms, such as web apps, mobile apps, and third-party services.
- Examples include payment APIs, weather APIs, and social media APIs.

__Key points to mention:__

- Uses HTTP methods like GET, POST, PUT, DELETE.
- Platform-independent and language-agnostic.
- Can be implemented in REST, SOAP, or GraphQL styles.

<img width="1580" height="828" alt="image" src="https://github.com/user-attachments/assets/855613fd-7bd1-49f2-b821-29bd62369d30" />
<img width="1607" height="756" alt="image" src="https://github.com/user-attachments/assets/74837450-898e-40f4-a05c-f3c28da215ea" />
<img width="1616" height="839" alt="image" src="https://github.com/user-attachments/assets/a7af7d03-76ad-4f12-9c7f-d0c3447ce9e9" />

# REST and RESTFUL ? difference ? interview question 
<img width="1023" height="507" alt="image" src="https://github.com/user-attachments/assets/a9300b2b-6bc4-4ef6-9700-af552fda1876" />

# REST Guidelines
<img width="1890" height="1017" alt="image" src="https://github.com/user-attachments/assets/fc0e9bf0-5c4d-476b-b400-b57202f7c6fb" />

# What is Authentication and Authorization ?

__Authentication:__ is the process of verifying who the user or client is (identity verification).
__Authorization:__ is the process of determining what actions or resources that authenticated user is allowed to access (permissions).

Example:

- __Authentication:__ → Logging in with username/password.
- __Authorization:__ → Allowing only admins to delete data.

__Types of Authentication supported in FastAPI:__
FastAPI doesn’t impose one fixed method but supports multiple authentication schemes via the fastapi.security module and integration with OAuth2. Common types include:

- `HTTP Basic Authentication` – Using username & password in the Authorization header.
- `HTTP Bearer Token` – Passing a token (like JWT) in the Authorization: Bearer <token> header.
- `OAuth2` – With password flow, authorization code flow, or implicit flow. Often combined with JWT.
- `API Key Authentication` – Sending a key via query parameters, headers, or cookies.
- `Custom Authentication` – Implementing your own logic using FastAPI’s dependency injection.
- `FastAPI uses dependency injection` to plug in authentication mechanisms, making it easy to swap between methods like JWT, OAuth2, or API Keys without changing endpoint logic.

<img width="1637" height="696" alt="image" src="https://github.com/user-attachments/assets/f00f792c-5d75-4e00-a679-7b203ff58b3f" />

# What is API Key authentication ?
<img width="992" height="586" alt="image" src="https://github.com/user-attachments/assets/7afdd907-fd70-40ef-8dda-ebe5fcdfc624" />
<img width="1630" height="820" alt="image" src="https://github.com/user-attachments/assets/b47173ab-6d29-46d8-88d8-6c2b2623273b" />
- User does not need username password in this method
