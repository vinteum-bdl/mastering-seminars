## Week 4 — Routing with Conditional Payments: HTLCs and Atomicity

### 🔹 1. Introduction

_This week we explore how Lightning enables payments across multiple hops, ensuring fairness and atomicity at every step. We'll study how Hash Time Locked Contracts (HTLCs) allow trustless routing and protect participants from fraud._

_You’ll see that routing a payment isn't magic — it's about carefully chained conditional agreements enforced by Bitcoin transactions!_

---

### 📙 2. Core Reading Assignment

- **Chapter 10**: Onion Routing

---

### 📈 3. Optional Reading Assignment

- For enthusiasts: Explore how keysend payments extend standard HTLC logic.
- Focus mainly on understanding source routing, onion construction, and hop-by-hop encryption.

---

### 🔍 4. Self-Study Questions

#### Chapter 10: Onion Routing

1. **When you send a Lightning payment through multiple nodes, what kind of information could intermediaries potentially learn if no privacy protections were in place?**
2. **Why can't we rely on encryption alone to protect privacy in Lightning routing?**
3. **How does onion routing protect the privacy of the sender and receiver during Lightning payments?**
4. **What prevents an intermediary node from tampering with or altering the forwarding instructions in a Lightning onion packet?**
5. **If you think about the sender, the intermediaries, and the receiver, who knows what in a properly onion-routed Lightning payment?**

