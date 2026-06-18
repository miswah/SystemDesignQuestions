# Facebook Like Button

## 1. Functional Requirements

### Core Features
- **Like a post**
  - `likePost(userId, postId)`
- **Unlike a post**
  - `unlikePost(userId, postId)`
- **Check if a user liked a post**
  - `isLiked(userId, postId) → boolean`
- **Get total like count**
  - `likesCount(postId)`
- **Idempotency**
  - Multiple clicks should not create duplicate likes
---

### Optional Functional Features
- Show list of users who liked (paginated)
- Notifications
  - Notify post owner when someone likes their post
- Analytics
  - Use likes for ranking / engagement signals

---

## 2. Non-Functional Requirements

**Performance & Latency** 
- Like action latency: **<100–200 ms**

**Scalability**
- Must support **billions of users**
- Handle **tens of thousands of writes/sec**

**Availability**
- Target: **99.99% uptime**
- System should degrade gracefully (likes shouldn't block feed)

**Consistency**
- **Strong consistency acceptable**
  - No delay in like counts
- **Read-after-write consistency for user**
  - User should immediately see their own like

**Throughput Characteristics**
- Highly **read-heavy system**
  - Reads >> Writes

---

## 3. Estimates (Realistic Scale)

**Traffic Estimates**
- Total likes/day: **~5 billion**
- Likes/sec: ~60,000 likes/sec
- 50K–70K write QPS

**Read vs Write Ratio**
- **Read:Write = 100:1**
---

### Data Storage

**Like Record Size**
- userId (8 bytes)
- postId (8 bytes)
- timestamp (8 bytes)

Total:
- **~24–32 bytes per like**

---

**Storage Growth**
- Daily:
  - ~150 GB raw data
- Yearly:
  - **~200–300 TB**

---