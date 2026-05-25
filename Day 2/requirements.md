# Load Balancer

## 1. Functional Requirements

### Core Features
- **Traffic Distribution**
  - Route incoming requests to backend servers
  - Support algorithms: Round Robin, Least Connections, Weighted Clarify how to change algorithm on fly

- **Health Checks**
  - Periodically check backend health (HTTP/TCP)
  - Remove unhealthy instances and re-add when recovered

- **Failover**
  - Automatically reroute traffic if a backend fails
  - Support multiple LB instances (HA)

- **Observability Hook**
  - Collect metrics: latency, error rate, traffic distribution

---

## 2. Non-Functional Requirements

- **Low Latency**
  - Minimal added overhead per request

- **High Availability**
  - ≥ 99.99% uptime
  - No single point of failure

- **Scalability**
  - Handle high RPS and concurrent connections
  - Horizontal scaling of LB nodes

### Reliability
- Graceful handling of backend failures
- No request loss during failover

### Performance
- Efficient connection handling (keep-alive, pooling)

### Security
- TLS support, basic DDoS protection

---

## 3. Traffic & Capacity Considerations

### Assumptions
- Read-heavy traffic (most requests are routing/forwarding)
- Millions to billions of requests per day

### Per-Second Load (Example)
- **Incoming Requests**
  - ~10K–1M+ RPS depending on scale

- **Backend Connections**
  - High concurrent connections requiring efficient pooling