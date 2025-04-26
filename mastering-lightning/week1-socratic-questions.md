# 📚 Week 1 – Socratic Questions
**Theme:** Bitcoin as a Language for Financial Contracts

### Question 1
> **When we say "Bitcoin moves money," what *actually* moves in the Bitcoin network?**

**Purpose:**
- Break the naive image of “coins moving around.”
- Lead students to recognize that **Bitcoin moves valid transactions**, not discrete coins.

**Example of Good Expected Answer:**
> In Bitcoin, nothing physically moves like coins or tokens. Instead, what "moves" are *transactions* that reference previous outputs and create new ones. Each transaction declares that certain previous outputs (UTXOs) are being spent and new outputs are being created for new owners. The network validates these transactions and updates the shared ledger accordingly. The "movement of money" is, in reality, a reorganization of ownership records enforced by the network’s consensus rules.

### Question 2
> **What is a UTXO, and why can it be thought of as both money and a contract?**

**Purpose:**
- Help students see a UTXO as both **a bearer of value** and **a set of spending conditions**.

**Example of Good Expected Answer:**
> A UTXO (Unspent Transaction Output) represents a specific amount of bitcoin that can be spent by satisfying certain conditions. It is "money" because it holds value, but it is also a "contract" because it contains a locking script — a program that specifies what must be proven or revealed to claim the funds. For example, the locking script might require a valid signature corresponding to a particular public key. Thus, every UTXO embeds rules that define under what circumstances ownership can be transferred.

### Question 3
> **In a Bitcoin transaction, what roles do the input and output scripts play?**

**Purpose:**
- Help students distinguish between **creating conditions (outputs)** and **fulfilling them (inputs)**.

**Example of Good Expected Answer:**
> In a Bitcoin transaction, **output scripts** create new conditions for future spending: they define what a future spender must provide (such as a valid signature) to claim the funds. **Input scripts** fulfill the conditions of previous outputs: they supply the necessary data, like a digital signature and public key, proving that the spender has the authority to use those funds. Together, input and output scripts form a self-contained validation system that enforces ownership transfer without relying on trust.

### Question 4
> **Why is it important that Bitcoin transactions are "programmable" with scripts, rather than just simple messages of value transfer?**

**Purpose:**
- Show that Bitcoin's **programmability** enables **complex financial arrangements** (essential for things like Lightning).

**Example of Good Expected Answer:**
> Bitcoin's scripting system allows transactions to encode complex conditions for spending funds, not just simple transfers from one party to another. This flexibility enables powerful financial mechanisms like multisignature wallets, time-locked contracts, escrow services, and payment channels. Without programmable scripts, Bitcoin would be limited to basic value transfer and could not support second-layer protocols like Lightning, which depend on creating and updating specific contract conditions dynamically.

### Question 5
> **If Lightning uses Bitcoin transactions under the hood, what might be one advantage of thinking about Lightning as "Bitcoin transactions disciplined by a protocol" rather than a separate thing?**

**Purpose:**
- Help students integrate Lightning into their Bitcoin mental model, avoiding the misconception that Lightning is a different currency.

**Example of Good Expected Answer:**
> Thinking of Lightning as "Bitcoin transactions disciplined by a protocol" highlights that Lightning payments are not separate from Bitcoin — they are a careful choreography of Bitcoin transactions, some real and some potential. Every balance update in Lightning corresponds to a Bitcoin transaction that could, if needed, be broadcast to the Bitcoin blockchain. This framing helps maintain conceptual clarity: Lightning extends Bitcoin's transaction model rather than creating a new form of money.
