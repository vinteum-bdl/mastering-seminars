# 📚 Week 7 – Socratic Questions
**Theme:** Current Challenges and Future Directions of Lightning

### Question 1
> **If the Lightning Network works well for many payments today, why are developers still working on improvements? What problems remain unsolved?**

**Purpose:**
- Push students to realize **LN is not "finished"**, and that real-world challenges remain.

**Example of Good Expected Answer:**
> While Lightning enables fast and cheap Bitcoin payments, it still faces important challenges. Managing liquidity efficiently, finding reliable routes, handling mobile and intermittent nodes, improving privacy, making backup and recovery safer, and reducing the burden of maintaining channel graphs are all active areas of development. Each of these challenges affects usability, reliability, and decentralization, and solving them is crucial for broader adoption.

### Question 2
> **Why is liquidity management such a difficult problem in Lightning?**

**Purpose:**
- Make students understand **capital inefficiency** and **unbalanced channels** as real operational limitations.

**Example of Good Expected Answer:**
> In Lightning, payments can only flow if there is sufficient outbound liquidity along a path. Channels can easily become unbalanced over time, where one side has all the funds. Rebalancing requires either routing payments carefully or opening new channels, both of which can be costly and complex. There is no perfect solution yet for dynamically maintaining liquidity where it is needed most without friction or centralization.

### Question 3
> **If Lightning payments depend on finding good routes, what happens as the network grows larger and more complex?**

**Purpose:**
- Surface **scalability tradeoffs** in decentralized routing.

**Example of Good Expected Answer:**
> As the network grows, the number of nodes and channels increases, making it harder for individual nodes to maintain an accurate and up-to-date view of the network. Pathfinding becomes computationally heavier, and failures due to liquidity uncertainty become more common. Some proposals aim to reduce this burden by introducing techniques like route hints, trampoline routing, or even partial delegation of routing, but these raise their own privacy and trust tradeoffs.

### Question 4
> **What new technologies or protocol upgrades are being explored to improve Lightning's privacy and efficiency?**

**Purpose:**
- Show students the **living nature of protocol evolution**.

**Example of Good Expected Answer:**
> Several new technologies are being researched and developed. These include PTLCs (Point Time Locked Contracts) for more flexible and private conditional payments, blinded paths to protect receiver identity, and more sophisticated onion routing schemes. Some proposals like rendezvous routing and trampoline routing aim to make routing more robust and private. Each innovation seeks to address current shortcomings without sacrificing Bitcoin's core principles.

### Question 5
> **If you could design one improvement for the Lightning Network, based on what you've learned, what would it be?**

**Purpose:**
- Encourage students to **synthesize knowledge**, **think creatively**, and **engage as future contributors**.

**Example of Good Expected Answer:**
> (Open-ended — mentors should encourage any thoughtful response.)
> A good answer would demonstrate understanding of Lightning’s real challenges — for example, proposing better liquidity discovery without compromising privacy, enhancing mobile node support, creating safer backup protocols, or optimizing routing under uncertain liquidity conditions. The key is showing awareness of tradeoffs and technical grounding in the proposal.
