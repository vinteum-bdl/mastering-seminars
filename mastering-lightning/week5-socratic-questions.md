# 📚 Week 5 — Routing Payments Across Independent Channels

Until now, we studied how two parties can open a channel, update its state, and enforce fairness using revocation keys.
But the real power of the Lightning Network lies in allowing people to pay others they aren’t directly connected to.

This week, we explore multi-hop payments by looking at a concrete scenario involving Alice, Bob, and Carol.
We’ll identify the challenges of coordinating across independent channels and use that to motivate the need for a new kind of contract:
the Hashed Time-Locked Contract (HTLC).

Let’s begin.

## Question 1
> **Alice has a channel with Bob, where she owns 1000 sats and Bob owns 2000 sats.
> Bob has another channel with Carol, where he owns 3000 sats and Carol owns 4000 sats.
> Alice wants to pay 100 sats to Carol.
> She considers sending 100 sats to Bob in their channel, asking him to forward 100 sats to Carol.
> What could go wrong? What can Bob do in this scenario?**

**Purpose:**
- Introduce the incentive problem in naive multi-hop payments.
- Emphasize that trusting intermediaries undermines the protocol's goals.

**Example of Good Expected Answer:**
> Bob might simply keep the 100 sats.
> Once Alice pays Bob in their channel, there’s nothing forcing him to forward those funds to Carol.
> Alice has no visibility into the Bob–Carol channel, and no way to reverse the transfer.
> This breaks the trustless nature of Lightning — we’re depending on Bob’s goodwill.

## Question 2
> **To avoid paying Bob first, Alice proposes the opposite:
> “Bob, if you forward 100 sats to Carol, I promise I’ll pay you 100 sats in our channel.”
> Suppose Bob agrees and sends the payment to Carol.
> Can Alice cheat now? How?**

**Purpose:**
- Highlight the same incentive problem in reverse.
- Show that “first move” disadvantage exists on both sides.

**Example of Good Expected Answer:**
> Yes, now Alice can cheat.
> After Bob forwards 100 sats to Carol, he expects Alice to pay him back in their channel.
> But Alice can simply disappear or refuse to cooperate.
> Bob has no way to enforce the deal — he already lost funds in the Carol channel and has no signed transaction from Alice reflecting the update.
> The core issue is again: there’s no contract, only a promise.

## Question 3
> **The problem in both cases is that we're relying on promises, not enforceable contracts.
> But Bitcoin transactions are a language for expressing contracts, and payment channels are built on Bitcoin transactions.
> Can we design a contract in the Alice–Bob channel that pays 100 sats to Bob only if Bob provides cryptographic proof that he made a payment to Carol?
> What kind of contract would that be? Describe how the commitment transaction would be modified to account for this contract.**

**Purpose:**
- Introduce HTLCs as contract-based promises.
- Emphasize conditionality and enforcement.

**Example of Good Expected Answer:**
> Yes, we can design a contract that says:
> “Bob can claim 100 sats from Alice only if he reveals a specific secret value.”
> This value must also be part of the payment to Carol — for example, Carol can claim 100 sats from Bob only if she reveals a secret R such that H = SHA256(R).
> Once Carol claims the payment, she reveals R, and Bob uses it to claim 100 sats from Alice.
> This kind of contract is called a Hashed Time-Locked Contract (HTLC).
> It enforces the forwarding relationship cryptographically — not with trust.

## Question 4
> **Let’s now describe how this HTLC-based payment from Alice to Carol actually works.
> Walk through all the state transitions in both channels:
> What changes in Alice–Bob and Bob–Carol commitment transactions?
> When and how do the HTLC outputs appear and disappear?
> What happens if something fails midway?**

**Purpose:**
- Solidify understanding of HTLCs as contract extensions of commitment transactions.
- Highlight atomicity and time-sensitive conditions.

**Example of Good Expected Answer:**
> Carol first generates a secret R and shares the hash H = SHA256(R) with Alice.
> Alice updates her commitment transaction with Bob to include an additional output with the HTLC:
> - “Bob can claim 100 sats if he reveals R within 30 blocks.”
> Bob updates his commitment with Carol to include another HTLC:
> - “Carol can claim 100 sats if she reveals R within 15 blocks.”
> Carol claims the payment by revealing R to Bob.
> Bob sees R and uses it to claim 100 sats from Alice.
> Once R is revealed and both payments succeed, the HTLCs are removed from both commitment transactions.
> If Carol doesn’t reveal R before her deadline, the HTLC expires, and Bob can reclaim his funds. The same applies in the Alice–Bob channel if Bob fails to claim in time.

## Question 5
> **Now let’s reverse the flow.
> Carol wants to pay 3000 sats to Alice through Bob.
> Carol has a channel with Bob, where she owns 4000 sats and Bob owns 3000 sats.
> Bob also has a channel with Alice, where Alice owns 1000 sats and Bob owns 2000 sats.
> Can the payment go through? What prevents it, even though Carol has enough funds?**

**Purpose:**
- Introduce the concept of liquidity constraints and balance direction.
- Emphasize that it's not just about whether Carol has the money — but whether the network has a path with the right liquidity flow.

**Example of Good Expected Answer:**
> The payment would fail.
> Even though Carol has enough funds and wants to send 3000 sats, the problem lies in the Bob–Alice channel.
> Bob only has 2000 sats there — that’s his sendable balance in that direction.
> He needs to forward 3000 sats to Alice, but he doesn’t have that much liquidity available.
> This shows that Lightning routing depends not only on the existence of a path, but also on the directional liquidity along that path.
> Payment routing is constrained by how funds are currently distributed across channels.
