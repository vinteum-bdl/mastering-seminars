# 📚 Week 2 – Lightning Channels as Systems of Bitcoin Transactions

This week we are focusing on opening and closing payment channels.
In asnwering the following questions, focus on the Bitcoin transactions Alice and 
Bob would have to build and what should they do to them (propagate to the network or keep off-chain on their private records).
Try to build the simplest solution to solve the most immediate problem posed.
There is no need for revocation keys or HTLCs for now, these are important security mechanisms we will introduce once we analyze the problems that arise from using the primitives we will build here.
This solution will not work on the real-world, but let complexity increase when complexity is needed.

### Question 1

> **Alice and Bob make frequent payments among each other, so they decide to open a payment channel.
> Alice contributes 1000 sats and Bob 2000 sats.
> To simplify, suppose Alice has a 1000 sats UTXO and Bob has a 2000 sats UTXO available.
> What kind of Bitcoin transaction do they need to build and broadcast to set up the channel?**

Purpose:
- Introduce the funding transaction as a multisig deposit.
- Ground the discussion in a concrete example with clear inputs.

Example of Good Expected Answer:

> They need to create a funding transaction that locks the combined 3000 sats into a 2-of-2 multisig output — a contract that requires both Alice and Bob’s signatures to spend.
> This transaction will have two inputs: one spending Alice's 1000 sats UTXO and another spending Bob's 2000 sats UTXO.
> Each party has to sign their respective input.
> The transaction must have a single output locked to a 2-of-2 multisig contract requiring that Alice and Bob coordinate to spend the combined funds.
> This transaction will be propagated to the Bitcoin network and must be confirmed before the channel is usable.

### Question 2

> **Suppose Alice and Bob sign the funding transaction and propagate it to the Bitcoin Network.
> Now, Alice becomes unresponsive.
> Can Bob recover his funds from the payment channel?**

**Purpose:**
- Lead students to realize the need for safe exists.
- Make students think about what can go wrong at all times an action is performed.

**Example of Good Expected Answer:**

> From the perspective of the Bitcoin network, there are no Bob's funds anymore since his UTXO was spent by the funding transaction he built with Alice.
> Now, there is only the combined 3000 sats of both Alice and Bob locked to a 2-of-2 multisig contract.
> Since Alice is unresponsive, Bob cant'recover his initial 2000 sats balance.

### Question 3

> Let's solve that by creating another transaction to allow for Alice and Bob to recover their funds in the case the other party becomes unresponsive.
> What kind of Bitcoin transaction do they need to build?

**Purpose:**
- Motivate the commitment transaction as a safety mechanism to allow for unilateral exit.

**Example of Good Expected Answer:**

> They need to create a second transaction that spend the multisig contract.
> It will have a single input, the 3000 sats UTXO from the funding transaction.
> Since it's a 2-of-2 multisig, both Alice and Bob will sign this input.
> The transaction must have two outputs.
> The first pays 1000 sats to Alice, and the second pays 2000 sats to Bob.
> In this way, each party will be able to recover their funds in case the other becomes unresponsive.

### Question 4

> We established that Alice and Bob must create two transactions to open a payment channel: a funding transaction and a commitment transaction.
> The former is used to commit funds to the channel, the later is there to guarantee both parties will have a escape route in case things go sour.
> In what order should Alice and Bob build and broadcast these transactions? Why does the order matter?

**Purpose:**
- Motivate students to think about what can go wrong and how one party could attack the other.

**Example of Good Expected Answer:**

> They should first create the commitment transaction, but not sign it, so that they can compute its txid.
> Next, they should create and sign the commitment transaction.
> In this way, they both guarantee they'll have an exit door before they commit to the funding transaction.
> Otherwise, one party might be unresponsive after the propagation of the funding transaction and the other would not be able to build the commitment transaction.

### Question 5

> In a traditional Bitcoin payment, you don't need to coordinate with anyone to spend your UTXO.
> Why do Lightning channels require so much coordination to be safe?
> What are we gaining, and what are we risking?

**Purpose:**

- Encourage reflection on the trust-cooperation tradeoff.
- Make students articulate why the added complexity exists and what it enables.
- Reinforce the importance of exit strategies in protocol design.

Example of Good Expected Answer:

> In a regular Bitcoin payment, each user independently constructs, signs, and broadcasts their transaction.
> There’s no need for coordination beyond the receiver sharing an address.
> In Lightning, we are locking funds into a shared multisig output and choosing to not spend it immediately, so we can reuse it for many off-chain balance updates.
> This demands tight coordination:
> both parties must agree on how to allocate funds, prepare transactions in advance, and commit to safety mechanisms like the commitment transaction.
> We gain lower fees and instant payments, but we risk losing funds if the protocol steps aren’t followed precisely.
> That’s why Lightning channels frontload the complexity:
> to enable efficient, private, and low-cost payments under the right trust assumptions.
