# Rate Limiter

## 1. Functional Requirements

### Core Features
- **Request Throttling**
  - Limit number of requests per client (user/IP/API key)
  - Example:
    - 100 requests/min per user
    - 1000 requests/min per API key
  - Configurable time windows: per second / minute / hour  

- **Multiple Limit Dimensions**
  - Per-user, per-IP, per-endpoint limits
 
- **Rate Limiting Algorithms**
  - Ability to switch/extend algorithms  

- **Dynamic Configuration**
  - Update rate limits without restart  

- **Response Handling**
   - with correct http headers

- **Distributed Enforcement**
    - Distributed system is not required but a plus point 

- **Burst Handling**
  - Allow bursting:
    - e.g., 100 req/min + burst of 20 requests  
  - Support:
    - Hard throttling (reject)
    - Soft throttling (allow slight exceed)
    - Dynamic throttling based on system load  

---

## 2. Non-Functional Requirements

- **Low Latency**
  - Overhead per request: **< 5–10 ms**  
  - Should not degrade API SLA  

- **High Availability**
  - Uptime: **≥ 99.99%**  
  - No single point of failure  

- **Scalability**
  - Support:
    - **100K – 500k+ RPS**  
  - Handle **1M+ active users**  

---

## 3. Traffic & Capacity Considerations

### Assumptions
- Write-heavy system:
  - Every request updates counter  
- High cardinality:
  - Millions of unique keys (user/IP)  

---

### Example Scale (Mid-Large System)

#### Incoming Traffic
- **Average RPS:** 100K  
- **Peak RPS:** 500K  
- **Burst RPS:** 1M  

---

#### Storage Estimation

- Data per key:
  - UserID → 8 bytes  
  - Counter → 4 bytes  
  - Timestamp → 8 bytes  
  - Overhead → ~20 bytes  
  - **Total ≈ 40 bytes per key**

- Active keys:
  - 10M users  

- **Memory Required:**
```
10M × 40 bytes ≈ 400 MB
```

---

#### Throughput Estimation
- Each request:
  - 1 read + 1 write → 2 ops  

- At 500K RPS:
```
