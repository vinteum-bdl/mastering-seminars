### Week 1: Why Bitcoin and the System's Architecture

#### Reading

- Chapters 1, 2

#### Motivating questions

1. What were the major problems of Digital Currencies before Bitcoin? How did Bitcoin solve them?
2. What are the major components of the Bitcoin System? What does it mean by "consensus rules"?
3. Why did Satoshi said transactions are "chain of digital signatures"? What is a UTXO? Whats the difference between UTXO and Account based model? Why did Bitcoin choose to stick with UTXO model?
4. Why is Bitcoin Core called a "Reference Implementation"? What other implementations of Bitcoin are out there? Is it preferable to have many implementations of Bitcoin?

### Week 2: Transactions and Script

#### Reading

- Chapters 6, 7

#### Motivating questions

1. What are the different components of a Bitcoin transaction?
2. What are transaction inputs, and how are they constructed? What are unlocking scripts?
3. What parts of the transaction structure got affected with the segwit upgrade? Were there any new fields added to the transaction structure?
4. Compare a coinbase transaction to a normal bitcoin transaction and highlight the differences between the two.
5. What are UTXOs (Unspent Transaction Outputs), and how is the balance of a wallet calculated?
6. What is the difference between a locking script (scriptPubKey) and an unlocking script (scriptSig)? What is the difference between a redeem script and a witness script?
7. What's P2PKH? How is it built?
5. What's P2SH? How is it built? What are the benefits of using P2SH over P2PKH? What are the drawbacks?
6. What's a scripted multisignature script? How is it built?

### Week 3: Digital Signatures

#### Reading

- Chapters 8

#### Motivating questions

1. What are digital signatures, where are they placed in a transaction, and what is their purpose?
2. Besides signing transactions, what other uses could digital signatures have?
3. What are the differences between Schnorr signatures and ECDSA signatures?
4. What is the Discrete Log Problem, and why is it important in Cryptography? What does it mean when we say "DLP is hard"? What would have happened if DLP wasn't a "hard" problem?
5. How are ECDSA signature malleable? Does this malleability also occur in Schnorr signatures? Is there a way to fix this malleability?

### Week 4: Blockchain and Consensus

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

