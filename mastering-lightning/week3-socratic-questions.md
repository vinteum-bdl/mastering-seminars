# 📚 Week 3 — Making Payments Using a Channel

Let’s recap the scenario from last week.
Alice and Bob opened a payment channel.
Alice contributed to the channel with a 1000 sats UTXO and Bob with a 2000 sats UTXO.
They built a funding transaction that spends each party's UTXO and locks the 3000 sats into a single output with a 2-of-2 multisig contract.
At the same time, they also built and signed a commitment transaction that spends the 2-of-2 multisig output.
This commitment transaction has two outputs: one paying 1000 sats to Alice and another paying 2000 sats to Bob.

Alice and Bob both hold a copy of the same commitment transaction.
We are going to change that today.
Again, we urge you to try to build the simplest solution given the problem at hand.
Today we will introduce timelocks and the punishment mechanism of Lightning.
We don't need revocation keys or HTLCs for now; they’ll appear next week.

### Question 1

> **Alice wants to pay 100 sats to Bob using the payment channel they established.
> For that to happen, they need to update their commitment transaction because its outputs are used to represent the agreed amount each party owns from the multisig UTXO they share.
> Describe this new commitment transaction.
> What transactions each of the parties have in hand after they create the payment?**

**Purpose:**
- Establish the notion that making a payment updates the channel state.
- Reinforce that a new commitment transaction must be created and signed.

**Example of Good Expected Answer:**
> To pay 100 sats to Bob, Alice and Bob must collaboratively build and sign a new commitment transaction that spends the same funding output, but with new values in the outputs: 900 sats to Alice and 2100 sats to Bob. Each party will now hold a signed transaction representing this updated state.

### Question 2
> **Note that Alice and Bob have two pre-signed commitment transactions at hand.
> Focus on Alice's perspective, now.
> She has the first commitment transaction paying her 1000 sats and a second transaction paying her 900 sats.
> How can she use that to steal 100 sats from Bob?
> In the current state of our design, can Bob do something to stop Alice from stealing him?**

**Purpose:**
- Confront students with the double-spend risk using outdated state.
- Reveal the problem of trust without punishment.

**Example of Good Expected Answer:**
> Alice now holds two valid, signed transactions: one where she has 1000 sats and one with 900.
> Nothing stops her from broadcasting the older one to reclaim a more favorable balance.
> In the current protocol, Bob has no defense against this — once the transaction is confirmed, it’s final.
> This reveals a key flaw: old states must be made unsafe to use.

### Question 3
> **Our protocol has a serious flaw: Alice can use an old, more favorable, channel state to steal funds from her channel counterparty.
> Part of the problem is that Alice can use the commitment transaction to immediately receive funds from the shared UTXO.
> How can we use timelocks in the commitment transaction to ensure she has to wait for some time (say, 2 three days) to claim her funds from the channel?
> Describe what has to change in the commitment transaction they are going to build and pre-sign.
> Is that sufficient to stop the stealing from Alice?**

**Purpose:**
- Introduce timelocks as a defensive mechanism.
- Show that delay alone isn't enough to prevent theft.

**Example of Good Expected Answer:**
> Alice’s output in her commitment transaction can be changed to a delayed output using a relative timelock (e.g., OP_CHECKSEQUENCEVERIFY).
> This means she cannot spend it until 2 days after the transaction is confirmed.
> This gives Bob time to react, but by itself, it’s not enough — if Bob has no special script to use during this delay, he still can’t recover the funds.

### Question 4
> **We introduced a delay to Alice when she wants to propagate the commitment transaction to close the channel.
> In that way, Bob has some time (2 days) to detect it, but right now he can't do anything to stop Alice.
> That delay means Alice won't be able to create a valid transaction to spend her side of the commitment transaction until some time has passed.
> What additional modification should we make to the commitment transaction so that Bob can create a valid spending transaction before Alice and reclaim her funds?
> This will efectivelly create a punishment mechanism: if Alice tries to close the channel with an out of date state, Bob will have some time to reclaim all funds in the channel, making it quite expensive to Alice to even try doing that.**

**Purpose:**
- Build a mechanism for punishable exits.

**Example of Good Expected Answer:**
> We can replace Alice’s delayed output with a special script: Bob can spend it immediately, but Alice has to wait for 2 days to spend.
> This makes broadcasting old commitments very risky because now the other party can immediately reclaim out funds.

### Question 5
> **We have created new contracts in the commitment transaction to protect Bob from Alice's attempt to use an old commitment transaction with an out of date channel state.
> Now consider that Bob can do the same to Alice.
> We will have to put the same mechanisms in place, but to the other side.
> Describe the Bob's version of the new commitment transaction.
> Alice and Bob will each hold a copy of the same pre-signed commitment transaction or they'll have to maintain different versions of it?**

**Purpose:**
- Reinforce asymmetry in the design of commitment transactions.
- Clarify that each party holds a different transaction.

**Example of Good Expected Answer:**
> Alice and Bob must each hold different versions of the commitment transaction.
> Alice’s version pays her immediately and delays Bob’s output; Bob’s version does the opposite.
> This ensures that if either party tries to cheat, the counterparty has both time and the ability to claim the funds through the punishment mechanism.
> The asymmetry is essential to prevent mutual exploitation while still allowing unilateral closure.

### Question 6
> **The commitment transaction has two outputs, the first belonging to Alice and the seconds belonging to Bob.
> In Questions 3 and 4, we were trying to prevent Alice from stealing Bob by propagating an old channel state.
> For that, we modified only Alice's output.
> Why we didn't need to change Bob's output at all, at that point?**

**Purpose:**
- Identify the exact point of failure in the protocol.
- Reinforce the design principle of least modification.

**Example of Good Expected Answer:**
> When Alice propagated her version of the commitment transaction, she is effectively making two payments.
> One of the outputs pays to her 1000 sats, of which 100 belong to Bob.
> So, we have to modify this output so that Alice can't that what's not hers.
> The second output pays 2000 sats to Bob, not to Alice.
> And since these 2000 sats indeed belong to Bob, they are being paid to their rightfull owner and nothing has to be done about it.

### Question 7
> **Our protocol still has a subtle but catastrophic vulnerability: Alice can still steal Bob's funds.
> Can you describe how?**

**Purpose:**
- Identify the new point of failure in the protocol.
- Identify the need for additional security mechanisms.

**Example of Good Expected Answer**
> We saw that if Alice tries to propagate an outdated commitment transaction, Bob can now punish her.
> Now, after the payment, Alice stops responding Bob's messages, she pretends her node is offline.
> After a while, Bob will try to close the channel with the last state, a commitment transaction that has two outputs.
> The first pays 900 sats to Alice now.
> The second pays 2100 sats to Bob in 2 days or 2100 sats to Alice now.
> Note that Bob has to wait 2 days to recover his funds because of the security mechanism we put in place to stop him from stealing from Alice by propagating an outdated channel state.
> When Alice detects this, she can immediately spend the 2100 sats outputs and Bob can do nothing to stop her, after all, it only depends on Alice's signature.
