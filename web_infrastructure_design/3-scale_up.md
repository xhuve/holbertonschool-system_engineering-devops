# Web Infrastructure

## Infrastructure Specifics

### 1. Add: 1 Server

- **Why?**: Adding an additional server increases the system's **scalability** and **redundancy**. This additional server can be used to distribute the workload across multiple servers, enhancing the capacity to handle traffic, improving performance, and providing backup resources in case of failure. It can also host a specific component like a web server, application server, or database server, contributing to a **decoupled architecture**.

### 2. Add: 1 Load Balancer (HAProxy) configured as a cluster with the other one

- **Why?**: Adding a second load balancer configured in a **cluster** with the existing one ensures **high availability**. If one load balancer fails, the other one will take over without causing downtime. This eliminates the **Single Point of Failure (SPOF)** at the load balancer level and ensures continuous traffic distribution.
  - **HAProxy Cluster**: The two load balancers (HAProxy) are configured to work in **Active-Active** or **Active-Passive** mode. In Active-Active, both load balancers handle traffic simultaneously, whereas in Active-Passive, one is active while the other is on standby, ready to take over in case of failure.

### 3. Split Components: Web Server, Application Server, and Database each on their own server

- **Web Server** (e.g., Nginx or Apache)
  - **Why?**: Separating the **web server** onto its own dedicated server enhances performance and scalability. The web server is responsible for handling incoming HTTP/HTTPS requests and serving static content (HTML, CSS, JavaScript). By decoupling it from other components, the system can scale the web layer independently, allowing it to handle more traffic without affecting other services.
- **Application Server** (e.g., Node.js, Python/Django, PHP)
  - **Why?**: Placing the **application server** on its own dedicated machine improves performance and fault isolation. The application server runs the business logic of the web application, processing dynamic requests and interacting with databases. Isolating it allows you to scale the application layer based on its specific workload without impacting the web server or database.
- **Database Server** (e.g., MySQL, PostgreSQL)
  - **Why?**: Moving the **database** to a dedicated server improves **data integrity**, performance, and manageability. The database requires significant resources (CPU, memory, storage) for managing and querying data. Isolating the database server prevents it from competing for resources with the web or application servers, and allows it to scale independently based on query load.

---

## Overview of Infrastructure Changes

### 1. Why Adding the Elements Improves the Infrastructure:

- **1 Additional Server**: Improves overall scalability and redundancy, providing more resources and fault tolerance.
- **HAProxy Load Balancer Cluster**: Ensures high availability by eliminating SPOF at the load balancer level and allowing failover in case one load balancer goes down.
- **Split Components (Web, Application, Database Servers)**: Improves performance by isolating services on dedicated machines, allows for independent scaling of each component, and enhances fault isolation, making the system more resilient and easier to manage.

By splitting the components and adding a clustered load balancer, the infrastructure becomes more scalable, fault-tolerant, and efficient. Each part of the system can be maintained and scaled independently, reducing the risk of cascading failures and ensuring smoother operations under high traffic or load.
