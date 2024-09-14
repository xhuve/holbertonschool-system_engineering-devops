# Web Infrastructure

## Infrastructure Specifics

### 1. What is a server?

Any computer or system that fulfills the role of providing resources, data, services, or programs to other computers (clients) over a network can be called a server. When talking about a web infastructure we can come across a OS server, which hosts the operating system wherein all the necessary files and program host and manage the server (Linux server, Windows server, etc), or a web server which hosts all our web files and provides them when a request is made on a certain port (Apache server, Ngnix server).

### 2. What is the role of the domain name?

A domain name is a human-readable address (e.g., `foobar.com`) that is mapped to an IP address where the website or service is hosted. It makes it easier for users to access websites without needing to remember numerical IP addresses of the servers.

### 3. What type of DNS record is `www` in `www.foobar.com`?

The `www` in `www.foobar.com` is typically an **A (Address) record** or **CNAME (Canonical Name) record**:

- **A Record**: Directly maps a domain name to an IP address.
- **CNAME Record**: Maps one domain name (e.g., `www.foobar.com`) to another domain name (e.g., `foobar.com`), which in turn points to an IP address.

### 4. What is the role of the web server?

The web server (such as Apache or Nginx) handles HTTP/HTTPS requests from users and serves static content (HTML, CSS, JS, images) or forwards dynamic requests to the application server. It processes incoming requests and returns the appropriate web pages.

### 5. What is the role of the application server?

The application server runs the business logic of the web application. It processes dynamic requests, interacts with the database, and generates the appropriate responses. For example, it runs server-side code (in languages like PHP, Python, Java, etc.) to produce dynamic content for the user.

### 6. What is the role of the database?

The database stores and manages the application’s data (e.g., user information, product catalogs). The application server interacts with the database to retrieve, modify, or delete data as required by the application logic. The database can hosted either as its own independent server, or can be run alongside other servers within one OS server

### 7. What is the server using to communicate with the computer of the user requesting the website?

The server communicates with the user’s computer via the **HTTP/HTTPS protocol** over the internet. When a user requests a webpage, the client (browser) sends an HTTP/HTTPS request to the server, which then sends back the requested data as an HTTP/HTTPS response.

---

## Infrastructure Issues

### 1. Single Point of Failure (SPOF)

- **Issue**: If a single server or component (e.g., a web server, database server) fails, the entire system can go down. This creates a **single point of failure (SPOF)**. If there’s no redundancy or failover mechanism, the system becomes unreliable.

### 2. Downtime when maintenance is needed (e.g., restarting web server for code deployment)

- **Issue**: When the web server or application server needs to be restarted during updates or code deployments, the website can experience downtime. This leads to service interruptions for users during maintenance periods.

### 3. Cannot scale with too much incoming traffic

- **Issue**: If the infrastructure is not designed to handle large amounts of traffic, it can become overloaded, leading to slow performance or even crashing. A single server may not have enough resources (CPU, RAM, bandwidth) to serve all the incoming requests during traffic spikes.

---

## Solutions to the Issues

1. **Eliminating SPOF**:

   - **Solution**: Introduce redundancy by having multiple web servers, application servers, and databases. Load balancers can distribute traffic among servers, ensuring that if one server fails, others can take over seamlessly.

2. **Avoiding downtime for maintenance**:

   - **Solution**: Implement **blue-green deployment** or **rolling updates**, where new versions of the application are deployed to a subset of servers first. This allows you to gradually roll out updates without taking the entire system offline.

3. **Handling increased traffic**:
   - **Solution**: Use **horizontal scaling** by adding more servers to distribute traffic. Implement **auto-scaling** systems that can dynamically add or remove servers based on traffic demand. Additionally, use **caching** to offload static content and improve response times for users globally.
