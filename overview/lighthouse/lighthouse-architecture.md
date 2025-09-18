# Lighthouse Architecture

There are two primary interfaces:

* **User Interface (UI):** Manage deposits/withdrawals, track live auctions, and view system statistics.
* **API:** Provide data queries and integration endpoints for developers and advanced users.

***

<figure><img src="../../.gitbook/assets/image (48).png" alt=""><figcaption><p><strong>Figure 4. Lighthouse Architecture</strong></p></figcaption></figure>

Lighthouse achieves robustness, stability, and performance by leveraging core components of Kubernetes (Ingress, Service, Deployment), a log monitoring system (ELK), and a message broker:

* **Event Processing:** The Lighthouse server asynchronously publishes all events to a message broker, ensuring that its core logic remains performant. A Kubernetes-based API server subscribes to these events, recording them in both database and the log monitoring system, respectively.
* **Quick Recovery:** Log and data enables rapid state restoration and operational continuity in the event of failure.
* **Role Separation:** The API server separates user-facing requests from core server logic, improving both robustness and scalability.
* **High Availability:** Lighthouse runs in a Kubernetes environment with autoscaling, periodic health checks, and zero-downtime deployments to maximize service reliability.

