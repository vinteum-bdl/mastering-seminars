# 📚 Week 6 – Socratic Questions
**Theme:** Onion Routing and Privacy in Multi-hop Payments

### Question 1
> **When you send a Lightning payment through multiple nodes, what kind of information could intermediaries potentially learn if no privacy protections were in place?**

**Purpose:**
- Make students think about **what is leaked by default** without extra measures.
- Set up the motivation for onion routing.

**Example of Good Expected Answer:**
> Without privacy protections, intermediaries could see the full payment path, including the sender and receiver, the amount being transferred, and possibly infer relationships between nodes. They could track user behavior, deanonymize users, and collect sensitive data about financial activity across the network.

### Question 2
> **Why can't we rely on encryption alone to protect privacy in Lightning routing?**

**Purpose:**
- Lead students to realize **encryption must be structured**, not just layered around the entire message.
- Prepare them for the **source routing vs. hop-by-hop knowledge** difference.

**Example of Good Expected Answer:**
> Simply encrypting the entire payment message wouldn't be enough because each intermediary needs to know specific forwarding information (like the next hop). If the entire message were encrypted, no one could forward it properly. Privacy must be designed carefully so that each node learns only what it strictly needs — nothing more. This requires a layered encryption model like onion routing.

### Question 3
> **How does onion routing protect the privacy of the sender and receiver during Lightning payments?**

**Purpose:**
- Introduce the **layered encryption concept** (like peeling an onion).
- Explain how each hop knows **only minimal information**.

**Example of Good Expected Answer:**
> Onion routing encrypts the payment instructions in multiple layers, each intended for a specific node along the route. Each node decrypts only its own layer, learning who to forward the payment to next, but not the final destination or the overall route. This way, no intermediary (except possibly the first and last) knows both where the payment came from and where it’s going, preserving user privacy across the network.

### Question 4
> **What prevents an intermediary node from tampering with or altering the forwarding instructions in a Lightning onion packet?**

**Purpose:**
- Highlight **integrity protections** alongside privacy.
- Show that onion routing isn’t just about secrecy, but also about correctness.

**Example of Good Expected Answer:**
> The encrypted layers are constructed in a way that prevents tampering. If an intermediary tries to alter forwarding information, they would not have the proper keys to correctly re-encrypt the onion packet for the next hop. Any tampering would be detected when the packet fails decryption at the next node. Additionally, certain integrity checks are built into the packet structure to ensure that unauthorized changes are detectable.

### Question 5
> **If you think about the sender, the intermediaries, and the receiver, who knows what in a properly onion-routed Lightning payment?**

**Purpose:**
- Synthesize the model: **who knows what information** at each step.

**Example of Good Expected Answer:**
> The sender knows the full route and all the necessary secrets to construct the onion. Each intermediary knows only the identity of the previous node, the next node, and the necessary information to forward the payment one step further. They do not know the original sender, the final receiver, or the overall path. The final receiver learns that they received a payment but does not know the full path the payment took to reach them. This division of knowledge maintains strong privacy across the network.
