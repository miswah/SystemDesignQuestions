# Notification Service

Design a highly scalable notification service that can deliver messages across multiple channels (Push, Email, SMS, In-App) with very high traffic (up to millions/sec), ensuring reliability, low latency, and user control.

---

## 1. Functional Requirements

- Multi-channel delivery
  - Push notifications (mobile/web)
  - Email
  - SMS
  - In-app notifications

- Event-driven notifications
  - Trigger on user actions (payments, messages)
  - Trigger on system events (fraud alerts, downtime)

- Priority handling
  - Critical (OTP, security alerts)
  - Non-critical (marketing, promotions)

- User preferences
  - Opt-in / Opt-out
  - Channel preferences
  - Quiet hours / DND

- Message templating
  - Dynamic templates (email/SMS)
  - Localization support

- Scheduling support
  - Immediate delivery
  - Delayed / scheduled messages

- Deduplication
  - Prevent duplicate notifications

- Broadcast Campaigns
  - Send to millions of users
---

## 2. Non-Functional Requirements

**Scalability**
- Handle millions to billions of notifications/day
- Support peak load up to 1M notifications/sec
- Horizontal scaling (stateless services + queues)

**Reliability**
- At-least-once delivery for critical notifications
- Ensure no message loss for important alerts

**Fault Tolerance**
- Retry with exponential backoff

**Observability**
- Metrics: throughput, latency, failure rate
- Logging and distributed tracing

---

## 3. Capacity Estimation

**Assumptions**

- Total users: 100 million
- Daily active users: 20 million
- Notifications per user per day: 10

**Traffic Calculation**

```
Total notifications/day = 20M × 10 = 200M

Average QPS = 200M / (24 × 3600)
             ≈ 2,300 requests/sec

Peak traffic factor = 10x

Peak QPS ≈ 23,000 notifications/sec
```

**Extreme Scale Scenario**

- Peak load: 1M notifications/sec
- Daily volume: 10B+ notifications

---

**Storage Estimation**

**Notification Payload**

- Average size: 1 KB

```
Storage/day = 200M × 1 KB = 200 GB/day
Monthly ≈ 6 TB
```

**Including Metadata**

- Approx 2x overhead

```
Total storage/month ≈ 12 TB
```
