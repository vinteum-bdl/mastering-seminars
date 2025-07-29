# 📚 Week 7 — Pathfinding, Gossip, and Liquidity

In previous sessions, we learned how to build secure payment channels, route payments using HTLCs, and protect user privacy with onion routing.

This week, we shift focus to the infrastructure of coordination:
- How nodes learn about the network,
- How they decide which route to use,
- And how liquidity (or lack of it) affects payment reliability.

We’ll reason from first principles about what routing requires in a decentralized setting — and how Lightning solves this problem without centralized coordination or global consensus on balances.

## Question 1
> **Suppose Alice wants to pay Carol. She doesn't have a direct channel, but she knows Bob does.
> She also suspects Carol is connected to Dave.
> How does Alice learn which nodes are connected to whom?
> Who tells her that these channels exist?**

**Purpose:**
- Reveal the need for a decentralized topology discovery mechanism.
- Motivate the gossip protocol.

**Example of Good Expected Answer:**
> Alice learns about public channels through the gossip protocol.
> Nodes in the Lightning Network propagate information about which channels exist, who’s involved, what fees are charged, and what timelocks are required.
> This allows each node to build a local view of the network graph and use it to compute routes.
> No central directory exists — each node relies on what others choose to announce.

## Question 2
> **Let’s say Alice learns that Bob has a channel with Carol.
> She doesn’t know the current balance in that channel.
> Why not? And why is this both a design feature and a limitation?**

**Purpose:**
- Make students confront the tradeoff between privacy and liquidity transparency.
- Expose the unpredictability of available paths.

**Example of Good Expected Answer:**
> Lightning channels are private contracts — their current balances are not publicly known.
> This protects users’ privacy, but it also means Alice doesn’t know if Bob has enough liquidity to forward the payment.
> Every node must guess which channels are viable, often based on past experience or probing.
> This makes routing uncertain — a path might exist but still fail due to insufficient funds.

## Question 3
> **Imagine routing worked like on the internet: each hop decides where to send the packet next.
> Why doesn’t Lightning use this approach? Why is the sender responsible for building the entire route ahead of time?**

**Purpose:**
- Highlight the contrast between best-effort IP routing and Lightning's need for strict, atomic coordination.
- Reinforce the design constraints of privacy and security.

**Example of Good Expected Answer:**
> In Lightning, each payment must either succeed end-to-end or fail completely — partial forwarding makes no sense.
> This requires atomic coordination across all hops.
> Only the sender knows the final destination and payment details.
> If hops could choose the next forwarder, they could leak or manipulate the payment path, violating privacy or correctness.
> So the sender constructs the entire route and encrypts instructions for each hop using onion routing.

## Question 4
> **Suppose Alice chooses a route but the payment fails mid-way — for example, because Bob doesn't have enough liquidity.
> What can she do to recover? Can she try again? How would she choose a better route?**

**Purpose:**
- Explore the concept of retries and adaptive routing.
- Introduce liquidity estimation heuristics.

**Example of Good Expected Answer:**
> Alice can retry the payment with a different route.
> Over time, her node might learn that some channels are unreliable or too small.
> Implementations use heuristics — like penalizing failed channels — or probing techniques to estimate available liquidity.
> But there's no perfect information.
> Retrying introduces delay and can reduce privacy if too many attempts are made.

## Question 5
> **To improve reliability, Lightning supports multi-path payments (MPP): splitting the payment into parts sent over different routes.
> What are the advantages and risks of this strategy? Why might a node choose to use it — or avoid it?**

**Purpose:**
- Encourage reasoning about real-world tradeoffs in protocol extensions.
- Highlight ongoing design work in the ecosystem.

**Example of Good Expected Answer:**
> MPP lets a sender combine liquidity from multiple smaller channels, increasing the chance of success.
> It also makes large payments more feasible.
> But it adds complexity — all parts must arrive in time and be locked atomically.
> Partial failure increases coordination risk.
> Some nodes might avoid MPP to keep things simpler or avoid privacy leaks from splitting paths.

## Question 6
> **Let’s say you want to design a better routing algorithm for your Lightning node.
> What kinds of data would you wish you had access to?
> Why can’t you access all of it? What would you prioritize in your design?**

**Purpose:**
- Invite students to synthesize what they’ve learned and imagine real improvements.
- Close the seminar with forward-looking thinking.

**Example of Good Expected Answer:**
> Ideally, I’d want to know each channel’s current balance, uptime, and past performance.
> But this data is either private or unavailable due to the decentralized design.
> I’d have to work with gossip data, failed payment history, and optional probing results.
> My priorities might depend on the context: minimize fees, maximize privacy, or prioritize reliability.
> Any routing algorithm must balance incomplete information, strategic behavior by peers, and user goals.
