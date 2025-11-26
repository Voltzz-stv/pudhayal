YT - https://youtu.be/eNwbZz8PGDc?si=ORRnXcjBmtR0Hlga

The vid was java based, get answers for js

The sources provided cover four main scenario-based microservices interview questions, along with comprehensive solutions for each.

Here are the questions and their corresponding answers:

---

### Scenario 1: Handling Failures and Ensuring Data Consistency in Synchronous Communication

**The Question:** If you have multiple microservices (A, B, and C) communicating synchronously via REST API, and a service in the middle of the request chain (B) fails, how would you handle the failure recovery and ensure data consistency?

**The Answer (Solutions using Resilience Patterns):** Failure recovery in a synchronous communication chain can be handled using resilience patterns.

1. **Circuit Breaker Design Pattern**:
    
    - **Purpose:** This pattern prevents the system from repeatedly calling a service that is failing. If a microservice (like B) is failing, repeated calls will further slow down the response to the client.
    - **Mechanism:** It acts like a safety switch. If the service is failing or too slow, the circuit breaker **opens**, stopping repeated calls to the failing service. This prevents overloading the failing service and gives it time to recover (e.g., time for the Kubernetes pod to restart). Once the service is deemed healthy again, the circuit breaker **closes**, allowing traffic to flow again.
    - **Tool/Implementation:** Use **Resilience4j Circuit Breaker**. Implement using the `@CircuitBreaker` annotation on the particular service (e.g., Order Service) and specify a **fall back method**.
2. **Retry Mechanism**:
    
    - **Purpose:** Use for **temporary or intermittent failures** (e.g., a pod being temporarily down due to network issues or latency).
    - **Mechanism:** Instead of immediately hanging up, the system automatically tries to make the request again after a brief delay. It works well when a short delay allows the temporary issue to resolve.
    - **Implementation Note:** Make sure not to retry hundreds of times, as this slows down the process. Use **Spring Retry** with the `@Retryable` annotation, often including **Exponential Backoff** to increase the delay between attempts.
3. **Set Timeouts**:
    
    - **Purpose:** To avoid **blocking the request chain**. If microservice B is unresponsive or too slow, it can prevent service A from giving a timely response back to the client.
    - **Mechanism:** Timeouts set a waiting limit; if the service does not respond within that time, the request is aborted. This prevents other systems from getting stuck.
    - **Implementation Note:** Configure REST API clients or HTTP components with connection timeouts and read timeouts.
4. **Fallback Mechanism and Caching**:
    
    - **Purpose:** When a service fails, send a default or a cached response back to the client. This prevents showing an error or a blank screen, improving user experience.
    - **Mechanism:** Store the recent successful response in a cache (e.g., **Redis**) and serve that cached data when the service is down.
    - **Constraint:** This can only be done where real-time data is not critically needed (e.g., showing a last known weather report, but not inventory levels).
5. **Move to Asynchronous Communication**:
    
    - **Purpose:** To avoid cascading failures. If the request is non-critical (like sending notifications), you can use asynchronous communication.
    - **Mechanism:** Use message brokers like **Kafka, RabbitMQ, or ActiveMQ** instead of synchronous REST APIs.
    - **Constraint:** This is not always possible (e.g., payments should be synchronous).

---

### Scenario 2: Distributed Transactions and Data Consistency

**The Question:** You have an e-commerce application with Order Service, Payment Service, and Inventory Service. An order should be successful only if both the Payment and Inventory are updated successfully. Otherwise, you must cancel the order. How would you ensure the order is successful only upon successful updates to Payment and Inventory?

**The Answer (Solutions for Distributed Transactions):** This scenario requires managing distributed transactions and data consistency.

1. **Saga Design Pattern (Recommended)**:
    
    - The Saga pattern ensures atomicity by using compensating transactions if any step fails.
    - **Approach A: Orchestration**:
        - **Control:** Centralized.
        - **Mechanism:** A central place called the **orchestrator** controls the entire flow. It starts the process and tells each service (Inventory, Payment, Shipping) sequentially what to do.
        - **Failure Handling:** The orchestrator manages centralized retries and errors.
    - **Approach B: Choreography**:
        - **Control:** Decentralized.
        - **Mechanism:** There is no central controller. Services listen for events published by other services (e.g., Payment Service publishes a "Payment Completed" event) and react to them independently. This results in loosely coupled microservices.
        - **Failure Handling:** Each service handles its own errors.
