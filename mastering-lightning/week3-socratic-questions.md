# 📚 Week 3 – Socratic Questions
**Theme:** Updating a Channel Means Replacing Commitment Transactions

### Question 1
> **When we say a Lightning payment was made, what changed inside the payment channel?**

**Purpose:**
- Shift student thinking from "sending coins" to "**updating local agreements** (commitments)."
- Make clear that **no coins "move"** — only agreements change.

**Example of Good Expected Answer:**
> When a Lightning payment happens inside a channel, no bitcoin moves on the blockchain. What changes is the channel state: the two participants collaboratively create new commitment transactions that reflect the updated balances. These new transactions replace the old ones as the valid view of who owns what, although all previous versions technically still exist until revoked.

### Question 2
> **Why can't we simply delete the old commitment transactions once a new one is agreed upon?**

**Purpose:**
- Highlight **Bitcoin's immutability** — once created and signed, transactions **exist** and can't be "deleted."
- Set up the revocation mechanism.

**Example of Good Expected Answer:**
> In Bitcoin, once a transaction is signed, it exists independently and can be broadcast at any time. There’s no way to physically delete it. In Lightning, this means old commitment transactions, even after a balance update, could still theoretically be broadcast by a malicious or mistaken party. Simply creating a new commitment transaction doesn't make the old ones invalid on their own.

### Question 3
> **What would happen if one party broadcasts an old commitment transaction after a channel balance has changed?**

**Purpose:**
- Make students realize the **fraud risk** inherent in having multiple valid transactions.
- Drive the necessity of **punishment mechanisms**.

**Example of Good Expected Answer:**
> If a party broadcasts an old commitment transaction, they could claim a higher balance than they actually deserve based on the current state. This would effectively allow them to steal funds from their counterparty. Because of this risk, Lightning must include a way to discourage and penalize the use of outdated channel states.

### Question 4
> **How does the revocation mechanism discourage cheating in Lightning channels?**

**Purpose:**
- Guide students to discover **revocation as a disincentive**.
- Introduce the **basic revocation key idea** without overwhelming technicalities.

**Example of Good Expected Answer:**
> In Lightning, every time a new commitment transaction is created, the counterparty is given a secret (the revocation key) that would allow them to immediately claim all the funds if an old transaction is broadcast. This creates a strong disincentive to cheat: if you try to publish an outdated transaction, your counterparty can punish you by taking all the funds involved in the channel.

### Question 5
> **If commitment transactions are just Bitcoin transactions, how complicated do you expect their scripts to be in order to implement revocation?**

**Purpose:**
- Demystify the technical implementation.
- Prepare students to see **basic scripts (multisig, timelocks, conditional spending paths)** are enough.

**Example of Good Expected Answer:**
> Although the behavior seems sophisticated, the scripts used are not very complex. They typically include two spending paths: one for the honest case (standard mutual agreement) and one for the punishment case (allowing the counterparty to claim all funds if a revoked transaction is used). This is accomplished with simple script primitives like multisignature checks, time delays, and secret reveals. Lightning leverages Bitcoin’s existing scripting language cleverly, without needing new opcodes or changes.
