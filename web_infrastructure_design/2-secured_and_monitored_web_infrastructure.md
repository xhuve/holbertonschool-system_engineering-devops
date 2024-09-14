# Web Infrastructure

## Infrastructure Specifics

### 1. For every additional element, why you are adding it?

- **Firewall**: The firewall is added to secure the network by controlling incoming and outgoing traffic based on predefined security rules. It acts as a barrier between trusted internal networks and untrusted external networks, preventing unauthorized access and attacks.
- **HTTPS**: Adding HTTPS ensures encrypted communication between the server and clients, protecting sensitive data from interception, eavesdropping, and man-in-the-middle attacks.
- **Monitoring Tools**: Monitoring tools are added to observe the performance and health of servers, applications, and services. They provide insights into system behavior, detect anomalies, and alert administrators when issues arise, enabling proactive maintenance and reducing downtime.

### 2. What are firewalls for?

Firewalls are used to **protect the infrastructure** by filtering network traffic based on security policies. They block unauthorized access, prevent data leaks, and mitigate various network-based attacks, such as DDoS, port scanning, or brute-force attacks.

### 3. Why is the traffic served over HTTPS?

Traffic is served over **HTTPS** to ensure secure communication by encrypting data transferred between the user's browser and the server. This prevents:

- **Eavesdropping**: Ensures third parties cannot listen to the communication.
- **Data Integrity**: Ensures that the data is not altered during transit.
- **Authentication**: Verifies the identity of the website, which helps protect against phishing attacks.

### 4. What is monitoring used for?

Monitoring is used to:

- Track system **performance metrics** (CPU, memory, network usage).
- Detect **anomalies** such as high response times, downtime, or failed services.
- **Alert** administrators of potential issues, enabling quick response.
- Provide insights into **resource usage** for capacity planning and scaling decisions.

### 5. How is the monitoring tool collecting data?

Monitoring tools collect data through:

- **Agents** installed on servers, which gather system metrics like CPU, memory, disk usage, and network activity.
- **Logs** from applications, web servers, and databases, which are analyzed to track error rates, request patterns, and performance issues.
- **APIs** that provide metrics on application-specific performance (e.g., request rates, latencies).

### 6. Explain what to do if you want to monitor your web server QPS (Queries Per Second)?

To monitor **QPS (Queries Per Second)** for your web server:

1. **Enable access logging**: Ensure that your web server (e.g., Apache or Nginx) is logging every request.
2. **Use a monitoring tool**: Install a monitoring tool (e.g., Prometheus, Grafana, or Datadog) that can collect and visualize QPS.
3. **Parse log files**: Use tools like `GoAccess` or `AWStats` to analyze the web server logs and calculate QPS.
4. **Set up alerts**: Configure alerts to notify you if QPS exceeds a certain threshold, indicating high traffic or potential issues.

---

## Infrastructure Issues

### 1. Why terminating SSL at the load balancer level is an issue?

- **Issue**: Terminating SSL at the load balancer means that the traffic between the load balancer and backend servers is **unencrypted**. This leaves sensitive data vulnerable to interception within the internal network, especially if the internal network is compromised.
- **Solution**: Use **end-to-end encryption** by ensuring that SSL is terminated at the application server level, with HTTPS used for both client-to-load balancer and load balancer-to-server communication.

### 2. Why is having only one MySQL server capable of accepting writes an issue?

- **Issue**: Having a single MySQL server responsible for all write operations creates a **Single Point of Failure (SPOF)**. If the server goes down, no writes can be performed, leading to downtime and potential data loss.
- **Solution**: Implement a **Primary-Replica** setup or **multi-primary** (multi-master) configuration, where additional MySQL servers can take over write operations in case the primary server fails, ensuring high availability.

### 3. Why having servers with all the same components (database, web server, and application server) might be a problem?

- **Issue**: When all servers have identical components (database, web server, and application server), the infrastructure lacks **separation of concerns**. This makes it harder to scale, optimize, or troubleshoot issues because the servers are overburdened with multiple roles. Additionally, a failure in one component (e.g., the database) could affect the performance of other components (e.g., web application).
- **Solution**: **Decouple the architecture** by using separate servers for each role (e.g., dedicated web servers, application servers, and database servers). This allows independent scaling, better resource allocation, and easier maintenance.