2. **Outbox Pattern**:
    
    - **Purpose:** Acts as a safety net to ensure an order event is sent only after all necessary tasks (like Inventory and Payment updates) are successfully completed, preventing inconsistencies.
    - **Mechanism:** A dedicated **Outbox Table** stores events (like "Order Created") that need to be sent to other services. This event recording happens within the **same transaction** as the primary service operation. A background worker (like **Debezium**) regularly checks this table and sends the events, typically via Kafka.
    - **Advantage:** Prevents event loss and ensures consistency. It also ensures exactly-once delivery of the order event.
3. **Idempotency**:
    
    - **Purpose:** To prevent duplicate orders, especially when retry mechanisms are used.
    - **Mechanism:** Use an **Idempotency Key** to check if a transaction is already present before processing it.
4. **Dead Letter Queue (DLQ)**:
    
    - **Purpose:** Prevents message loss for failed messages.
    - **Mechanism:** A specialized queue where messages that failed multiple processing attempts (e.g., three retries) are sent. The DLQ holds these failed messages, allowing for later troubleshooting, manual retries, or sending notifications to users.
    - **Implementation:** Message brokers like **Kafka** and **RabbitMQ** support Dead Letter Queues.

---

### Scenario 3: Security, Rate Limiting, and Validation at the Entry Point

**The Question:** Your application exposes multiple microservices to the outside world. How would you ensure security, rate limiting, and request validation at the entry point itself?

**The Answer (Implementation at the API Gateway):** These mechanisms should be implemented at the **API Gateway level**, which serves as the entry point for external traffic.

1. **Security (Authentication)**:
    
    - **Mechanism:** Implement cloud-level or API Gateway security using **JWT Tokens**.
    - **Implementation Note:** Use **JWT Authentication Filters** at the Gateway level.
2. **Rate Limiting**:
    
    - **Purpose:** To prevent the system from being overwhelmed or bombarded by thousands of unnecessary requests (which can cause performance degradation or system crashes).
    - **Mechanism:** Use tools like **Bucket4j** to throttle requests based on the IP or user. **Redis** is used to track how many requests a specific user or IP address has made. You can set a **replenish rate** (e.g., 10 requests per second) and a **burst capacity** (e.g., maximum 20 requests). Requests exceeding the limits are blocked.
3. **Request Validation**:
    
    - **Purpose:** To ensure incoming requests are correct before they navigate through multiple microservices, avoiding useless processing of bad requests.
    - **Mechanism:** Use **Spring Validations** (e.g., `@Valid`, `@NotNull`) or interceptors in Spring Boot to validate input parameters like email formats, minimum/maximum size, and null checks.
    - **Implementation Note:** Use **Request Validation Filters** at the Gateway level.

---

### Scenario 4: Securing Inter-Service Communication

**The Question:** When security is applied at the API Gateway level for external requests, how would you still secure your inter-service communication (e.g., how should Order Service and Payment Service validate each other)?

**The Answer (Solutions for Internal Traffic Security):** Securing internal traffic within a microservice architecture requires a different approach than external security.

1. **Mutual Service-to-Service Authentication (mTLS)**:
    
    - **Mechanism:** Both communicating services (A and B) verify each other’s identity by presenting their certificates. This establishes a mutual trust before allowing the connection.
    - **Implementation Note:** Can be enabled using **OpenSSL** to create and share certificates.
2. **Service Mesh**:
    
    - **Purpose:** A dedicated infrastructure layer to handle complex service-to-service communication issues, including security.
    - **Mechanism:** Microservices do not talk directly to each other but communicate through the service mesh (e.g., **Istio or Linkerd**), which manages how traffic is secured.
3. **OAuth 2.0 / JWT**:
    
    - **Mechanism:** Implement identity providers (like **Octa, Keycloak, or Auth0**) at the individual service level to handle authentication for internal calls.
4. **API Gateway Routing**:
    
    - **Mechanism:** Route all internal requests (e.g., A to B) through the API Gateway, centralizing security checks for inter-service calls.
5. **Shared Secrets (API Keys)**:
    
    - **Mechanism:** Services share secret keys and send them in the request headers to validate that the other service is authorized.