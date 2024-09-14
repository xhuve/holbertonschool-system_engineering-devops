# Infrastructure: Explanations and Issues

## Infrastructure Specifics

### 1. For every additional element, why you are adding it?

- **Load Balancer**: A load balancer distributes traffic across multiple servers to ensure no single server is overwhelmed. It helps improve fault tolerance, allowing the infrastructure to handle more requests and remain operational if one server fails.
- **Primary-Replica (Master-Slave) Database Cluster**: This ensures data redundancy and improves read performance by having one **Primary** (Master) node handling write operations, and multiple **Replica** (Slave) nodes handling read operations. It improves fault tolerance and read scalability.
- **Firewall**: Protects the system from unauthorized access, malicious traffic, and attacks by filtering incoming and outgoing network traffic based on security rules.
- **HTTPS**: Provides secure communication between the server and clients by encrypting data to prevent eavesdropping and data tampering during transmission.
- **Monitoring Tools**: Track system health, performance metrics, and detect failures or bottlenecks early. It helps with proactive troubleshooting and reduces downtime.

### 2. What distribution algorithm is your load balancer configured with, and how does it work?

- **Weighted Round Robin**: The load balancer is configured with the **Weighted Round Robin** algorithm, which distributes incoming traffic evenly across all available servers in a rotating sequence. It also allows you to give the _weight_ a certain server can handle, given the scenario where one server can handle more requests (due to hardware) than another server.
  - **How it works**: When a client request arrives, the WRR algorithm doesn’t just randomly distribute it to any server. Instead, it intelligently directs the request to the server with the highest weight. This means that a server with a higher weight (indicating higher capacity) will receive a larger share of the client requests compared to a server with a lower weight.

### 3. Is your load-balancer enabling an Active-Active or Active-Passive setup, and what is the difference?

- **Active-Active Setup**: The load balancer in this setup is **Active-Active**, where multiple servers are actively serving traffic simultaneously. It improves resource utilization, fault tolerance, and performance as all servers share the load.
  - **Active-Active vs. Active-Passive**:
    - **Active-Active**: All servers or systems are active and handling traffic simultaneously. If one fails, the load is redistributed across the remaining servers.
    - **Active-Passive**: Only one (active) server handles traffic, while the passive server stays on standby. If the active server fails, the passive server takes over.

### 4. How does a database Primary-Replica (Master-Slave) cluster work?

- In a **Primary-Replica (Master-Slave) database cluster**, the **Primary node** (Master) handles all write operations and propagates changes to **Replica nodes** (Slaves). The replicas receive updates from the primary and can serve read-only queries.
  - **Replication**: Data changes made on the primary node are replicated (synchronized) to the replicas either synchronously (immediate replication) or asynchronously (delayed replication).

### 5. What is the difference between the Primary node and the Replica node in regard to the application?

- **Primary Node (Master)**: Handles all **write** operations (inserts, updates, deletes) for the application.
- **Replica Node (Slave)**: Only handles **read** operations. Write operations cannot be sent to replicas, which are designed to offload read traffic from the primary node and improve query performance in read-heavy applications.

---

## Infrastructure Issues

### 1. Where are SPOF (Single Points of Failure)?

- **Single Load Balancer**: If the load balancer is a single instance without failover or redundancy, it becomes a **SPOF**. If it fails, no traffic can be routed to the servers.
- **Single Primary Database**: The primary node of the database is a **SPOF**. If it fails and there is no failover mechanism (e.g., promoting a replica to the primary), the application will be unable to perform write operations.

### 2. Security Issues

- **No Firewall**: Without a firewall, the system is vulnerable to unauthorized access, network-based attacks, and malicious traffic. A firewall is critical for securing the infrastructure.
- **No HTTPS**: Without HTTPS, communication between the server and clients is **unencrypted**, leaving the data vulnerable to interception, eavesdropping, and man-in-the-middle attacks.

### 3. No Monitoring

- **No Monitoring Tools**: Without monitoring, there is no way to track system performance, detect outages, or proactively identify potential problems. This can lead to undetected failures, extended downtime, and poor performance, as issues are only addressed reactively.
