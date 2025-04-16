# Mastering Bitcoin Seminar: 6-week format

| Week | Reading         | Topics                                                               |
|------|-----------------|----------------------------------------------------------------------|
| 1    | Chapters 1 to 4 | Why Bitcoin, System's Architecture, Bitcoin Core, Keys and Addresses |
| 2    | Chapters 5, 6   | HD Wallets and Transactions                                          |
| 3    | Chapters 7, 8   | Script and Digital Signatures                                        |
| 4    | Chapters 9, 10  | Fees, network                                                        |
| 5    | Chapters 11, 12 | Blockchain, Mining and Consensus                                     |
| 6    | Chapters 13, 14 | Security Model and Lightning Network                                 |

### Week 1: Why Bitcoin, System's Architecture, Bitcoin Core, Keys and Addresses

#### Reading

- Chapters 1, 2, 3 and 4

#### Motivating questions

1. What were the major problems of Digital Currencies before Bitcoin? How did Bitcoin solve them?
2. What are the major components of the Bitcoin System? What does it mean by "consensus rules"?
3. What are the two main components of a Transaction? What does each component include?
4. Why did Satoshi said transactions are "chain of digital signatures"? What is a UTXO? Whats the difference between UTXO and Account based model? Why did Bitcoin choose to stick with UTXO model?
5. How is Proof of Work mining similar to "needle in haystack" problem? What happens when two blocks are mined by different miners at the same height, how does the network decide which is the "right" block?
6. Why is Bitcoin Core called a "Reference Implementation"? What other implementations of Bitcoin are out there? Is it preferable to have many implementations of Bitcoin?
7. What are BIPs (Bitcoin Improvement Proposals)? What are their role in the Bitcoin development process?
8. What is a Bitcoin address, and why are addresses used instead of raw public keys?
9. What are the different kinds of Bitcoin addresses? Explain the differences between P2PKH and P2SH.
10. What is base58? What is bech32? How bech32 improves upon base58? Are there any problems in bech32? How are they solved?

### Week 2: HD Wallets and Transactions

#### Reading

- Chapters 5, 6

#### Motivating questions

1. What is a Bitcoin wallet?
2. What is the difference between deterministic and non-deterministic wallets?
3. What are XPubs, XPrivs, and Chaincode?
4. What are the different components of a Bitcoin transaction?
5. What are transaction inputs, and how are they constructed? What are unlocking scripts?
6. What parts of the transaction structure got affected with the segwit upgrade? Were there any new fields added to the transaction structure?
7. Compare a coinbase transaction to a normal bitcoin transaction and highlight the differences between the two.
8. What are UTXOs (Unspent Transaction Outputs), and how is the balance of a wallet calculated?
9. What are various sources of transaction malleability? How does segwit fix transaction malleability?

### Week 3: Script and Digital Signatures

#### Reading

- Chapters 7, 8

#### Motivating questions

1. What is the difference between a locking script (scriptPubKey) and an unlocking script (scriptSig)? What is the difference between a redeem script and a witness script?
2. What are the different ways to create contracts in the script? Briefly highlight pros and cons of each.
3. Is the Turing incompleteness of Bitcoin's scripting language (SCRIPT) a feature or a deficiency?
4. What's P2PKH? How is it built?
5. What's P2SH? How is it built? What are the benefits of using P2SH over P2PKH? What are the drawbacks?
6. What's a scripted multisignature script? How is it built?
7. What are digital signatures, where are they placed in a transaction, and what is their purpose?
8. Besides signing transactions, what other uses could digital signatures have?
9. What are the differences between Schnorr signatures and ECDSA signatures?
10. What is the Discrete Log Problem, and why is it important in Cryptography? What does it mean when we say "DLP is hard"? What would have happened if DLP wasn't a "hard" problem?
11. How are ECDSA signature malleable? Does this malleability also occur in Schnorr signatures? Is there a way to fix this malleability?

### Week 4: Fees, network

#### Reading

- Chapters 9, 10

#### Motivating questions

1. Why do we need to pay transaction fees when we have block reward as an incentive? Is there a minimum fee that every transaction needs to pay? Is it a consensus rule or policy rule?
2. What are the RBF rules for fee-bumping a transaction? Which rules are important to protect against DoS attacks?
3. What is transaction pinning? How is it a vulnerability for multiparty time-sensitive protocols such as LN?
4. What is a peer-to-peer network? Give two examples of successful peer-to-peer networks that preceded Bitcoin.
5. What is a block finding race? How does compact block relay prevent it?
6. How does a new node discover other Bitcoin nodes on the network in order to participate?
7. What are the privacy trade-offs in using a light weight client?
8. Explain in brief what is a Mempool and what is an Orphan Pool.

### Week 5: Blockchain, Mining and Consensus

#### Reading

- Chapters 11, 12

#### Motivating questions

1. Describe the structure of a block and what data does a block header contain?
2. What is a Merkle Tree and what significance does it have in the Blockchain?
3. What is a Light Client in context to Bitcoin? How do Light Clients verify transactions associated to their addresses?
4. Explain mainnet and testnet in brief. Can testned coins have value?
5. Explain signet and regtest in brief. When would you use regtest for testing, and when Signet?
6. What are the goals of Bitcoin mining and what are the incentives for the miners?
7. Explain in brief how does the Bitcoin network attain emergent decentraliszd consensus.
8. What is Mining Difficulty? Why and how is it adjusted?
9. What factors could cause a change in Bitcoin’s consensus rules? How is a change in consensus rules achieved in a decentralized network like Bitcoin?
10. Define a Hard fork and explain whether a new software implementation of the consensus rules is a pre-requisite for it.
11. Explain a soft fork. What are some common criticisms of a soft fork?

### Week 6: Security Model and Lightning Network

#### Reading

- Chapters 13, 14

#### Motivating questions

1. What could be the consequences of applying centralized security models to a decentralized network like Bitcoin?
2. Explain the concept of root of trust in security models. What should be the root of trust for Bitcoin applications?
3. What are payment channels in context to Bitcoin? How do they facilitate extremely high transaction throughput?
4. Explain what are funding and commitment transactions in context of payment channels.
5. What is a uni-directional payment channel? Give an example.
6. What is a bi-directional payment channel? Give an example.
7. Can a Bitcoin transaction be cancelled? Explain asymmetric revocable transactions.
8. What is a HTLC? Which OP-code is used to achieve it in context to payment channels?
