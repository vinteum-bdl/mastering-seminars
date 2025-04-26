# 📚 Week 4 – Socratic Questions
**Theme:** Routing Chains Multiple Conditional Payments (HTLCs)

### Question 1
> **If a payment needs to travel through several channels, what would happen if each intermediary could claim the funds before passing them along?**

**Purpose:**
- Surface the **trust problem** in multi-hop payments.
- Lead students to see the need for **conditional payments**.

**Example of Good Expected Answer:**
> If intermediaries could freely claim funds before forwarding payments, they could steal the money or refuse to forward it after receiving it. This would make routing unreliable and unsafe. Without a mechanism to enforce atomicity, users could not trust the network to deliver payments securely across multiple hops.

### Question 2
> **How can we create a condition that forces each participant in a payment route to only get paid if the next one does too?**

**Purpose:**
- Push students toward discovering the **need for linked conditions**.
- Prepare the ground for introducing **HTLCs**.

**Example of Good Expected Answer:**
> We can use a secret that must be revealed to claim the funds. If each hop requires the same secret to claim their portion of the payment, and only the final recipient knows it initially, then the secret can propagate backward through the route. Each intermediary can only collect their payment if the next hop forwards the secret, enforcing fair behavior across the entire route.

### Question 3
> **What is the basic idea behind a Hash Time Locked Contract (HTLC)?**

**Purpose:**
- Formally introduce the **concept of HTLCs** as the solution to atomic multi-hop payments.

**Example of Good Expected Answer:**
> An HTLC is a special kind of Bitcoin output that can be spent by revealing a specific secret (a preimage corresponding to a known hash) or, if the payment is not completed in time, reclaimed by the sender after a timeout. This creates a conditional contract: the receiver must reveal the secret to claim the payment, or the sender can recover their funds if the receiver doesn't cooperate. In routing, this mechanism ensures that every participant only gets paid if the payment successfully reaches the final recipient.

### Question 4
> **Why is it important to have a time limit (a timeout) in each HTLC?**

**Purpose:**
- Help students understand the **timeout mechanism** protecting senders.
- Prevent funds from being locked indefinitely.

**Example of Good Expected Answer:**
> The timeout ensures that if something goes wrong — for example, if an intermediary disappears or refuses to forward the payment — the sender doesn't lose their funds indefinitely. After the timeout expires, the sender can reclaim the money. This protects the network against deadlocks and stuck payments, making it safe to try routing even in unreliable network conditions.

### Question 5
> **If we look closely, is routing a payment through Lightning really a single action, or something else?**

**Purpose:**
- Solidify the understanding that **routing is chaining independent local updates**, not one global operation.
- Combat intuitive but wrong "magic payment" ideas.

**Example of Good Expected Answer:**
> Routing a Lightning payment is not a single operation but a carefully coordinated chain of local updates across different channels. Each link in the chain updates its own local state based on the HTLC conditions, and the whole process is tied together through the shared secret. From the user’s perspective, it feels like one payment, but under the hood, it's multiple coordinated updates that must succeed or all safely cancel.
