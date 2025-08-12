# 📚 Week 5 — Routing Payments Across Independent Channels

In the previous weeks, we explored how two parties can establish a payment channel and update its state securely and privately.
We now understand:
- How a channel is opened using Bitcoin transactions;
- How the balance is updated through new commitment transactions;
- How the punishment mechanism discourages cheating through revocation keys.

But Lightning isn’t just about bilateral payment channels.
The real magic is that you can pay someone you're not directly connected to.

This week, we study how Lightning enables multi-hop payments — a mechanism to route a payment across a path of independent channels, such as:
Alice → Bob → Carol.

The key challenge here is coordination.

Each channel is governed by its own logic and its own protocol history.
Alice and Bob may have a channel.
Bob and Carol may have another.
But these channels don’t know about each other — they’re entirely independent systems.

So how can we make sure that if Alice pays Bob, and Bob pays Carol, then Bob doesn’t cheat by keeping the money?
And more generally: how do we make sure that either all hops in the route succeed, or none of them do?

That’s the problem of atomicity across independent systems.

This week, we’ll introduce Hashed Time-Locked Contracts (HTLCs) as a solution to that problem.
HTLCs use a clever combination of hashes and time locks to create a chain of conditional payments, where each hop is secured by a contract that:
- Can only be fulfilled by revealing a secret,
- And expires if the payment can’t be completed in time.

This gives Lightning its routing capability:
We don’t need to trust intermediaries, because intermediaries are held cryptographically accountable for forwarding the payment — or losing their chance to claim funds.

---

## 📙 Core Reading Assignment
1. Antonopoulos et al, Mastering the Lightning Network — Chapter 4: Routing Payments
2. Antonopoulos et al, Mastering the Lightning Network — Chapter 7: Read again with focus on Hashed Time-Locked Contracts (HTLCs)
3. Elle Mouton, [LN Things Part 4: HTLCs](https://ellemouton.com/posts/htlc/)
4. Lightning Labs, [A Technical Walkthrough of Hash Time Locked Contracts and Lightning Channel Operations](https://lightning.engineering/posts/2023-06-28-channel-normal-op/) 

---

## 📈 Optional Reading Assignment
- Lightning Labs, [The Builder's Guide to the LND Galaxy!](https://docs.lightning.engineering)
- Christian Decker, [Lightning ≈ Bitcoin](https://youtu.be/8lMLo-7yF5k?si=rTGo0vMUeBVTHexM)
- [BOLT 2](https://github.com/lightning/bolts/blob/master/02-peer-protocol.md) and [BOLT 4](https://github.com/lightning/bolts/blob/master/04-onion-routing.md) (skim for real-world implementation detail)

---

## 🔍 Self-Study Questions
1. What is the main challenge in routing a payment through multiple independent channels?
2. Why is it not enough to have each pair of peers coordinate off-chain as we do in a single payment channel?
3. Describe what can go wrong if Bob receives a payment from Alice and then refuses to forward the payment to Carol.
4. Why is atomicity important when routing payments across multiple channels?
5. What is an HTLC? What role does the hash preimage play in ensuring atomicity?
6. How do time locks interact with hashes in HTLCs to create a secure conditional payment?
7. Suppose Carol knows the preimage R for a hash H. How does that allow Alice to safely initiate a payment to Carol through Bob?
8. In the payment flow Alice → Bob → Carol, which participant generates the preimage? Who knows it at the beginning, and who learns it by the end?
9. How is trustlessness preserved even when routing through intermediaries? Why can’t Bob steal the payment?
10. What happens if one hop in the route fails (e.g., Carol goes offline)? How do HTLCs allow the payment to be reversed cleanly?
11. Describe how time locks are structured to cascade from the final recipient (e.g., Carol) back to the sender (e.g., Alice).
12. What is the relationship between HTLCs and the commitment transactions we've been building so far? Are HTLCs separate transactions or extensions of the same protocol?
13. What are the tradeoffs of using HTLCs? Do they affect privacy, scalability, or complexity?
14. If Lightning nodes are constantly adding and removing HTLCs from their commitment transactions, what kind of new failure modes or risks might arise?
15. Why is routing considered one of the hardest unsolved challenges in Lightning protocol design, even today?
