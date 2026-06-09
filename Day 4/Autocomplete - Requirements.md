# Autocomplete (Typeahead) System

## 1. Functional Requirements

### Core Features
- **Real-time Suggestions**
  - Provide suggestions as user types (per keystroke or debounced input)
  - Latency target: < 100 ms end-to-end per query

- **Prefix-based Search**
  - Return suggestions that match given prefix
  - Example:
    - Input: "ap"
    - Output: ["apple", "application", "april"]

- **Ranking & Relevance**
  - Rank suggestions based on:
    - Popularity (global frequency)
    - Recency (trending queries)
    - Personalization (user history)

- **Top-5**
  - Return top 5 suggestions
---

## 2. Non-Functional Requirements

- **Low Latency**
  - P95 latency: **< 100 ms**
  - Backend latency: **< 20–30 ms**

- **High Availability**
  - Uptime: **≥ 99.99%**
  - No single point of failure

- **Scalability**
  - Handle:
    - **100K – 300K RPS**
  - Support:
    - **10M+ active users**

- **Consistency**
  - Eventual consistency for updates is acceptable

- **Read Optimization**
  - Highly optimized for read-heavy workloads

---

## 3. Traffic & Capacity Considerations

### Assumptions
- Read-heavy system:
  - Each keystroke triggers a request
- Average query length:
  - 5–10 characters → multiple requests per search session

---

### Example Scale (Mid-Large System)

#### Incoming Traffic
- Daily Active Users (DAU): 10M  
- Avg searches/user/day: 5  
- Avg keystrokes per search: 8  

Total queries/day = 10M × 5 × 8 = 400M


Average RPS ≈ 400M / (24 × 3600) ≈ 4,600 RPS
Peak RPS ≈ 5–10x → 25K – 50K RPS
Burst RPS ≈ 100K+