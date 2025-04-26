## Week 2 — Lightning Channels as Systems of Bitcoin Transactions

### 🔹 1. Introduction

_This week we focus on understanding what a Lightning payment channel actually is: a structure built from Bitcoin transactions. We explore how channels are opened, how balances are managed, and why secure coordination between peers is crucial._

_Lightning channels allow frequent off-chain payments while preserving the security model of Bitcoin's base layer. Master the core architecture before worrying about advanced use cases!_

---

### 📙 2. Core Reading Assignment

- **Chapter 6**: Lightning Network Architecture
- **Chapter 7**: Payment Channels

---

### 📈 3. Optional Reading Assignment

- Skim deeper technical details about network stack transport options (e.g., different types of network I/O protocols) if curious.
- Focus mainly on the architecture overview and payment channel fundamentals.

---

### 🔍 4. Self-Study Questions

#### Chapter 6: Lightning Network Architecture

1. **Explain the purpose of each protocol layer in the Lightning Network. Can parts of the architecture be implemented differently while maintaining compatibility?**
2. **Compare the Lightning Network’s layered architecture to that of the internet. What general benefits does layering provide in network design?**
3. **Why does the Lightning Network support multiple network transport protocols at the connection layer? What are the benefits of this flexibility?**

#### Chapter 7: Payment Channels

1. **Define a Lightning payment channel in terms of Bitcoin transactions. What key information about the channel must both participants track?**
2. **Describe the protocol steps to open a payment channel. Which Bitcoin transactions must be created, signed, and broadcast?**
3. **When sending a payment across a Lightning channel, what happens to the Bitcoin transactions underlying the channel?**
4. **Explain why commitment transactions are asymmetric between peers. What problem does this asymmetry solve?**
5. **Why must the funding transaction be confirmed on-chain to open a Lightning channel? What risks would arise if it stayed off-chain?**
6. **What is a channel state? How do peers manage and agree on updates to the channel state over time?**
7. **How do two peers cooperatively close a Lightning channel? What happens to the underlying Bitcoin transactions during a cooperative close?**
8. **What happens if a peer closes a channel unilaterally while there are unsettled HTLCs? How is each pending payment resolved?**
