## Week 3 — Routing and Payment Forwarding

### 🔹 1. Introduction

_This week we dive into how Lightning payments actually travel across the network. We'll explore the distinction between routing and pathfinding, the structure and purpose of HTLCs, and how local channel updates allow global payment flows._

_Focus on understanding that routing is not magic — it’s the careful linking of conditional payments across independent channels!_

---

### 📙 2. Core Reading Assignment

- **Chapter 8**: Routing on a Network of Payment Channels
- **Chapter 9**: Channel Operation and Payment Forwarding

---

### 📈 3. Optional Reading Assignment

- Skim detailed script examples if you feel overwhelmed.
- Focus mainly on the concepts of pathfinding, routing, HTLC conditions, and payment forwarding logic.

---

### 🔍 4. Self-Study Questions

#### Chapter 8: Routing on a Network of Payment Channels

1. **Distinguish routing from pathfinding in Lightning. Who performs each task, and which one scales the network?**
2. **How does the Lightning Network route payments across multiple channels without requiring global coordination?**
3. **What is an HTLC and how does it ensure fairness and atomicity in Lightning payments?**
4. **Analyze the HTLC script in Example 8-1. How does it enforce payment conditions using hashes and timelocks?**
5. **In the A -> B -> C -> D payment path, what risks or consequences arise if Carole reveals the payment preimage to Alice before Bob? Why would she need to reveal it to Bob at all?**
6. **What is signature binding in the context of HTLCs, and why is it necessary for Lightning’s security?**

#### Chapter 9: Channel Operation and Payment Forwarding

1. **Why are HTLCs used even for local (non-routed) Lightning payments?**
2. **Outline the steps involved in making a local Lightning payment using HTLCs.**
3. **If an in-flight HTLC expires while the counterparty is offline, what risks exist and what actions should the online peer take?**
4. **What are the possible spending paths for an HTLC output? In each path, who can claim the funds and under what conditions?**
5. **In a Lightning channel funded by Alice, can Alice send HTLCs to Bob, and can Bob send HTLCs to Alice? Explain why or why not.**
