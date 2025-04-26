## Week 5 — Pathfinding, Gossip, and Liquidity Challenges

### 🔹 1. Introduction

_This week we explore how nodes in the Lightning Network find routes for payments without a central coordinator. We’ll study the role of the gossip protocol in maintaining a view of the network, and how liquidity limitations introduce unique challenges compared to traditional networks._

_Focus on understanding that **finding a route** is a local, dynamic, and privacy-conscious activity!_

---

### 📙 2. Core Reading Assignment

- **Chapter 11**: Gossip and the Channel Graph
- **Chapter 12**: Pathfinding and Payment Delivery

---

### 📈 3. Optional Reading Assignment

- Explore liquidity probing techniques and their privacy implications if you are curious.
- Focus mainly on the basics of gossip updates, building the channel graph, and how source-based routing works.

---

### 🔍 4. Self-Study Questions

#### Chapter 11: Gossip and the Channel Graph

1. **How does a Lightning node discover peers and available channels using the gossip protocol?**
2. **What is the channel graph, and why do Lightning nodes need to maintain one?**
3. **What messages constitute the gossip protocol in the Lightning Network?**

#### Chapter 12: Pathfinding and Payment Delivery

1. **Not only successful but also failed payment attempts can reveal information. How could payment failures be abused to infer channel balances, and at what cost?**
2. **What are the benefits and downsides of using source-based onion routing in Lightning, compared to destination-based routing?**
3. **What happens when different nodes use different pathfinding algorithms? How does this affect interoperability?**
4. **Maintaining a full channel graph and performing pathfinding can be expensive. Could third parties help? What would be the privacy and trust implications?**
5. **In what ways does Lightning's pathfinding process rely on the information provided by the gossip protocol?**
