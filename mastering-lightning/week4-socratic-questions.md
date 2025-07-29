# 📚 Week 4 - Cheating with Valid Transactions and the Need for Revocation Keys

Let’s what we are doing:
Alice and Bob opened a payment channel.
Alice contributed to the channel with a 1000 sats UTXO and Bob with a 2000 sats UTXO.
They built a funding transaction that spends each party's UTXO and locks the 3000 sats into a single output with a 2-of-2 multisig contract.
Alice makes a 100 sats payments to Bob.

Last week we saw that the commitment transactions must be asymmetric, i.e., Alice and Bob will hold different versions to implement a punishment mechanism in case the other party tries to cheat by propagating an outdated commitment transaction.
Let's focus on Alice's version of the commitment transaction; it has two outputs:
1. pays 2100 sats to Bob immediately (we call this `to_remote` output),
2. pays 900 sats to Bob immediately or to Alice in two days (we call this `to_local` output).

Bob's commitment transaction is symmetric, but timelocked against him (try to describe Bob's version of the transaction).

But this protocol has a serious flaw: Alice can still cheat and steal Bob's funds.
She does so not by using an outdated commitment transaction, that would be too risky because of the penalty mechanism we have put in place; but by making Bob propagate the latest commitment transaction to close the channel.

Let's explore this vulnerability and how it's solved using revocation keys.
Forget about HTLCs, though, they are not needed now.

### Question 1
> **Last week, we designed asymmetric commitment transactions:
> the broadcaster’s output is timelocked, and the counterparty’s output is spendable immediately.
> Suppose Alice and Bob have a channel with a current state where Alice has 900 sats and Bob has 2100 sats.
> Now, Alice stops responding. Bob broadcasts his commitment transaction to unilaterally close the channel.
> Can Alice steal any of Bob’s funds? How?**

**Purpose:**
- Reveal the vulnerability of the broadcaster’s commitment transaction.
- Help students identify that the counterparty controls the key for one of the outputs.

**Example of Good Expected Answer:**
> Yes, Alice can steal Bob’s funds. In Bob’s commitment transaction, the output that pays him is timelocked, but the output that pays Alice is immediately spendable by Alice.
> This means Alice can take the 900 sats as soon as the transaction confirms.
> But that’s not the problem — the issue is that Bob’s output also allows Alice to spend the 2100 sats immediately, because the output script has a branch that pays to Alice without delay, using her public key.
> Since she knows the corresponding private key, she can sign a transaction spending that output right away, and Bob can’t stop her.

### Question 2
> **One way to fix this is to stop using Alice’s real public key in the output script.
> Suppose Bob’s output is timelocked and can be spent either by Bob after 2 days, or by someone with a special public key — one that Alice doesn’t know the private key for.
> What problem does this fix? What does it break?**

**Purpose:**
- Lead students to recognize that you can make the output unspendable by Alice — but at a cost.
- Introduce the tension between cheat prevention and penalty enforcement.

**Example of Good Expected Answer:**
> If we make the output spendable only by a key that Alice doesn’t control, she can no longer steal funds by broadcasting Bob’s commitment transaction.
> But this breaks the punishment mechanism:
> In the case where Bob tries to cheat by broadcasting an old state, Alice can’t reclaim his output either, because she also doesn’t know the key needed to claim it.
> So we stop Alice from cheating — but we also stop her from punishing Bob if he cheats.

### Question 3
> **So we want the output to be unspendable by Alice right now — but spendable by her in the future if Bob misbehaves.
> Can we design the output so that it’s locked to a key Alice can only reconstruct after Bob gives her some secret?
> What would the update process look like in this design?**

**Purpose:**
- Introduce the idea of conditional control — that the script should reference a key whose private part is revealed only after a new state is agreed upon.
- Transition to the concept of revocation keys.

**Example of Good Expected Answer:**
> Yes. We can construct an output that uses a key whose private part is only computable if Bob gives Alice some secret.
> When Bob and Alice agree on a new state, Bob gives Alice that secret for the previous state, enabling her to claim the output in case Bob tries to broadcast it.
> But Bob keeps the secret for the current state private — so Alice can’t use it right now to cheat.
> Only once the next state is locked in, the previous state becomes unsafe for Bob to use.

### Question 4
> **Let’s zoom in. The commitment transaction has an output script that says:
> "If revocation key: spend immediately; else: wait 2 days and use the to_local key."
> What exactly is this 'revocation key'? How is it created, and what makes it secure to use in this context?**

**Purpose:**
- Examine the cryptographic construction of the revocation key.
- Transition from conceptual understanding to actual mechanism.

**Example of Good Expected Answer:**
> **The revocation key is a public key that’s derived from secrets known only by the counterparty after a state is revoked.
> It’s constructed using two keys:
> A per-commitment point (unique to that channel state), and
> A base revocation base key (constant across the channel).
> The actual revocation public key is derived from a formula using both.
> Only when the per-commitment secret is revealed (during a state update), the counterparty can compute the private key corresponding to the revocation pubkey.
> Until then, it’s just an unusable public key — the broadcaster cannot spend it.**

## Question 5
> **Let’s put it all together.
> Suppose Alice wants to pay Bob 100 sats using their channel.
> Walk through the full protocol step-by-step:
> How is the channel state updated? What transactions are created, what information is exchanged, and how is the previous state made unsafe to use?
> Why is the term “revocation” a bit misleading in this context?**

**Purpose:**
- Ensure students internalize the entire channel update process.
- Reinforce that Bitcoin doesn’t support revoking a transaction — only changing incentives around broadcasting it.
- Emphasize the relationship between state update, signatures, and conditional secret revelation.

**Example of Good Expected Answer:**
> To make the payment, Alice and Bob construct a new pair of asymmetric commitment transactions — one for each of them — that reflect the new balances (Alice: 900 sats, Bob: 2100 sats).
> They exchange signatures and only consider the update final once both sides hold a fully signed version of their own commitment transaction.
> Once that’s done, each party sends the revocation secret corresponding to the previous state to the other.
> This secret allows the counterparty to compute the private key of the revocation output in the old commitment transaction.
> That way, if someone broadcasts the old state, the counterparty can immediately claim all the funds.
> The previous transaction is still valid — Bitcoin doesn’t support deleting or invalidating it.
> But by revealing a secret, the revoker gives the other party the ability to punish any attempt to use it.
> So “revocation” doesn’t mean erasure — it means arming the other party to make that state toxic to use.
