# Mastering Bitcoin Seminar: 7-week format

## Resources

- [Mastering Bitcoin Book (open source version)](https://github.com/bitcoinbook/bitcoinbook)
- [Mastering Bitcoin Book (physical version)](https://a.co/d/4UNf4jo)

## Syllabus 

| Week | Reading         | Topics                               |
|------|-----------------|--------------------------------------|
| 1    | Chapters 1, 2   | Why Bitcoin, System's Architecture   |
| 2    | Chapters 3, 4   | Bitcoin Core, Keys and Addresses     |
| 3    | Chapters 5, 6   | HD Wallets and Transactions          |
| 4    | Chapters 7, 8   | Script and Digital Signatures        |
| 5    | Chapters 9, 10  | Fees, network                        |
| 6    | Chapters 11, 12 | Blockchain, Mining and Consensus     |
| 7    | Chapters 13, 14 | Security Model and Lightning Network |

### Week 1

Chapter 1: Why Bitcoin

1. What were the major problems of Digital Currencies before Bitcoin? How did Bitcoin solve them?
2. What is the double-spend problem, and how did bitcoin solve it?
3. Why isn't Bitcoin designed with a hierarchical network structure?
4. What determines the rate of inflation in bitcoin?
5. Do you think it would be better if bitcoin transactions were reversible? Pros and Cons?

Chapter 2: System's Architecture

1. What are transaction inputs and outputs and what do they have to do with the transfer of value?
2. Why is a transaction fee needed and how is it calculated?
3. Why did Satoshi said transactions are "chains of digital signatures"? 
4. What is a UTXO? Whats the difference between UTXO and Account based model? Why did Bitcoin choose to stick with UTXO model?
5. How is Proof of Work mining similar to "needle in haystack" problem? What happens when two blocks are mined by different miners at the same height, how does the network decide which is the "right" block?

### Week 2

Chapter 3: Bitcoin Core

1. Why is Bitcoin Core called a "Reference Implementation"? What other implementations of Bitcoin are out there? Over 95% of Bitcoin nodes run Bitcoin Core, what's the problem of running a different implementation?
2. What are BIPs (Bitcoin Improvement Proposals)? What are their role in the Bitcoin development process?
3. What are some common reasons you would run your own full node?
4. What is the difference between a pruned node and a full (AKA archival) node? 

Chapter 4: Keys and Addresses

1. What is the relationship between private keys, public keys, and signatures? 
2. What is a Bitcoin address, and why are addresses used instead of raw public keys?
3. How do we know that the discrete log problem is hard to break? 
4. What are output and input scripts? How do they relate to receiving and spending Bitcoins?
5. What are the differences between P2PKH and P2SH?
6. What are Bech32 and Base58 addresses? What issues are associated with each?

### Week 3

Chapter 5: Wallet Recovery

1. What are the functions a Bitcoin wallet should perform? Does a wallet need to implement full node capabilities to function properly?
2. What is the difference between deterministic and non-deterministic wallets?
3. What are seeds, XPubs, XPrivs, and Chaincode?
4. Why does address reuse reduce privacy? Can you think of other de-anonymizing missteps that might happen due to bad user-experience design or lack of privacy education?

Chapter 6: Transactions

1. What are the different components of a Bitcoin transaction?
2. What are transaction inputs, and how are they constructed? What are unlocking scripts?
3. What parts of the transaction structure got affected with the segwit upgrade? Were there any new fields added to the transaction structure?
4. Compare a coinbase transaction to a normal bitcoin transaction and highlight the differences between the two.
5. What are UTXOs and how is the balance of a wallet calculated?
6. What are various sources of transaction malleability? How does segwit fix transaction malleability?

### Week 4

Chapter 7: Script

1. What is the difference between a locking script (scriptPubKey) and an unlocking script (scriptSig)? What is the difference between a redeem script and a witness script?
2. What are the different ways to create contracts in the script? Briefly highlight pros and cons of each.
3. Is the Turing incompleteness of Bitcoin's scripting language (SCRIPT) a feature or a deficiency?
4. What's P2PKH? How is it built?
5. What's P2SH? How is it built? What are the benefits of using P2SH over P2PKH? What are the drawbacks?
6. What's a scripted multisignature script? How is it built?

Chapter 8: Digital Signatures

1. What are digital signatures, where are they placed in a transaction, and what is their purpose?
2. Besides signing transactions, what other uses could digital signatures have?
3. What are the differences between Schnorr signatures and ECDSA signatures?
4. What is the Discrete Log Problem, and why is it important in Cryptography? What does it mean when we say "DLP is hard"? What would have happened if DLP wasn't a "hard" problem?

### Week 5

Chapter 9: Transaction Fees

1. Why do we need to pay transaction fees when we have block reward as an incentive? Is there a minimum fee that every transaction needs to pay? Is it a consensus rule or policy rule?
2. What challenges are associated with estimating appropriate fee rates for transactions?
3. What are the RBF rules for fee-bumping a transaction? Which rules are important to protect against DoS attacks?
4. What is transaction pinning? How is it a vulnerability for multiparty time-sensitive protocols such as LN?

Chapter 10: The Bitcoin Network

1. What is a peer-to-peer network? Give two examples of successful peer-to-peer networks that preceded Bitcoin.
2. How do new nodes discover peers on the network when they first come online?
3. Why is package relay particularly important for time-sensitive protocols like the Lightning Network?
4. How does the CPFP mechanism incentivize miners to confirm transactions? 
5. What are the privacy trade-offs in using a lightweight client?
6. Explain in brief what is a Mempool. The mempool is synchronized by the network as the blockchain?

### Week 6

Chapter 11: The Blockchain

1. Describe the structure of a block and what data does a block header contain?
2. What is a Merkle Tree and what significance does it have in the Blockchain?
3. What is a Light Client in context to Bitcoin? How do Light Clients verify transactions associated to their addresses?
4. Explain mainnet, testnet in brief. Can testnet coins have value?
5. Explain signet and regtest in brief. When would you use regtest for testing, and when Signet?

Chapter 12: Mining and Consensus

6. What are the goals of Bitcoin mining and what are the incentives for the miners?
7. Explain in brief how does the Bitcoin network attain emergent decentraliszed consensus.
8. What is Mining Difficulty? Why and how is it adjusted?
9. What factors could cause a change in Bitcoin’s consensus rules? How is a change in consensus rules achieved in a decentralized network like Bitcoin?
10. Contrast hard and soft forks. Why do we want to avoid hard forks? What are some common criticisms of a soft fork?

### Week 7

Chapter 13: Bitcoin Security

1. What could be the consequences of applying centralized security models to a decentralized network like Bitcoin?
2. Explain the concept of root of trust in security models. What should be the root of trust for Bitcoin applications?
3. How do developers of the protocol fit into the trust model? What safeguards are in place to ensure there are not any single points of failure?
4. How can we protect ourselves from the thousands of software components that run on our personal computers?

Chapter 14: Second-Layer Applications

3. What are payment channels in context to Bitcoin? How do they facilitate extremely high transaction throughput?
4. Explain what are funding and commitment transactions in context of payment channels.
5. What is a uni-directional payment channel? Give an example.
6. What is a bi-directional payment channel? Give an example.
7. Can a Bitcoin transaction be cancelled? Explain asymmetric revocable transactions.
8. What is a HTLC? Which OP-code is used to achieve it in context to payment channels?
