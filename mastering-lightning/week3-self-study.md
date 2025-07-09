# 📚 Week 3 — Making Payments Using a Channel

Last week we discussed what it means to open a payment channel with a funding transaction and the basic security mechanism that allows for unilateral exit, the commitment transaction.
We established the basic language to talk about payment channels: a pair of valid Bitcoin transactions; one that is propagated to the network and lock funds on the channel, another that is kept off-chain by both parties as a security machanism.
The commitment transaction deserves further inquiry and design, as we will discuss this week.

Let's recap the scenario from last week.
Alice and Bob opened a payment channel.
Alice contributed to the channel with a 1000 sats UTXO and Bob with a 2000 sats UTXO.
They built a funding transaction that spend each other UTXOs and lock the 3000 sats to a single output with a 2-of-2 multisig contract.
At the same time, they also built and signed a commitment transaction that spends the 2-of-2 multisig.

This commitment transaction has two outputs, the first paying 1000 sats to Alice and the second paying 2000 sats to Bob.
Here comes an important observation: **these outputs reflect the balance each party owns from the channel funds**.
We call these balances the **state of the payment channel**.
Moreover, since this commitment transaction is pre-signed by both parties, it reflects an agreement between the channel participants about how much each one owns from the shared UTXO they created in the funding transaction.

Thus, to make a payment on the channel means to update the state of the channel by creating a new commitment transaction.
That is, supposed Alice wants to pay 100 sats to Bob.
They need to coordinate to create a new commitment transaction that will reflect the new state of ownership of the shared UTXO (the 2-of-2 multisig): Alice will own 900 sats and Bob will own 2100 sats.
This is more involved than what it looks at first.
Let's dive in.

---

### 📙 Core Reading Assignment

1. Antonopoulos et al, [Mastering the Lightning Network](https://github.com/lnbook/lnbook) -  **Chapter 7**: Payment Channels.

Pay special attention to the sections "Sending Payments Across the Channel" and "Advancing the Channel State".

2. Elle Mouton, [LN Things Part 2: Updating State](https://ellemouton.com/posts/updating-state/)

3. Elle Mouton, [LN Things Part 3: Revocation in more detail](https://ellemouton.com/posts/revocation/)

---

### 📈 Optional Reading Assignment

- James Prestwich, [Bitcoin’s Time Locks](https://medium.com/summa-technology/bitcoins-time-locks-27e0c362d7a1).

- Brian Mancini, [Revocable transactions with LN-Penalty](https://www.derpturkey.com/revocable-transactions-with-ln-penalty/)

- fiatjaf, [A Lightning penalty transaction](https://fiatjaf.com/73095980.html)

---

### 🔍 Self-Study Questions

1. How is a payment channel's "state" defined in the context of Bitcoin transactions? What does it mean for a channel to have a certain "balance" between two partners?
2. What is a "commitment transaction," and what is its primary role in managing the channel balance off-chain? How does it differ from a "refund transaction"?
3. Explain how sending a payment from Alice to Bob essentially involves "redistributing the balance" of the channel.
4. What are the limitations that restrict a channel, as mentioned in Chapter 3? How does the updating process relate to these limitations?
5. If Alice sends 300 sats to Bob within a 3000 sats channel, how many valid commitment transactions might Alice hold, and what balances would they represent?
6. Why does the existence of multiple valid commitment transactions present a "cheating" problem? Since Bitcoin transactions are generally irreversible, why can't a malicious party simply broadcast an older, more favorable commitment transaction?
7. How does the Lightning Network address the "cheating with prior state" problem, given that Bitcoin transactions are censorship-resistant? What is the fundamental principle behind the "fairness protocol" in this context?
8. What is the "aggressive approach" of LN-Penalty in case of a protocol breach? What happens to a cheater's funds? Why is this "all or nothing" principle crucial for security?
9. What is the specific goal of the "revocation" process, even though Bitcoin transactions cannot truly be revoked?
10. Explain the concept of "asymmetric commitment transactions". How do the commitment transactions held by Alice and Bob differ?
11. Define `to_local` and `to_remote` outputs in a commitment transaction. Which party's funds are paid to which output?
12. What is the `to_self_delay` parameter, and how is it negotiated between channel partners?
13. Why is the `to_local` output always "timelocked" by `to_self_delay`, while the `to_remote` output is immediately spendable? What specific risk does this delay mitigate?
14. According to "Bitcoin's Time Locks," what are the differences between transaction-level and script-level timelocks, and how do absolute (`OP_CLTV`) and relative (`OP_CSV`) timelocks function? How does `OP_CLTV` specifically relate to the first version of Lightning channels?
15. What is a "revocation key"? How does it allow the cheated party to claim the cheater's entire balance?
16. How are `revocationpubkey` and `per_commitment_point` derived and used to create the revocationpubkey for each channel state?
17. Explain how the old state is "revoked" by the exchange of a private key (e.g., dA1 from Alice to Bob) during a state update. Why is it safe for a party to reveal this "secret" for the previous commitment?
18. "Revocable transactions with LN-Penalty" states that the `to_local` output is a "revocable sequence maturing contract (RSMC)" with two branches of execution. Describe these two branches.
19. How does an "honest" node detect a protocol breach (i.e., an old commitment transaction being broadcast)? What software/tools are necessary for this monitoring?
20. What is the "channel reserve," and why is it required for each channel partner to maintain a minimum balance? How does it relate to the game theory incentives of the penalty mechanism?
21. What are the disadvantages and costs associated with a "force close" compared to a "mutual close"?
22. Why is continuous uptime important for a Lightning node operator? How do watchtowers help mitigate the risk of a node being offline during a protocol violation?
23. What is the "hot wallet risk" associated with Lightning Network funds? How can funds be "swept" to reduce this risk?
24. Despite the security mechanisms, what are some lingering risks or vulnerabilities mentioned in the sources regarding Lightning node operation (e.g., bugs, backups, data loss)? How does the static channel backup (SCB) attempt to address some of these, and what are its limitations?
