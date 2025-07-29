# 📚 Week 6 — Deep Dive into Privacy

So far, we’ve explored how the Lightning Network enables secure, scalable payments by using Bitcoin transactions in a coordinated off-chain protocol.
We’ve seen how channels are opened, updated, closed, and how multi-hop payments can be routed across the network using HTLCs.

But what about privacy?

While Lightning is often marketed as a privacy-enhancing solution for Bitcoin, the reality is more nuanced.
Some aspects of Lightning offer better privacy than on-chain payments.
Others introduce new risks — and new design challenges.

This week, we focus on understanding:
- What kinds of information are visible to different parties in the Lightning Network;
- Which parts of a routed payment are exposed to intermediaries;
- How HTLCs — while enabling atomic multi-hop payments — leak information about the payment path;
- How onion routing (inspired by Tor) is used to reduce this leakage and protect user privacy;
- What limitations and tradeoffs still exist in Lightning’s privacy model.

By the end of this week, you should be able to reason about the threat model of a Lightning payment and describe how privacy is (or isn’t) preserved at different layers of the protocol.

---

## 📙 Core Reading Assignment

1. Antonopoulos et al, Mastering the Lightning Network — Chapter 5: Lightning Routing
  - Sections on onion routing, Sphinx packets, and privacy implications

---

## 📈 Optional Reading Assignment

- BOLT 4 — Onion Routing Protocol

---

## 🔍 Self-Study Questions
1. How does Lightning improve privacy compared to regular on-chain Bitcoin payments? In what ways is it worse?
2. When Alice sends a payment to Carol via Bob, what parts of the payment do each of the participants (Alice, Bob, Carol) see?
3. What information is leaked to intermediaries during a Lightning payment? Can Bob learn that Carol is the final recipient?
4. What does it mean for a payment to be routable, but not private?
5. Why are HTLCs a source of privacy leakage in the Lightning Network? What information do they reveal?
6. How does onion routing help preserve privacy during multi-hop payments?
7. What is a Sphinx packet? What information does it carry, and how does it protect the payment path?
8. Describe how an intermediary node (e.g., Bob) processes an incoming onion-routed HTLC.
9. What is the difference between source routing and hop-by-hop routing? Which one does Lightning use, and what are the privacy implications?
10. Why does the sender have to know the full path in Lightning? How does this affect privacy and scalability?
11. What is trampoline routing, and how does it attempt to improve privacy and scalability at the same time?
12. Are onion routing and HTLCs enough to guarantee payment privacy? What attacks still remain possible (e.g., timing, probing, channel closure inference)?
13. In what ways does channel structure (e.g., public vs private channels) influence network-level privacy?
14. How does path length affect privacy in Lightning? Is a longer path always more private?
15. What are some open challenges in improving privacy for Lightning? What tradeoffs do proposed solutions make (e.g., computational cost, route reliability)?
