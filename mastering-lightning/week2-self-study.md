# 📚 Week 2 — Lightning Channels as Systems of Bitcoin Transactions

Last week you saw that the most important piece of the Bitcoin protocol is the concept of Bitcoin transactions.
Each transaction represents money being spent (its inputs) and money being received (its outputs).

More precisely, there is no notion of "receiving money" in the protocol — that’s how humans interpret Bitcoin transactions.
What actually exists are contracts (`scriptPubKey`) written into transaction outputs, which lock a certain `amount` of bitcoin.
These outputs are intended to be used later as inputs to another transaction.
While this hasn’t happened yet, we call the output a **UTXO** (Unspent Transaction Output).

To spend a UTXO, a new transaction must include a reference to it (`txid` and `index`) and present the required data to fulfill the contract (`scriptSig`).
This data often includes a digital signature and other information, such as a public key or a preimage.

In the standard Bitcoin payment flow, valid transactions are eventually confirmed by being included in a block.
Each transaction must include fees to incentivize miners to confirm them.
This introduces costs in terms of:

- Throughput: limited number of transactions per block;
- Confirmation delay: time until inclusion in a block;
- Fees: paid to compete for block space;
- Privacy leakage: since everyone sees and verifies every transaction;

Bitcoin is designed to work without trust — no need to believe your counterparty is honest.
These costs have to be paid for the security guarantees provided by the Bitcoin network.
But if both parties do trust each other (at least temporarily), they can avoid some of Bitcoin’s costs by skipping global validation.
The challenge is to create a setup in which either party can unilaterally exit and reclaim their funds if trust breaks down.

This week, we explore how two parties can create a **payment channel** using Bitcoin transactions.
The goal is to coordinate a secure deposit (on-chain) and design a mechanism for tracking updates (off-chain) while allowing either party to cash out (on-chain) at any moment — safely and independently.

The key conceptual insight is this: **a Lightning channel is a set of Bitcoin transactions** that are coordinated off-chain under mutual agreement.
These transactions define how funds are allocated, updated, and eventually settled on-chain.

Participants should begin to understand:

- What kinds of Bitcoin transactions are required to create a Lightning channel;
- The role of funding and commitment transactions, and why commitment transactions are asymmetric;
- How trust assumptions shift: we assume cooperation off-chain, but ensure that unilateral exit via on-chain enforcement is always possible;
- That the Lightning protocol doesn’t invent new money or mechanisms — it arranges the use of Bitcoin transactions under disciplined rules for coordination.

With this foundation, we prepare to explore how channels are updated over time and used to route payments in a scalable, privacy-conscious way.

---

### 📙 Core Reading Assignment

1. Antonopoulos et al, [Mastering the Lightning Network](https://github.com/lnbook/lnbook) -  **Chapter 3**: How the Lightning Network Works.

2. Antonopoulos et al, [Mastering the Lightning Network](https://github.com/lnbook/lnbook) -  **Chapter 7**: Payment Channels.

Pay special attention to how the funding and commitment transactions are built.
This week we are not intereted in how the channel state is updated.

3. Federico Tenga, [Understanding Payment Channels](https://blog.chainside.net/understanding-payment-channels-4ab018be79d4)

4. Elle Mouton, [LN Things Part 1: Creating a channel](https://ellemouton.com/posts/creating-a-channel/)

5. James C., [Bitcoin Protocol Design: Payment Channels Revisited](https://www.youtube.com/watch?v=4SdBa8ZOfqg)

---

### 📈 Optional Reading Assignment

- Christian Decker - [History of the Lightning Network](https://www.youtube.com/watch?v=HauP9F16mUM)

- [A Brief History of Payment Channels: from Satoshi to Lightning Network](https://old.reddit.com/r/Bitcoin/comments/cc9psl/technical_a_brief_history_of_payment_channels/)

- [Lightning transactions: from Zero to Hero](https://github.com/t-bast/lightning-docs/blob/master/lightning-txs.md)

- [BOLT 3: Bitcoin Transaction and Script Formats](https://github.com/lightning/bolts/blob/master/03-transactions.md) - Try to get a feel for how the scripts are used, don't bother understanding all the nitty-gritty.

---

### 🔍 Self-Study Questions

1. How does the Lightning Network aim to change the way people exchange value online, and what opportunities does it provide to Bitcoin?
2. Explain the concept of a "fairness protocol" and its importance as the backbone of decentralized systems like Bitcoin and the Lightning Network. How does Lightning achieve "fair outcomes without a central authority"? What role do incentives and disincentives play?
3. Differentiate between "on-chain" and "off-chain" payments. What is usually the only type of transaction recorded on the Bitcoin blockchain in the context of the Lightning Network?
4. Why is avoiding on-chain confirmations during payments a key goal for payment channels?
5. What is the "financial relationship" a Lightning payment channel represents, and how is the balance allocated?
6. What limitations restrict a channel?
7. What are some useful properties of payments made within a payment channel regarding privacy and settlement?
8. How is a payment channel initiated and "anchored" to the Bitcoin blockchain?
9. What specific type of Bitcoin contract is used for the funding transaction?
10. Can we just send funds to the funding transaction script? What problem does this pose, and how does the protocol address it?
11. Why must the funding transaction be confirmed on-chain to open a Lightning channel? What risks would arise if it stayed off-chain?
12. What is a "dual-funded channel," and what is its current status in Lightning implementations?
13. Explain the purpose of "commitment transactions" in managing the channel balance off-chain.
14. Describe the ways a payment channel can be closed. Which is preferred, and why might the others be necessary?
15. What are the implications and costs of a "force close" compared to a "collaborative close"?
16. Ideally, you only see two on-chain transactions over the lifetime of a payment channel, one to open the channel and one to close it. How does this reflect the efficiency goal of payment channels?

When answering these questions, focus on how to construct valid Bitcoin transactions and which information is needed by each party.
