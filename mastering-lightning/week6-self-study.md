## Week 6 — Privacy in Lightning: Onion Routing and Beyond

### 🔹 1. Introduction

_This week we dive deeper into privacy protections in Lightning. We'll focus on how onion routing works, what information is hidden from intermediaries, and how the design choices of Lightning affect user anonymity._

_Focus on understanding that **every hop in the payment route learns as little as possible** — privacy is engineered carefully, not assumed!_

---

### 📙 2. Core Reading Assignment

- **Chapter 10**: Onion Routing (reviewed again, from a privacy-centric perspective)

---

### 📈 3. Optional Reading Assignment

- Explore recent proposals like blinded paths or rendezvous routing if you are interested in how privacy might be improved further in future versions of Lightning.

---

### 🔍 4. Self-Study Questions

#### Chapter 10: Onion Routing (Privacy Perspective)

1. **When sending a Lightning payment, what could intermediaries learn if no onion routing or encryption were used?**
2. **Why isn't simple encryption enough to protect sender and receiver privacy in Lightning?**
3. **How does onion routing ensure that each hop knows only the minimum necessary information?**
4. **What happens if an intermediary tries to tamper with the encrypted forwarding information in a payment packet?**
5. **At the end of a properly routed payment, who knows what? How much does the sender, intermediaries, and receiver each know?**

