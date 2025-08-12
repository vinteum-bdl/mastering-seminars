# 📚 Week 7 — Pathfinding, Gossip, and Liquidity

We now understand how to build secure payment channels, how to route payments across independent channels using HTLCs, and how onion routing helps preserve privacy.

But we’ve mostly taken one thing for granted: How does Alice even know that Bob has a channel to Carol?
And how does she know how much liquidity Bob has in that channel — or which paths are viable to begin with?

This week, we explore the network-level infrastructure that makes Lightning routing possible:
- How peers learn about the existence of channels;
- How they discover public node identities, channel balances, and fee policies;
- How pathfinding is performed — and what makes it so different from routing on the internet.

Unlike IP routing, which uses best-effort hop-by-hop forwarding, Lightning uses source routing:
The sender must learn enough about the network to construct the entire path in advance — a nontrivial task in a decentralized, liquidity-constrained, privacy-conscious environment.

This week, we’ll dive into:
- The gossip protocol used to spread information about the network topology;
- The limitations of this approach (especially around private channels and liquidity);
- The heuristics used by Lightning implementations to choose routes;
- The tensions between privacy, reliability, and discoverability.
This is a great opportunity to reflect on Lightning not just as a set of contracts and scripts, but as a living, dynamic, global network that must balance coordination, efficiency, and user autonomy.

---

## 📙 Core Reading Assignment

1. Antonopoulos et al, Mastering the Lightning Network — Chapter 5: Routing
- Focus on sections: Gossip Protocol, Route Finding, and Channel Liquidity

---

## 📈 Optional Reading Assignment

- Rene Pickhardt and Stefan Richter, [Optimally Reliable & Cheap Payment Flows on the Lightning Network](https://arxiv.org/abs/2107.05322)

---

## 🔍 Self-Study Questions
1. What information about Lightning channels is publicly advertised on the network?
2. What is the gossip protocol, and how does it help peers build a map of the network?
3. What are the limitations of the gossip model? What kinds of information does it not reveal?
4. What is the difference between public and private channels? How does that distinction affect routing and discoverability?
5. How do routing nodes decide what fee policies to advertise? What role do these play in pathfinding?
6. Why must Lightning use source routing instead of hop-by-hop forwarding like in IP networks?
7. What does it mean that the sender is responsible for choosing the entire payment route?
8. Why is the current balance of a channel not known to the rest of the network? How does this affect route selection?
9. What kinds of failures can occur when attempting a multi-hop payment? What mechanisms exist to retry or adjust the route?
10. What is probing in the context of routing? How is it used to estimate liquidity — and how might it violate privacy?
11. What is a multi-path payment (MPP)? Why might a sender use this technique?
12. What are the tradeoffs involved in route selection: cost, privacy, success probability, and speed?
13. How do Lightning implementations like LND and CLN attempt to guess which channels have sufficient liquidity?
14. What are the main ideas behind Pickhardt Payments? How do they improve upon the default routing heuristics?
15. If you were to design your own Lightning routing algorithm, what data would you wish you had access to? What tradeoffs would you face?
