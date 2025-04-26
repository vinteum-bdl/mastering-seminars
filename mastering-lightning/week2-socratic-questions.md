# 📚 Week 2 – Socratic Questions
**Theme:** Lightning Channels as Systems of Bitcoin Transactions

### Question 1
> **If Bitcoin transactions are contracts, what might we need to create if two people want to keep exchanging value between themselves without publishing every change to the blockchain?**

**Purpose:**
- Guide students toward **off-chain agreements** as a solution to inefficiency.
- Seed the concept of **payment channels**.

**Example of Good Expected Answer:**
> If every change in balance had to be recorded on-chain, it would be slow, expensive, and expose private transaction details. To avoid this, two people could create an initial transaction locking funds under shared control, and then exchange signed but unpublished updates that redistribute those funds between them. This would allow them to transact many times off-chain, only resorting to the blockchain if there is a dispute or if they want to close the relationship.

### Question 2
> **What role does the funding transaction play when opening a Lightning channel?**

**Purpose:**
- Make students recognize the **on-chain anchoring** that underpins Lightning channels.

**Example of Good Expected Answer:**
> The funding transaction establishes the initial locked value that the channel will manage. It creates a 2-of-2 multisignature output requiring cooperation from both participants to spend. This output secures the funds in a way that both parties can verify and builds the trust foundation necessary for off-chain updates. Without the funding transaction anchoring the channel to the Bitcoin blockchain, there would be no enforceable starting point.

### Question 3
> **Why do we need commitment transactions if we already have a funding transaction?**

**Purpose:**
- Help students differentiate between **locking funds (funding tx)** and **managing balances (commitment tx)**.

**Example of Good Expected Answer:**
> The funding transaction only locks the funds jointly, but it doesn't say how those funds are supposed to be divided at any given moment. Commitment transactions express the current agreement about who owns what portion of the funds. Each time the channel balance changes, new commitment transactions are created, signed, and stored by both parties to reflect the updated state, while the funding transaction remains unchanged on-chain.

### Question 4
> **If both participants create commitment transactions, but don't immediately publish them, what kinds of risks might arise if someone disappears before the process is finished?**

**Purpose:**
- Highlight **operational risks** during the channel opening.
- Stress the importance of **safe sequencing**.

**Example of Good Expected Answer:**
> If one participant disappears before both sides have safely exchanged valid commitment transactions, the other participant could be left with no way to recover their funds. They might have already locked money into the funding transaction, but without a commitment transaction, they have no unilateral way to claim it. This shows why Lightning protocols require careful sequencing: exchanging valid commitments must happen before publishing the funding transaction.

### Question 5
> **What could happen if the commitment transaction is not fully agreed upon and signed *before* the funding transaction is broadcast?**

**Purpose:**
- Emphasize **why the protocol must enforce safe operations** to prevent loss of funds.

**Example of Good Expected Answer:**
> If the funding transaction is broadcast without valid, signed commitment transactions in place, one party could lose control over their funds. They would have locked bitcoin into a multisig output without holding any way to claim their share unilaterally. If the other party becomes uncooperative or disappears, the honest participant could face a total loss. This highlights why the Lightning protocol demands that the necessary safety structures (commitments) must be prepared before funds are committed on-chain.
