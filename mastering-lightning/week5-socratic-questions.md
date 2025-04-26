# 📚 Week 5 – Socratic Questions
**Theme:** Pathfinding and Gossip — Finding Payment Routes

### Question 1
> **In Lightning, who is responsible for figuring out the path a payment should take: the sender, the receiver, or the network?**

**Purpose:**
- Make students realize **pathfinding is the sender’s responsibility**.
- Break assumptions that "the network" or "the recipient" somehow handles routing.

**Example of Good Expected Answer:**
> In Lightning, the sender is responsible for finding the full route that the payment will take through the network. The network does not route payments like the internet does; instead, the sender must gather enough information about the available channels and their properties to construct a viable path to the receiver. This design preserves decentralization and privacy but makes sending more complex.

### Question 2
> **Why do Lightning nodes need to maintain a graph of channels and nodes?**

**Purpose:**
- Introduce the idea of **local knowledge construction** through the **gossip protocol**.

**Example of Good Expected Answer:**
> Each Lightning node needs to build and maintain a local view of the network — a channel graph — to make informed decisions about payment routing. The graph shows which nodes are connected to which others, along with information like channel capacity (when advertised). Without this information, nodes would have no way to find payment paths to distant peers. The gossip protocol distributes updates about the network to allow nodes to keep their graphs reasonably accurate.

### Question 3
> **What crucial information about channels is *not* publicly available through the gossip network?**

**Purpose:**
- Push students to think critically about **hidden liquidity** as a routing challenge.

**Example of Good Expected Answer:**
> The most crucial missing information is the **current liquidity balance** inside each channel — that is, how much money is available in each direction. While nodes gossip about the existence and capacity of channels, they do not reveal real-time balances. This means that even if a path looks good on the graph, it might fail in practice if the intermediary nodes do not have enough liquidity to forward the payment.

### Question 4
> **What are some risks if a Lightning node relies too much on third-party services to find routes?**

**Purpose:**
- Introduce **privacy and security concerns** with outsourcing pathfinding.

**Example of Good Expected Answer:**
> If a Lightning node outsources pathfinding to a third party, it must share information about intended payments, such as the destination and possibly even the amount. This weakens privacy and introduces trust assumptions that Lightning was designed to avoid. Additionally, malicious or compromised routing services could manipulate path suggestions or censor certain destinations. Keeping pathfinding local preserves both privacy and autonomy.

### Question 5
> **Given that liquidity is hidden and pathfinding is hard, why doesn't Lightning just reveal all balances to make routing easier?**

**Purpose:**
- Force students to understand the **privacy vs. efficiency tradeoff** in Lightning’s design.

**Example of Good Expected Answer:**
> Revealing all channel balances would make routing much easier and more reliable, but it would seriously harm user privacy. Observers could track how much money each node holds and infer relationships between users. By hiding liquidity information, Lightning protects users' financial privacy at the cost of making routing more probabilistic and sometimes causing payment failures. It's a deliberate design tradeoff prioritizing user sovereignty over network optimization.
