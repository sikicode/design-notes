## Design Rate Limiter
### Why do we use rate limiter
- Prevent resource starvation: DDOS attacks
- Manage policies and quotas: time duration/quantity limit
- Control data flow: avoid burdening one single machine (distribute date evenly)
- Avoid excess costs: provide freemium services to certain limits
### Functional Requirements
- Limit # of requests a client can send to an API within a time window
- Make each limit configurable
- Notify user when threshold is crossed
### Non-functional requirements
- High Availability 
- Low Latency
- Scalability
### 