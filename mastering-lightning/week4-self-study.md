# 📚 Week 4 — Cheating with Valid Transactions and the Need for Revocation Keys

Last week, we introduced asymmetric commitment transactions as a mechanism to defend against cheating with outdated channel states.
Each party holds a different version of the commitment transaction, where:
- The output that pays the local party (the one broadcasting) is timelocked,
- The output that pays the remote party is immediately spendable.
This asymmetry gives the honest party time to react in case the other broadcasts an old state.

But this week, we will scrutinize that mechanism more closely and uncover a subtle but catastrophic vulnerability: even if everyone uses only the latest commitment transaction, it is still possible to steal funds — not by cheating with old state, but by exploiting how the protocol handles unilateral closes.

This is a turning point in our understanding.

We'll explore:

Why the current design is unsafe even if everyone follows the rules.
- How commitment transactions give each party the power to spend the other’s funds in the event of a close.
- Why this requires the introduction of a new mechanism: revocation keys.
- How revocation keys allow a party to “arm” the other with a secret that makes cheating self-destructive.

---

## 📙 Core Reading Assignment

1. Antonopoulos et al, Mastering the Lightning Network — Chapter 7, sections on Asymmetric Commitment Transactions, Revocation Keys, and Penalty Mechanisms.

2. Elle Mouton, [LN Things Part 3: Revocation in More Detail](https://ellemouton.com/posts/revocation/)

3. Brian Mancini, [Revocable Transactions with LN-Penalty](https://www.derpturkey.com/revocable-transactions-with-ln-penalty/)

---

## 📈 Optional Reading Assignment

- fiatjaf, [A Lightning Penalty Transaction](https://fiatjaf.com/73095980.html)

- BOLT 2 — [Peer Protocol for Channel Management](https://github.com/lightning/bolts/blob/master/02-peer-protocol.md) (raw specification, if you are feeling more confident)

---

### 🔍 Self-Study Questions

1. What is the goal of using asymmetric outputs in commitment transactions? How does this mechanism prevent a party from cheating with old state?
2. In the current protocol design (without revocation keys, with penalty mechanism), how is each party’s commitment transaction structured? What conditions must be met for either party to claim the funds?
3. Why is it important that a party delays their own output, but the counterparty receives theirs immediately?
4. Suppose Bob initiates a unilateral close using the most recent commitment transaction. Describe how Alice might still be able to steal Bob’s funds. What assumption is she violating?
5. Why is the problem from the previous question not solvable by longer timelocks or reordering outputs?
6. Why can’t we remove the asymmetric structure altogether and just use symmetric commitment transactions? What problems reappear?
7. In your own words, explain the specific scenario in which a party can close the channel honestly, but still be robbed by the counterparty.
8. What is the root cause of the vulnerability exposed this week? Is it about transaction validity? Signature reuse? Control over keys?
9. What mechanism could allow Bob to claim Alice’s output if she tries to cheat? What’s missing from our current protocol that would make this possible?
10. Explain the concept of a revocation key. What is its intended purpose in the protocol?
11. How does the act of revoking an old state prevent its use as a cheating strategy? What makes it final?
12. Why must revocation secrets only be revealed after both parties have signed the new channel state?
13. Suppose Alice gives Bob a revocation secret for a prior state. What power does Bob now have if Alice tries to broadcast that prior state?
14. How do revocation keys make old commitment transactions provably unsafe to broadcast? What economic incentive does this create?
15. How is this entire mechanism aligned with Bitcoin’s model of contracts and enforcement via spend conditions?
