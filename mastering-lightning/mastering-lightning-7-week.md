# Mastering the Lightnin Network Seminar: 7-week format

## Resources

- [Mastering the Lightning Network Book (open source version)](https://github.com/lnbook/lnbook)
- [Mastering the Lightniong Network Book (physical version)](https://a.co/d/8gTqytB)

## Syllabus 

| Week | Reading                   | Topics                                                       |
|------|---------------------------|--------------------------------------------------------------|
| 1    | Appendix A, Chapters 2, 3 | Bitcoin Fundamentals Review, How the Lightning Network Works |
| 2    | Chapters 6, 7             | Network Architecture and Payment Channels                    |
| 3    | Chapters 8, 9             | Routing and Payment Forwarding                               |
| 4    | Chapters 10               | Onion Routing                                                |
| 5    | Chapters 11, 12           | Gossip, the Channel Graph, Pathfinding                       |
| 6    | Chapters 15               | Lightning Payment Requests                                   |
| 7    | Chapters 16               | Security and Privacy                                         |

### Week 1

Appendix A: Bitcoin Fundamentals Review

1. What's an UTXO?
2. What are locking and unlocking scripts? Where are they present in the Bitcoin transactions?
3. What's locking an UTXO to a secret? How are hashes used to achieve this?
4. What kinds of time locking mechanisms are available in Bitcoin transactions?
5. How can someone unlock the script shown in Example A-1? (This is quite hard to understand now, try your best).

Chapter 2: Getting Started

1. What are the functions a Lightning Wallet has to perform? How they differ from a Bitcoin wallet? Does the term wallet accurately describe the set of functions users needs? How could using this term be helpful or confusing for a new lightning user?
2. What do I have to do to join the Lightning Network and make and receive payments?
3. "Lightning is not a separate token or coin, it is Bitcoin." One of the loudest critiques of lightning is that this is NOT true. Can you articulate why they think that lightning is not bitcoin?

Chapter 3: How the Lightning Network Works

1. Describe the Lightning Network in terms of channels. What is needed to set up a "Lightning Network?" Is there only one Lightning Network?
2. Which parts of the Lightning Network are public? Which parts are private? How could we improve the privacy?
3. What data must a Lightning Network node keep in order to route payments and protect itself against loss of funds? As a node operator, how does this scale?
4. Why is revoking a transaction in bitcoin tricky? Why can't we simply invalidate older channel states?
5. Describe the differences between a bitcoin address and a Lightning Network payment invoice. What are the security assumptions of the invoice?

### Week 2

Chapter 6: Lightning Network Architecture

1. How important are each of the different network protocol layers? Is it possible to choose to implement some of them differently, whilst remaining compatible with the wider lightning network?
2. How does the Lightning Network layered architecture approach compare to that of the internet? What are some of the benefits of a layered architecture in general networks?
3. Looking at the network connection layer in the diagram, why would we need all the different types of network I/O protocols?

Chapter 7: Payment Channels

1. Considering how transactions work in the Bitcoin Protocol, what's a payment channel? What information does it keep track of?
2. What are the step to open a channel? Which transactions have to be created or signed?
3. Considering how transactions work in the Bitcoin protocol, what does it mean to send a payment accross a lightning channel?
4. The commitment transactions are "asymmetric". What does that mean, and why is that the case?
5. Why can't we keep the funding transaction off-chain until we close the channel?
6. What's the channel state and how peers keep track of it?
7. How peers cooperatively close the payment channel?
8. What happens if one node in the channel tries to unilaterally close the channel whilst there is a payment (HTLC) in-flight which has not been settled?

### Week 3

Chapter 8: Routing on a Network of Payment Channels

1 .What is the difference between routing and pathfinding? Who is responsible for these actions? Which one is part of LN's scaling model?
2. How payments are routed in the lightning network?
3. What's a HTLC? How does it ensure fairness in the protocol?
4. Explain the logic of the HTLC script shown in Example 8-1.
5. Alice pays Dylan through Bob and Carole. (A -> B -> C -> D). What happens if Carole reaches out to Alice and tells her the payment preimage that she received from Dylan, before telling Bob? In fact, why would she even tell Bob the preimage at all?
6. What's signature binding of HTLCs? Why do we need it?

Chapter 9: Channel Operation and Payment Forwarding

1. Why do we use HTLCs in local payments even if we are not routing?
2. What are the steps to make a local payment using HTLCs?
3. Alice and Bob have an in-flight HTLC which has timed out (expired). Alice would like to remove the HTLC from the channel, however Bob has gone offline. Is Alice in any danger? What action if any should she take?
4. What are all the ways in which an HTLC output script can be spent? If Alice sent the HTLC to Bob, who is able to spend which paths?
5. If Alice funded the channel between her and Bob, is Alice able to send HTLCs to Bob, and is Bob able to send HTLCs to Alice?

### Week 4

Chapter 10: Onion Routing

1. What's source based routing and how does it differ from the usual packet switching used in the Internet?
2. What's the principle behind onion routing? Which and how criptographic primitives are used to ensure it will perform as expected?
3. How to ensure that each hop will not be able to figure out its place in the route?
4. How each hop can access the information it requires to perform its job?
5. What's a keysend payment? How does it work?

### Week 5

Chapter 11: Gossip and the Channel Graph

1. How does a lightning node discovers peers using BOLT11?
2. What's the channel graph? Why lightning nodes have to build one?
3. What messages constitute the gossip protocol in the lightning network?

Chapter 12: Pathfinding and Payment Delivery

1. Not only successful, but also failed payment attempts can be used to gather information on the liquidity ranges of channels. Can this be abused to surveil channel balances, and what cost does the attacker incur?
2. What are the benefits and downsides of using source-based onion routing in LN, as compared to destination-based routing?
3. What happens when different nodes use different pathfinding algorithms? To what extent do they remain interoperable?
4. Maintaining a channel graph and performing pathfinding are computationally quite expensive. Could we offload that work to third parties? How would that impact an individual's privacy, security and ability to receive payments?
5. In which ways does pathfinding rely on messages from the gossip protocol?

### Week 6

Chapter 15: Lightning Payment Requests

1. Why can't we need invoices and can't use static payment addresses like in the Bitcoin base layer?
2. Alice (A) paid Carole (C) through Bob (B) (A->B->C). What happens when she makes the same payment again, with the same route and the same payment hash? What happens when instead of routing through Bob, she routes through Dylan (A->D->C)?
3. BOLT11 invoices cannot be safely reused. Why is this not true for Bitcoin (L1) addresses, ignoring the privacy implications?
4. Each invoice is signed with "[a] signature [that] allows the sender to verify that the payment request was indeed created by the destination of the payment." Why is this necessary? Why would anyone create an invoice that does not pay to their own node?
5. As per BOLT8, all communication on the Lightning Network is encrypted. Could BOLT11 invoices also be encrypted, and why are they not? Is that a security threat?

### Week 7

Chapter 16: Security and Privacy of the Lightning Network

1. What does it mean to de-anonymize someone? What's the anonymity set?
2. How the base layer and the lightning network differ in terms of privacy?
3. What kind of attacks are possible in the lightning network? Can any be used to steal bitcoin from lightning nodes?

