## Week 1 — Bitcoin as a Contract Language

### 🔹 1. Introduction

_This week we start by understanding the foundation of Bitcoin and why transactions are better thought of as programmable contracts rather than simple payments. We also introduce the Lightning Network at a high level and prepare to see it as a system grounded in Bitcoin’s transaction model._

_Focus on the **concepts of UTXOs, scripts, and Bitcoin as a contract language**. Don’t worry yet about full technical mastery — aim for clear mental models._

---

### 📙 2. Core Reading Assignment

- **Appendix A**: Bitcoin Fundamentals Review
- **Chapter 2**: Getting Started
- **Chapter 3**: How the Lightning Network Works

---

### 📈 3. Optional Reading Assignment

- _None for this week._
  (All assigned reading is important for grounding.)

---

### 🔍 4. Self-Study Questions

#### Appendix A: Bitcoin Fundamentals Review

1. **Define a UTXO and explain why it's fundamental to Bitcoin's model.**
2. **Describe locking and unlocking scripts and explain their role within Bitcoin transactions.**
3. **How can a UTXO be locked to a secret? Why are cryptographic hashes important for this technique?**
4. **What kinds of time locking mechanisms exist (absolute and relative) and how are they used?**
5. **Analyze Example A-1. What data must be provided to satisfy the conditions of the script?**

#### Chapter 2: Getting Started

1. **Analyze the functions a Lightning wallet must perform. How does it differ from a Bitcoin wallet? In what ways is the term "wallet" helpful or misleading for new users?**
2. **List and explain the steps needed to join the Lightning Network and start making and receiving payments. Which steps depend on Bitcoin layer actions?**
3. **Some critics argue Lightning is not truly Bitcoin. What are their arguments? How does understanding the protocol help you evaluate this claim?**

#### Chapter 3: How the Lightning Network Works

1. **Describe the Lightning Network as a system of payment channels. What elements are required to build a functioning Lightning Network? Is there a single global Lightning Network?**
2. **Which aspects of Lightning are publicly visible and which are private? Suggest ways privacy could be improved.**
3. **What data must a Lightning node maintain to operate safely and route payments? How does this burden change as the network grows?**
4. **Why is it difficult to revoke an old Bitcoin transaction? Why can't Lightning channels simply invalidate old channel states?**
5. **Compare a Bitcoin address and a Lightning Network payment invoice. What different security assumptions underlie each method?**
