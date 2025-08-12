# 📚 Week 1 – Bitcoin as a Language for Financial Contracts

A Bitcoin transaction is used to communicate a payment from one person to another.
Every payment on Bitcoin begins with the creation of a transaction that expresses who is paying, how much is being paid, and under which conditions that payment can be claimed.
In other words, **Bitcoin transactions are programmable contracts**, not just simple messages to transfer value.

These transactions are validated by all participants in the network and, once confirmed by being included in a block, the payment is considered final.
This global validation process means that, even in a payment between just two people, the entire network is involved.
That’s a design feature — Bitcoin’s model assumes that no one is to be trusted, so everyone verifies everything.

But this comes at a cost.
When the whole network is involved, there’s friction: time spent waiting for confirmation, and fees paid to incentivize inclusion in a block.
These constraints — latency and cost — are direct consequences of Bitcoin’s global trustless model.

This is the starting point for our journey.
The Lightning protocol is a particular way we use the Bitcoin protocol under additional trust assumptions we are going to discuss in the following weeks.
To understand the Lightning Network, we must first understand the structure and flow of Bitcoin payments on the base layer, and how these design choices create both security and scalability challenges.

Focus on the **concepts of UTXOs, scripts, and Bitcoin as a contract language**.

---

### 📙 Core Reading Assignment

You might be tempted to think you already understand how Bitcoin works and skip this week's readings.
Trust me, you probably don't understand Bitcoin transactions well enough to understand the Lightning protocol.
I dare say 80% of Lightning is dealing with Bitcoin transactions.
There's no way to understand it without becoming fluent in the language of Bitcoin transactions.

1. Antonopoulos et al, [Mastering the Lightning Network](https://github.com/lnbook/lnbook) -  **Appendix A**: Bitcoin Fundamentals Review.

2. Antonoupolos, [Mastering Bitcoin](https://github.com/bitcoinbook/bitcoinbook) - **Chapter 6**: Transactions and **Chapter 7**: Authorization and Authentication.

3. James Prestwich, [Bitcoin’s Time Locks](https://medium.com/summa-technology/bitcoins-time-locks-27e0c362d7a1).

4. Antonopoulos et al, [Mastering the Lightning Network](https://github.com/lnbook/lnbook) - Chapter 3**: How the Lightning Network Works

4. Christian Decker, [Lightning ≈ Bitcoin](https://youtu.be/8lMLo-7yF5k?si=YxvVLKmz8zFoj0yU)

---

### 📈 Optional Reading Assignment

- Poon and Dryja, [The Bitcoin Lightning Network: Scalable Oﬀ-Chain Instant Payments](https://lightning.network/lightning-network-paper.pdf).

The academic paper that introduced the idea of the Lightning Network, if you are feeling adventurous.
On the first reading, note that all they are talking about are Bitcoin transactions and specific contracts (`scriptPubkey`s). 

- Christian Decker - [History of the Lightning Network](https://youtu.be/HauP9F16mUM?si=ZeH1dlpTf3vuSZRw)

- Curiousinventor - [Bitcoin Lightning Network Explained: How it Actually Works](https://www.youtube.com/watch?v=yKdK-7AtAMQ&list=PLUr_dJkzOLr83CRbuevW4I5CpFFth5Cbm&index=6)

- Curiousinventor - [Bitcoin Lightning Transactions & Protocol Deep Dive](https://www.youtube.com/watch?v=to8XItlplac)

---

### 🔍 Self-Study Questions

1. What are the parts of a Bitcoin transaction?
2. What's an UTXO? Why it's fundamental to Bitcoin's model?
3. Describe locking and unlocking scripts and explain their role within Bitcoin transactions.
4. Suppose someone created a transaction with a 1 BTC output locked by a p2pkh contract. Who's the owner of this 1 BTC? What data he must present to spend his 1 BTC?
4. Describe a 2-of-2 multisig contract (locking script) using Bitcoin Script. Describe the spending script for this contract.
5. How can an UTXO be locked to a secret? Why are cryptographic hashes used for this technique?
6. What kinds of time locking mechanisms exist (absolute and relative) and how are they used?
7. Example A-1 of the Mastering the Lightning Network book shows an example of a conditional contract, i.e., a contract with different spending paths. How many conditions there are in this contract? What data must be provided to satisfy the conditions of each spending path in this contract?
