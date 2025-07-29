# 📚 Week 6 — Privacy in the Lightning Network and the Role of Onion Routing

So far, we've been thinking about correctness, safety, and liveness.
But what about privacy?

This week we’ll reason through what information is leaked when a payment is routed, who learns what, and what tools the Lightning Network provides to mitigate these leaks.

We'll begin with a simple multi-hop scenario and work our way toward understanding the structure of Sphinx packets, the rationale for source routing, and the tradeoffs behind Lightning’s current privacy model.

## Question 1
> **Alice wants to send 100 sats to Carol. She has a channel with Bob, who in turn has a channel with Carol.
> So the route is: Alice → Bob → Carol.
> What does Bob learn when he helps forward this payment? Can he tell that Carol is the final recipient? Can he tell the original sender?**

**Purpose:**
- Reveal what information is visible to intermediaries.
- Set up the motivation for onion routing.

**Example of Good Expected Answer:**
> In a naïve implementation, Bob sees both Alice (the previous hop) and Carol (the next hop), as well as the payment amount and the hash preimage condition.
> He can infer that Carol is likely the final recipient — especially if he doesn't know of further connections.
> Alice’s identity is also visible to him.
> This creates a privacy risk for both sender and recipient.

## Question 2
> **Imagine the payment were split over two paths: one through Dave and one through Eve, both leading to Carol.
> Could Carol learn who the original sender was, or how many hops were involved?
> What about Bob, Dave, or Eve — could any of them reconstruct the full route?**

**Purpose:**
- Emphasize that Lightning lacks built-in anonymity.
- Explore the visibility of partial vs full routes.

**Example of Good Expected Answer:**
> Carol only sees the final HTLC she receives.
> If no additional metadata is revealed, she might not know who the original sender was.
> But if the route is short or the payment pattern is unique, she could guess.
> Intermediaries (like Bob, Dave, or Eve) only see their direct neighbors in the route.
> Without onion routing, however, they could potentially correlate information across payments or collaborate to deanonymize users.

## Question 3
> **To fix this, the Lightning Network uses onion routing.
> What is the basic idea behind onion routing?
> What information does each hop see, and what remains hidden?**

**Purpose:**
- Introduce onion routing as a privacy-preserving strategy.
- Shift student thinking from explicit path declarations to layered encryption.

**Example of Good Expected Answer:**
> In onion routing, the sender encrypts routing instructions in layers — like an onion.
> Each hop peels one layer to learn:
> the amount to forward,
> the next hop’s identity,
> and how long to hold the HTLC (timelock).
> But it cannot see the full route, the original sender, or the final destination (beyond its neighbor).
> This minimizes what any single node can learn.

## Question 4
> **Let’s zoom in on the data that travels with the payment.
> What is a Sphinx packet, and why is it used in the Lightning Network instead of just simple encryption?
> How does it enhance privacy?**

**Purpose:**
- Examine the structure of routing data.
- Bridge theory and implementation.

**Example of Good Expected Answer:**
> A Sphinx packet is a structure that carries encrypted routing instructions through the network.
> It ensures that each hop:
> Can only decrypt its own instructions;
> Cannot distinguish the packet's size or infer how many hops remain;
> Cannot link a packet across the network even if multiple nodes collude.
> This makes correlation attacks much harder and protects both sender and recipient privacy.

## Question 5
> **Lightning uses source routing: the sender picks the entire path ahead of time and includes encrypted instructions for each hop.
> Why is this design good for privacy — and what tradeoffs does it introduce for scalability or route discovery?**

**Purpose:**
- Encourage critical reflection on protocol design tradeoffs.
- Prepare students for Week 7's topic: pathfinding and network discovery.

**Example of Good Expected Answer:**
> Source routing gives the sender full control over the route, which means no node in the middle decides how to forward the payment.
> This helps preserve privacy — no intermediary knows the full path or destination.
> However, it requires the sender to know the entire network topology and available liquidity, which can be difficult.
> It shifts complexity to the sender and makes routing harder at scale.

## Question 6
> **Even with onion routing and encrypted HTLCs, certain attacks are still possible.
> For example, an attacker might send test payments or observe timing patterns to infer information.
> What kinds of privacy attacks still threaten Lightning payments? What would you want to investigate further?**

**Purpose:**
- Encourage students to think critically about remaining vulnerabilities.
- Prompt self-directed exploration of current research.

**Example of Good Expected Answer:**
> Some known attacks include:
> Timing analysis: If a node sees the exact moment a payment is forwarded and then later received, it might infer its position in the route.
> Probing attacks: A node can send fake payments through the network to learn about channel balances or paths.
> Correlation: If the same node appears in multiple hops, it can compare what it sees at different points in the route.
> These attacks show that even with encrypted routing data, metadata and traffic patterns can still leak information.
> It would be worth investigating proposals like blinded paths, trampoline routing, or PTLCs to improve privacy further.
