---
title:  "SCA Journal Club: Bitcoin Whitepaper"
subtitle:
date:   2020-12-31 00:00:00
update:
author: Joe Cheung
description:
tags: cryptocurrency
wordcount: 3754-5195
---

*\[Epistemic status: just going through the Bitcoin whitepaper. The first 12 headings correspond to the parts in the whitepaper. I wish I had any investment advice.\]*

1. TOC
{:toc}

Inspired by Ben Reinhardt’s [Seminal Paper Club](https://benjaminreinhardt.com/seminal-paper-club/), I wanted to read more seminal papers starting with Satoshi Nakamoto’s Bitcoin whitepaper [*<span class="underline">Bitcoin: A Peer-to-Peer Electronic Cash System</span>*](https://bitcoin.org/bitcoin.pdf). It’s surprisingly readable, definitely recommended.

Bitcoin is a [<span class="underline">clever but ugly</span>](https://www.gwern.net/Bitcoin-is-Worse-is-Better#) solution to the double-spending problem using a peer-to-peer distributed timestamp server to generate computational proof of the chronological order of transactions. While Bitcoin is far from the first attempt at electronic money, and in fact involves no major mathematical or cryptographic breakthroughs, it has become a [<span class="underline">Schelling point</span>](https://nakamoto.com/bitcoin-becomes-the-flag-of-technology/) synonymous with cryptocurrency, and remains by far the [<span class="underline">largest</span>](https://www.coinbase.com/learn/crypto-basics/what-is-bitcoin) one by market capitalization and trading volume.

Key dates:
- 05/2007: coding began in C++
- 08/2008: domain name “bitcoin.org” registered and feedback on drafts of the whitepaper was sought from [<span class="underline">Wei Dai</span>](https://en.wikipedia.org/wiki/Wei_Dai) and [<span class="underline">Hal Finney</span>](https://en.wikipedia.org/wiki/Hal_Finney_\(computer_scientist\))
- 31/10/2008: the whitepaper was published to a public cryptography mailing list
- 03/01/2009: open-sourced and launched the Bitcoin network with the mining of the genesis block
    - embedded in the coinbase was “[<span class="underline">The Times 03/Jan/2009 Chancellor on brink of second bailout for banks.</span>](https://www.thetimes.co.uk/article/chancellor-alistair-darling-on-brink-of-second-bailout-for-banks-n9l382mn62h)” A comment on the instability caused by fractional-reserve banking as seen in quantitative easing since the 2008 Financial Crisis.
- 12/01/2009: first Bitcoin transaction of 10 BTC from Satoshi to Finney
- 05/2010: first commercial Bitcoin transaction of two Papa John’s pizza for 10,000 BTC (288,755,000 USD as of 2020/12/31)
- 04/11: control of Bitcoin website and repository was handed off to [<span class="underline">Gavin Andresen</span>](https://en.wikipedia.org/wiki/Gavin_Andresen) (600,000-700,000 BTC still sits at Satoshi’s address today)

![](/images/2020-12-31-Bitcoin-Whitepaper/image5.png)  
[*<span class="underline">Satoshi’s first email.</span>*](https://www.metzdowd.com/pipermail/cryptography/2008-October/014810.html)

## Introduction

Satoshi begins by pointing out the inherent weaknesses of relying almost exclusively on financial institutions to serve as trusted third parties to process electronic payments. Transactions can be reversed when banks mediate disputes, which increases transactional cost, limits minimum practical transaction size, and providers non-reversible services risk not getting paid. Third parties are:

- untrustworthy;
- frequently hacked;
- give too much information to the government without consent;
- and accept a certain percentage of fraud as unavoidable thus increasing everyone’s cost.

Bitcoin replaces trust with cryptographic proof by allowing any 2 willing parties to transact directly with each other without the need for a trusted third party.

As [<span class="underline">William Stanley Jevons</span>](https://plato.stanford.edu/entries/william-jevons/) famously defined in [<span class="underline">Money and the Mechanism of Exchange</span>](https://www.econlib.org/library/YPDBooks/Jevons/jvnMME.html), the properties of money are:

- [<span class="underline">store of value</span>](https://en.wikipedia.org/wiki/Store_of_value) i.e. non-perishable and consistently valued by others;
- [<span class="underline">medium of exchange</span>](https://en.wikipedia.org/wiki/Medium_of_exchange);
- and [<span class="underline">unit of account</span>](https://en.wikipedia.org/wiki/Unit_of_account).

Anything can serve as money as long as there is stable social consensus about its value i.e. *trust*.

Though the overwhelming majority of bitcoin transactions take place on a cryptocurrency exchange, rather than being used in transactions with merchants. Delays processing payments through the blockchain of about ten minutes make bitcoin use very difficult in a retail setting. But hey, [<span class="underline">Sci-Hub</span>](https://www.coindesk.com/blackballed-by-paypal-scientific-paper-pirate-takes-bitcoin-donations) runs on Bitcoin donations\!

## Transactions

**Cryptographic proof**

Satoshi defines an electronic coin as a chain of digital signatures. A digital signature is where the public-key encrypts plaintext, and the private-key deciphers the ciphertext. In Bitcoin, your key pair is itself your identity, hence the pseudonymity. A digital signature can be expressed as:

- Sign(message, KEYprivate) = 256-bit signature
- Verify(message, 256-bit signature, KEYpublic) = T/F

![](/images/2020-12-31-Bitcoin-Whitepaper/image10.png)

Of course, it is a bit more complicated in practice. [<span class="underline">Public-key cryptography</span>](https://en.wikipedia.org/wiki/Public-key_cryptography) began when the [<span class="underline">RSA</span>](https://en.wikipedia.org/wiki/RSA_\(cryptosystem\)) (Rivest–Shamir–Adleman) cryptosystem was invented in 1977 from the trapdoor function (functions that are harder to compute than to verify) of integer factoring. For instance, it is harder to find the prime factors of 177 but easier to verify the multiple of 3\*59. RSA key size has ballooned to the current recommendation of 2048 bits to compensate for [<span class="underline">Moore’s Law</span>](https://en.wikipedia.org/wiki/Moore%27s_law).

Almost all cryptocurrency deploys [<span class="underline">Elliptic Curve Digital Signature Algorithm</span>](https://en.wikipedia.org/wiki/Elliptic_Curve_Digital_Signature_Algorithm) (ECDSA), and Bitcoin popularised using [<span class="underline">secp256k1</span>](https://en.bitcoin.it/wiki/Secp256k1). It is a type of [<span class="underline">elliptic-curve cryptography</span>](https://en.wikipedia.org/wiki/Elliptic_curve_cryptography) (ECC) which is built out of the trapdoor function of multiplying over elliptic curves in finite fields. Our best algorithms for computing discrete logarithms over certain elliptic curves are exponential, while our best algorithms for factoring integers are sub-exponential, hence integer factoring is easier (though not all curves are the same). Standard ECC keys are 256 bits, about 1/10 the size of RCA keys, and collision-resistant i.e. two inputs do not hash to the same output.

The security of an encryption scheme is established by a [<span class="underline">reduction</span>](https://en.wikipedia.org/wiki/Provable_security) i.e. a proof that if this scheme is broken, another known hard problem can also be solved. If reduction is not enough, security is likely to be proportional to the number of mathematicians who failed at solving it\! Because [<span class="underline">P vs NP</span>](https://en.wikipedia.org/wiki/P_versus_NP_problem) is still unsolved, it is an open question whether integer factoring and computing discrete logarithms are truly hard NP-complete problems i.e. no algorithm can solve in faster than in exponential time (e.g. computing perfect strategy in chess). However, [<span class="underline">Shor’s algorithm</span>](https://en.wikipedia.org/wiki/Shor%27s_algorithm) can efficiently compute discrete logarithms on a quantum computer. Luckily, a Bitcoin address is the 160-bit hash of a 256 bit public-key for compression, which provides quantum resistance; a quantum computer can only be quadratically more efficient, so there is still 80-bit security.

[<span class="underline">Public-key cryptography</span>](https://nakamoto.com/public-key-cryptography/) is a kind of asymmetric encryption, as compared to symmetric encryption that uses the same key for both encryption and decryption. As it happens, the former is much slower (measured in milliseconds i.e. 10<sup>-3</sup> s) than the latter (measured in microseconds i.e. 10<sup>-6</sup> s). Hence, protocols generally use asymmetric cryptography to establish identities, then create a shared session key to continue communicating over a symmetric cipher.

Any public-key cryptography system depends on robust key generation, and turns out computers are deterministic machines that don’t always generate high-quality randomness\! Insufficient [<span class="underline">entropy</span>](https://en.wikipedia.org/wiki/Entropy_\(computing\)) in key generation has led to many attacks against cryptosystems, for example a [<span class="underline">bug</span>](https://bitcoin.org/en/alert/2013-08-11-android) in Android led to many Bitcon apps generating insecure private keys that were quickly cracked. This is why in practice people always say *never roll your own crypto*.

**Double-spending problem**

Satoshi raises the main problem that Bitcoin solves: [<span class="underline">double-spending</span>](https://en.wikipedia.org/wiki/Double-spending). Alice can pay the same digital $10 to Bob and Charlie, neither of whom can tell which copy is real. [<span class="underline">PayPal</span>](https://en.wikipedia.org/wiki/PayPal)’s anti-counterfeit effort involved a single database with no direct user access, but Cypherpunks tried to solve the double spend problem without having to trust a third party. For example, [<span class="underline">e-gold</span>](https://en.wikipedia.org/wiki/E-gold#:~:text=E%2Dgold%20was%20a%20digital,to%20other%20e%2Dgold%20accounts.) was collateralised with gold, while [<span class="underline">DigiCash</span>](https://en.wikipedia.org/wiki/DigiCash) was collateralised with USD, but neither was beyond state control. [<span class="underline">b-money</span>](https://en.bitcoin.it/wiki/B-money) by Wei Dai and [<span class="underline">BitGold</span>](https://www.investopedia.com/terms/b/bit-gold.asp) by Nick Szabo were proposed schemes vulnerable to sybil attacks where a botnet can determine the outcome of a majority vote.

## Timestamp server

If Alice sends double-spend by sending Bitcoin to Bob and Charlie, Bob can verify that it is indeed from Alice using Alice’s public-key, but so can Charlie. To solve the double-spending problem without relying on third-party minting, all transactions must be public and every participant must adhere to a single history of transactions to determine which transaction was received first.

Satoshi proposes a timestamp server as a form of public ledger. It is a series of (hash, timestamp) where it calculates the hash of a block of previous timestamps and publishes it widely.

## Proof-of-work

A [<span class="underline">cryptographic hash function</span>](https://en.wikipedia.org/wiki/Cryptographic_hash_function) inputs a string of characters of arbitrary length and maps it to another string of characters of fixed length, for example SHA-256(message) = 32 byte hash. Hash functions have a few important properties:

- *Deterministic*: the same message always results in the same hash
- *One-way*: generating the message from the hash can only be brute-forced
- *Avalanche-effect*: changing a single bit (severely) jumbles other bits i.e. similar inputs have outputs with no discernible relationship
- *Collision-resistant*: i.e. two inputs do not hash to the same output
    - [<span class="underline">SHA-256</span>](https://en.wikipedia.org/wiki/SHA-2) has a range of 2<sup>256</sup> while number of atoms in the universe is around 2<sup>260</sup> so it is very unlikely to produce hash collision by pigeonholing

Trouble is that for any hash function you can actually always do better than brute-force by using a [<span class="underline">birthday attack</span>](https://en.wikipedia.org/wiki/Birthday_attack#:~:text=A%20birthday%20attack%20is%20a,between%20two%20or%20more%20parties.): how many guests need to be at a party on average so two guests share the same birthday? Surprisingly, you only need 23 guests, as it gives 253 unique pairs (n(n-1))/2, each having a 1/365 chance of sharing a birthday, i.e. 50.7% chance. Hence √n is a good approximation for the 50% threshold for a birthday collision. Current computational tractability is around 2<sup>80</sup>, so a SHA-128 can be birthday-attacked by brute-forcing 2<sup>64</sup>. This is why if we want 128-bit security, we need a 256-bit hash function.

In a [<span class="underline">proof of work</span>](https://en.wikipedia.org/wiki/Proof_of_work) (PoW) you usually have a challenge string *c* and you are looking for a nonce *n* such that hash(*c*+*n*) will result in a string with a certain number of leading zeroes. Let’s say our challenge string was “Hello, world\!” and our target was to get a SHA-256 hash beginning with ‘000’. One way to go about it is to start with a nonce of ‘0’ and progressively increment it until you get a hash starting with ‘000’. In this case that would take 4251 tries. If the hash is required to start with 30 zeros, the probability is 1/(2<sup>30</sup>) about 1 in a billion.

The only way to produce a satisfactory nonce is by guessing a lot of times i.e. spending a lot of computational power. Once PoW is done it can be verified easily by hashing the block containing the nonce. A block also contains the list of all previous transactions, and the previous hash thus chaining to the previous block, so changing a block would change the hash of the block and all subsequent blocks, requiring all the PoW to be redone.

Thus, trust is placed at the longest *blockchain* which has the greatest PoW computational power invested. Users keep their own copy of the longest blockchain that has the addition of the new block from miners, producing a decentralised consensus.

A scammer has to add blocks faster to maintain the longest blockchain forever than all honest nodes adding to the blockchain, which becomes harder exponentially as the blockchain grows. As long as the majority of CPU power is controlled by honest nodes, it is infeasible for the slower attacker to catch up to the longest blockchain. To compensate for Moore’s Law and the number of miners, the number of zeroes required in the hash is increased periodically to maintain about 10 mins to find the nonce to add a new block.

![](/images/2020-12-31-Bitcoin-Whitepaper/image9.png)
[*<span class="underline">Semi-log plot of relative mining difficulty.</span>*](https://commons.wikimedia.org/wiki/File:History_of_Bitcoin_difficulty.svg#/media/File:History_of_Bitcoin_difficulty.svg)

Unfortunately, [<span class="underline">centralised crypto mining</span>](https://www.investopedia.com/investing/why-centralized-crypto-mining-growing-problem/) is a growing problem as those with enough money in areas that subsidise electricity are concentrating computing power in the hands of a few.

## Network

Satoshi proposes 6 steps to run the network:

1. New transactions are broadcast to all nodes
2. Each node collects new transactions into a block
3. Each node works on finding a difficult proof-of-work for its block
4. When a node finds a proof-of-work, it broadcasts the block to all nodes
5. Nodes accept the block only if all transactions in it are valid and not already spent
6. Nodes express their acceptance of the block by working on creating the next block in the chain, using the hash of the accepted block as the previous hash

**P2P Network**

Before Bitcoin, decentralised [<span class="underline">peer-to-peer</span>](https://en.wikipedia.org/wiki/Peer-to-peer) (P2P) networking was pioneered by [<span class="underline">Napster</span>](https://en.wikipedia.org/wiki/Napster) in 1999 which was a cross between client-server and P2P network: client query search is indexed at Napster server, while the file is fetched directly from peers. By 2009, [<span class="underline">BitTorrent</span>](https://en.wikipedia.org/wiki/BitTorrent) accounted for 70% (\!) of all internet traffic.

In a P2P network, each peer makes queries and responds to queries. In contrast, in a centralised client-server model, the central server or a fleet of servers behind a load balancer provides a service per each clients’ query.

In the [<span class="underline">Bitcoin P2P network</span>](https://nakamoto.com/bitcoins-p2p-network/), the bootstrap node is the entry point, from which point you can then organically find new peers. Of course, the danger with a bootstrap node is that if it is not authenticated, it could be malicious and perform a [<span class="underline">man-in-the-middle</span>](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) or [<span class="underline">eclipse attack</span>](https://www.usenix.org/system/files/conference/usenixsecurity15/sec15-paper-heilman.pdf). In Bitcoin Core, the canonical Bitcoin implementation, these bootstrap nodes are [<span class="underline">hard-coded</span>](https://github.com/bitcoin/bitcoin/blob/master/src/chainparams.cpp) as trusted DNS servers maintained by the core developers.

Pros of P2P:

- *Crash fault tolerant*: even if individual nodes fails, the system functions, which is crucial to scalability
- *Censorship resistant*: even if individual node is censored, the network is not censored

Cons of P2P:

- A coherent single snapshot of the global state only possible in centralised architecture
- High churn rate when peers go online and offline means demanding high fault tolerance
- Hard to moderate and cannot enforce quality control (Bitcoin uses a reputation system where infractions score points, and enough points result in shadowbans)
- Lack of network-level privacy (pseudonymity provides some privacy, but if you connect to just 50% of the network, you can see the “message wave” propagate from the sender and figure out their IP address)

![](/images/2020-12-31-Bitcoin-Whitepaper/image16.png)
[*<span class="underline">In principle, you can connect to all 11303 nodes to become a supernode to reconstruct the flow of messages post hoc from a god's-eye view.</span>*](https://bitnodes.io/)

Since 2015, Bitcoin has used diffusion to propagate gossip messages, where the client waits a random exponential delay before gossiping to its peers. It can be written as:

```
def gossip(msg):
  for peer in peers:
    schedule_send(peer, msg, wait=np.random.exponential(1.0 / theta))
```

Unfortunately, there is still a lot to be done to improve Bitcoin’s network-level privacy,

## Incentive

Creating a block by doing the PoW i.e. mining, is rewarded with a small amount of Bitcoin in a special transaction called a *coinbase*, thus introducing new bits of Bitcoin to the economy. Each block is limited to around 2,400 transactions, compared to [<span class="underline">Visa</span>](https://en.wikipedia.org/wiki/Visa_Inc.) handling on average 1,700 transactions/second and up to 24,000 transactions/second (which is known as [<span class="underline">the Bitcoin scalability problem</span>](https://en.wikipedia.org/wiki/Bitcoin_scalability_problem)). To incentivise miners to include Alice’s payment to Bob in a block, Alice can optionally include a transaction fee for the miner, which also incentivises attackers to choose putting computational power to mining over scamming.

Every 210,000 blocks, around 4 years, the reward for PoW is halved. As the reward decreases geometrically over time, it creates an artificial scarcity as there will never be more than 21 million Bitcoin. The limit will be reached circa 2140, and further proof of work to continue the blockchain will be rewarded solely by transaction fees.

![](/images/2020-12-31-Bitcoin-Whitepaper/image7.png)
[*<span class="underline">Total Bitcoins in circulation.</span>*](https://commons.wikimedia.org/wiki/File:Total-bitcoins.svg#/media/File:Total-bitcoins.svg)

Mining Bitcoin gets progressively harder as the network grows, and so eventually mining it en masse requires a lot of hardware, electricity, and cooling. This creates a breakeven point for mining, which is a factor that was not anticipated by Satoshi.

## Reclaiming Disk Space Using Merkle Tree

A [<span class="underline">Merkle tree</span>](https://nakamoto.com/merkle-trees/) is what you get when you repeatedly hash e.g. SHA-2 pairs of nodes until there is one hash left. If the number of transactions is odd, the last hash will be duplicated before hashing. You can create a hash tree with only 2 elements:

```
from hashlib import sha1

def h(s): return sha1(s.encode()).hexdigest() # hashing helper function

block1 = “Block 1”
block2 = “Block 2”

digest1 = h(block1)
digest2 = h(block2)

root = h(digest1 + digest2)
print(root)
# d1c6d4f28135f428927a1248d71984a937ee543e
```

h(digest1 + digest2) is the root of this hash tree, known as the *Merkle root*, which must be a unique identifier of this exact tree. To check if the client-side Merkle tree is corrupt, you only need to recompute its Merkle root and compare it to the canonical Merkle root.

![](/images/2020-12-31-Bitcoin-Whitepaper/image1.png)
[*<span class="underline">Note that if you modify any element of the tree, even by 1 bit, the avalanche effect would cause the hash upstream to change all the way up to the Merkle root.</span>*](https://nakamoto.com/merkle-trees/)

To pinpoint a faulty block, request the two hashes below the root in the canonical Merkle tree, and figure out which hash doesn’t match up with our client-side tree, repeat until the base is reached. Assuming there’s a single faulty block, this will let you pinpoint that block with only *O*(log*n*) comparisons (where *n* is the number of underlying data blocks).

To save bandwidth, Satoshi proposes only using block headers: instead of broadcasting all transactions in the previous block, only the Merkle root is transmitted. Despite that, the blockchain size was 317 GB at last measure, still a burden for most retail machines to store.

![https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2FVollinian%2FnG3BWtM2wZ.png?alt=media\&token=c45bad57-629d-483e-bdda-0d8186877775](/images/2020-12-31-Bitcoin-Whitepaper/image4.png)
[*<span class="underline">The Bitcoin blockchain.</span>*](https://nakamoto.com/merkle-trees/)

## Simplified Payment Verification

Similarly, to confirm a transaction has been accepted into a block, you only need to download the block header instead of downloading every transaction and every block. A “light client” can download just the chain of block headers: 80-byte chunks of data for each block that contain only five things:

- A hash of the previous header
- A timestamp
- A mining difficulty value
- A proof of work nonce
- A root hash for the Merkle tree containing the transactions for that block.

![](/images/2020-12-31-Bitcoin-Whitepaper/image6.png)
[*<span class="underline">Data structure of blocks in the ledger.</span>*](https://commons.wikimedia.org/wiki/File:Bitcoin_Block_Data.png#/media/File:Bitcoin_Block_Data.png)

For example, to check *Tx0*, you only need to *Hash0*, and request *Hash1* from another client’s block to get *Hash01* by hashing *Hash0* and *Hash1*. You then can then request *Hash23* from the other client’s block, then hash *Hash01* and *Hash23* to get the Merkle root *Tx\_Root*, and compare with the Merkle root in the block header.

This kind of inclusion proof is known as a *Merkle proof*, which also only requires *O*(log*n*) hashes to transmit.

## Combining And Splitting Value

Combining transaction amounts will result in more efficient transfers as opposed to creating a separate transaction for every cent involved. For example, Alice transfers 10BTC to Bob, if Bob wants to transfer 2BTC to Charlie, he can set up a transaction with one input of 10BTC and two outputs of 2BTC to Charlie and 8BTC to Bob himself.

## Privacy

A new key-pair should be used for each new transaction. For example, Alice wants to transfer 2BTC to Bob, she will set up a transaction with input of 10BTC and with two outputs of 2BTC to Bob and 8BTC to Daniel, where Charlie is her new identity so no one can link Daniel to Alice.

In practice, Bitcoin is only really private for those who take great caution to ensure their anonymity. Most Bitcoin is now traded between centralized exchanges that require ID and occasionally bank account verification by law. Also, transactions can be linked to individuals and companies through "idioms of use" (e.g transactions that spend coins from multiple inputs indicate that the inputs may have a common owner) and corroborating public transaction data with known information on owners of certain addresses.

Bitcoin’s speculation-fueled popularity put it in the spotlight of government and central banks long ago. For example, the US Department of Justice [seized](https://www.justice.gov/usao-ndca/pr/united-states-files-civil-action-forfeit-cryptocurrency-valued-over-one-billion-us) $1 billion in Bitcoin from the dark web marketplace Silk Road.

According to the [<span class="underline">Library of Congress</span>](https://www.loc.gov/law/help/cryptocurrency/cryptocurrency-world-survey.pdf), an "absolute ban" on trading or using cryptocurrencies applies in nine countries: Algeria, Bolivia, Egypt, Iraq, Morocco, Nepal, Pakistan, Vietnam, and the United Arab Emirates. An "implicit ban" applies in another 15 countries, which include Bahrain, Bangladesh, China, Colombia, the Dominican Republic, Indonesia, Kuwait, Lesotho, Lithuania, Macau, Oman, Qatar, Saudi Arabia and Taiwan.

## Calculations

Satoshi outlines the math that makes a successful [<span class="underline">attack</span>](https://www.theblockcrypto.com/amp/linked/71272/bitcoin-gold-devs-blockchain-reorg?__twitter_impression=true) on the blockchain extremely unlikely. At the very least, even if someone manages to create a chain rivaling the honest one, they would not be able to create Bitcoin from thin air because honest nodes will not accept an invalid transaction. All they can do is race the honest chain to be the longest and erase their own transactions from the block they create, but again the longer the chain is, an exponentially greater amount of CPU power will be needed to catch up.

In fact, it has gotten too expensive to even try.

![](/images/2020-12-31-Bitcoin-Whitepaper/image8.png)
[*<span class="underline">As of October 2019, hypothetically it would take more than $4B in hardware cost alone to attack Bitcoin’s blockchain.</span>*](https://www.coinbase.com/learn/crypto-basics/what-is-bitcoin)

## References

From [<span class="underline">Gwern</span>](https://www.gwern.net/Bitcoin-is-Worse-is-Better#):

> The interesting thing is that all the pieces were in place for at least 8 years before Satoshi’s publication, which was followed more than half a year later by the first public prototype. If we look at the citations in the whitepaper and others, and then order the relevant technologies by year in descending order:

> 1. 2001: [<span class="underline">SHA-256</span>](https://en.wikipedia.org/wiki/SHA-256) finalized
> 2. 1999–present: [<span class="underline">Byzantine fault tolerance</span>](https://en.wikipedia.org/wiki/Byzantine_fault_tolerance) (PBFT etc.)
> 3. 1999–present: [<span class="underline">P2P networks</span>](https://en.wikipedia.org/wiki/P2P_networks) (excluding early networks like [<span class="underline">Usenet</span>](https://en.wikipedia.org/wiki/Usenet) or [<span class="underline">FidoNet</span>](https://en.wikipedia.org/wiki/FidoNet); [<span class="underline">MojoNation</span>](https://en.wikipedia.org/wiki/MojoNation) & [<span class="underline">BitTorrent</span>](https://en.wikipedia.org/wiki/BitTorrent), [<span class="underline">Napster</span>](https://en.wikipedia.org/wiki/Napster), [<span class="underline">Gnutella</span>](https://en.wikipedia.org/wiki/Gnutella), [<span class="underline">eDonkey</span>](https://en.wikipedia.org/wiki/eDonkey_network), [<span class="underline">Freenet</span>](https://en.wikipedia.org/wiki/Freenet), [<span class="underline">i2p</span>](https://en.wikipedia.org/wiki/i2p) etc.)
> 1. 1998: Wei Dai, [<span class="underline">B-money</span>](http://weidai.com/bmoney.txt)
> 2. 1997: [<span class="underline">HashCash</span>](https://en.wikipedia.org/wiki/HashCash); 1998: Nick Szabo, Bit Gold; ~2000: MojoNation/BitTorrent; ~2001–2003, [<span class="underline">Karma</span>](http://kayapo.tribler.org/trac/raw-attachment/wiki/ExistingReputationSystems/KARMA,%20A%20Secure%20Economic%20Framework%20for%20Peer-to-Peer%20Resource%20Sharing.pdf), etc.
> 3. 1992–1993: Proof-of-work for spam
> 4. 1991: [<span class="underline">cryptographic timestamps</span>](https://en.wikipedia.org/wiki/Trusted_timestamping)
> 5. 1980: [<span class="underline">public key cryptography</span>](https://en.wikipedia.org/wiki/public_key_cryptography)
> 6. 1979: [<span class="underline">Hash tree</span>](https://en.wikipedia.org/wiki/Merkle_tree)

> This lack of novelty is part of the appeal—the fewer new parts of a cryptosystem, the less danger. All that was lacking was a Satoshi to start a Bitcoin.

## More Nice Graphs 

![](/images/2020-12-31-Bitcoin-Whitepaper/image14.png)  
[*<span class="underline">Moore’s law</span>*](https://commons.wikimedia.org/wiki/File:Moore%27s_Law_Transistor_Count_1971-2016.png)

![](/images/2020-12-31-Bitcoin-Whitepaper/image2.png)  
[*<span class="underline">Bitcoin’s academic pedigree.</span>*](https://queue.acm.org/detail.cfm?id=3136559)

![](/images/2020-12-31-Bitcoin-Whitepaper/image15.png)  
[*<span class="underline">Should’ve bought Bitcoin?</span>*](https://www.blockchain.com/charts/market-price?timespan=all&scale=1)

![](/images/2020-12-31-Bitcoin-Whitepaper/image12.png)  
*[<span class="underline">Bitcoin is very volatile.</span>](https://nakamoto.com/bitcoin-becomes-the-flag-of-technology/)*

![](/images/2020-12-31-Bitcoin-Whitepaper/image13.png)  
[*<span class="underline">TIL Hong Kong is an economically volatile region.</span>*](https://blog.coinbase.com/charting-the-course-of-bitcoin-11-years-and-counting-b4e17969d4e1)

![](/images/2020-12-31-Bitcoin-Whitepaper/image11.png)  
[*<span class="underline">2% of accounts control 95% of bitcoin assets.</span>*](https://www.bloomberg.com/news/articles/2020-11-18/bitcoin-whales-ownership-concentration-is-rising-during-rally)

![](/images/2020-12-31-Bitcoin-Whitepaper/image3.png)  
*[<span class="underline">Bitcoin price bubbles in 2011, 2013 and 2017.</span>](https://commons.wikimedia.org/wiki/File:Bitcoin-bubble-chart-history-2017.png#/media/File:Bitcoin-bubble-chart-history-2017.png) Cryptocurrencies have long been criticised as [<span class="underline">speculative bubbles</span>](https://en.wikipedia.org/wiki/Cryptocurrency_bubble).*

## Additional reading

More explainer (can skip):
- [<span class="underline">Fermat’s Library's annotated Bitcoin whitepaper</span>](https://fermatslibrary.com/s/bitcoin)
- [<span class="underline">Wikipedia article on Bitcoin</span>](https://en.wikipedia.org/wiki/Bitcoin#cite_note-RCAWJune2018LOC-209)
- [<span class="underline">Introduction To Cryptocurrency</span>](https://nakamoto.com/introduction-to-cryptocurrency/)
- [<span class="underline">A technical introduction to Bitcoin for non-technical people</span>](https://alexdanco.com/2019/03/18/a-technical-introduction-to-bitcoin-for-non-technical-people/)
- [<span class="underline">When Bitcoin grows up</span>](https://www.lrb.co.uk/v38/n08/john-lanchester/when-bitcoin-grows-up)

Bitcoin/crypto:
- [<span class="underline">Nakamoto.com</span>](https://nakamoto.com/) with contributions from all the big names.
- [<span class="underline">Bitcoin’s Guardian Angel: Inside Coinbase Billionaire Brian Armstrong’s Plan To Make Crypto Safe For All</span>](https://www.forbes.com/sites/michaeldelcastillo/2020/02/19/coinbase-billionaire-brian-armstrongs-plan-to-make-bitcoin-ethereum-xrp-safe-for-all/)
- [<span class="underline">Stripe on Bitcoin</span>](https://stripe.com/gb/blog/bitcoin-the-stripe-perspective)
- [<span class="underline">In Search of the Elusive Bitcoin Billionaire</span>](http://reason.com/archives/2017/11/28/in-search-of-the-elusive-bitco)
- [<span class="underline">This Is What Happens When Bitcoin Miners Take Over Your Town</span>](https://www.politico.com/magazine/story/2018/03/09/bitcoin-mining-energy-prices-smalltown-feature-217230)
- [<span class="underline">Nassim Taleb on Bitcoin</span>](https://medium.com/opacity/bitcoin-1537e616a074)
- [<span class="underline">As Traditional Payments Get Faster, What’s Left for Bitcoin?</span>](https://breakermag.com/as-traditional-payments-get-faster-whats-left-for-bitcoin/)
- [<span class="underline">Why Bitcoin Will Take a Long Time to Dethrone the Dollar</span>](https://www.coindesk.com/why-bitcoin-will-take-a-long-time-to-dethrone-the-dollar)
- [<span class="underline">Sam Altman on Bitcoin (2013)</span>](https://blog.samaltman.com/thoughts-on-bitcoin)
- [<span class="underline">Bitcoin’s Biggest Hack In History: 184.4 Billion Bitcoin from Thin Air</span>](https://hackernoon.com/bitcoins-biggest-hack-in-history-184-4-ded46310d4ef)
- [<span class="underline">Gwern on Bitcoin is worse is better</span>](https://www.gwern.net/Bitcoin-is-Worse-is-Better#)
- [<span class="underline">Coding Bitcoin from Scratch in Rust</span>](https://monokh.com/posts/bitcoin-from-scratch-part-1)
- [<span class="underline">Bitcoin’s most puzzling tradeoffs</span> <span class="underline">explained</span>](https://medium.com/@nic__carter/bitcoin-bites-the-bullet-8005a2a62d29)
- [<span class="underline">What's Really Driving the Cryptocurrency Phenomenon?</span>](https://www.gwern.net/docs/www/iterative.capital/0f2a6e1b25cbf4a115aeae3693e009e98d9de126.html)
- [<span class="underline">Alex Tabarrok on Bitcoin is less secure than most people think</span>](https://marginalrevolution.com/marginalrevolution/2019/01/bitcoin-much-less-secure-people-think.html)
- Vitalik Buterin [<span class="underline">on mining</span>](https://bitcoinmagazine.com/articles/mining-2-1403298609/), [<span class="underline">a philosophy of blockchain validation</span>](https://vitalik.ca/general/2020/08/17/philosophy.html), [<span class="underline">notes on blockchain governance</span>](https://vitalik.ca/general/2017/12/17/voting.html),
- Tyler Cowen on [<span class="underline">Bitcoin will not take over the world</span>](https://www.gwern.net/Silk-Road#), [<span class="underline">Bitcoin volatility is a feature not a bug</span>](https://marginalrevolution.com/marginalrevolution/2017/12/can-bitcoin-good-store-value-price-volatile.html), [<span class="underline">no longer thinks Bitcoin is a bubble</span>](https://marginalrevolution.com/marginalrevolution/2017/11/bitcoin-just-bubble.html), [<span class="underline">Bitcoin is here to stay</span>](https://www.bloomberg.com/opinion/articles/2019-06-28/bitcoin-s-rise-shows-crypto-is-alive-and-well)

Blockchain:
- [<span class="underline">Ten years in, nobody has come up with a use for blockchain</span>](https://hackernoon.com/ten-years-in-nobody-has-come-up-with-a-use-case-for-blockchain-ee98c180100) and its sequel [<span class="underline">Blockchain is not only crappy technology but a bad vision for the future</span>](https://medium.com/@kaistinchcombe/decentralized-and-trustless-crypto-paradise-is-actually-a-medieval-hellhole-c1ca122efdec)
- [<span class="underline">Harvard Business Review on blockchain</span>](https://hbr.org/2017/01/the-truth-about-blockchain)
- [<span class="underline">Blockchain social networks</span>](https://medium.com/decentralized-web/blockchain-social-networks-c941fb337970)
- [<span class="underline">Tyler Cowen on blockchains</span>](https://www.bloomberg.com/opinion/articles/2018-04-27/blockchains-warrant-skepticism-but-keep-an-open-mind?utm_content=crypto&utm_medium=social&utm_campaign=socialflow-organic&utm_source=twitter)
- [<span class="underline">Eight Popular Blockchain Use Cases And Why They Do Not Work</span>](https://blog.smartdec.net/you-do-not-need-blockchain-eight-popular-use-cases-and-why-they-do-not-work-f2ecc6cc2129)
- [<span class="underline">Blockchains and the Opportunity of the Commons</span>](https://marginalrevolution.com/marginalrevolution/2018/06/blockchains-opportunity-commons.html)
