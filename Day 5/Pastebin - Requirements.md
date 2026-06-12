# Pastebin System Design

## Problem Statement

Design a **Pastebin-like system** where users can create and share text snippets using a short URL.  
The system should support:

- Creating a new paste
- Retrieving a paste using a short link
- Optional expiration of pastes maybe 100 days life time (clean up)
---

## 1) Functional Requirements

- **Create Paste**
  - Content, title, expiry
  - Generate short URL

- **Get Paste**
  - Fetch via short link
  - Respect visibility & expiry (user should be able to private it in that case others should not be able to view it)
  - (optional) Visibility for specifiy users only

- **Delete Paste**
  - By owner

- **Optional**
  - Edit paste by owner only
  - Rate limiting

---

## 2) Non-Functional Requirements

- **Availability:** ~99.9%
- **Low Latency:**  
  - Read < 100 ms (cached)  
  - Write < 300 ms
- **Scalability:** Read-heavy system
- **Durability:** No data loss (replication)
- **Consistency:**  
  - Strong for writes/delete  
  - Eventual for feeds/search
- **Security:** Access control, HTTPS, XSS protection
- **Cost Efficient:** Expire old data (100 days clean up)

---

## 3) Capacity Estimation

### Assumptions
- 10M pastes/month
- Avg size = 10 KB
- Read:Write = 10:1

### Traffic
- Writes: ~40 QPS (peak ~80)
- Reads: ~4000 QPS (peak ~8000)

### Storage

#### Total Writes per Month
- 40 writes/sec × 86400 × 30  
≈ **~103 million writes/month**

#### Monthly Storage
- 103M × 11 KB  
≈ **~1,133,000,000 KB (~1.1 TB/month)**

#### Yearly Storage
- 1.1 TB × 12  
≈ **~13 TB/year**


#### Monthly Reads
- 4000 reads/sec × 86400 × 30  
≈ **~10.4 billion reads/month**

#### Data Transfer
- 10.4B × 10 KB  
≈ **~104 TB/month**

---
