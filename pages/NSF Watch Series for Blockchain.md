[TOC]

# NSF Watch Series for Blockchain

## NSF 44th Watch Series: The Jekyll and Hyde of Smart Contracts

This talk basically introduces one program called 'Town Criers' to bridge the smart contract and authentic informaciton source. In the background, the professor talked about history of blockchain and mechanism of Ethereum.

In the beginning



http://www.tvworldwide.com/events/nsf/170420/globe_show/default_go_archive.cfm?gsid=3069&type=flv&test=0&live=0

Smart contracts are autonomous programs that run on and inherit the properties of blockchains. They may be viewed as emulating trusted third parties, in that they enforce fair play between parties without preexisting trust relationships. This capability promises to transform industries as diverse as supply chain management, finance, insurance, and digital rights management. Smart contracts promise comes with technical and social challenges, however. In this talk, I'll outline the Five Grand Challenges identified by the Initiative for CryptoCurrencies and Contracts (IC3) as critical to blockchain deployment, and focus on two of them. I'll explore the nascent risk of criminal smart contracts, which are smart contracts that solicit or offer the perpetration of a crime. I'll also explore the challenge of delivering strongly authenticated data to smart contracts. I'll introduce the soon-to-be-launched Town Crier authenticated-data or "oracle" service, and describe some applications that it will enable in existing smart contract systems in the near future.

**Bio**

![img](http://www.tvworldwide.com/events/nsf/170420/images/Juels_Ari_cropped_340_272.jpg)Ari Juels is a Professor of Computer Science at the Jacobs Institute at Cornell Tech in New York City, which he joined in 2014. He is also Co-Director of the Initiative for CryptoCurrencies and Contracts (IC3). He was previously Chief Scientist at RSA, and received his PhD at UC Berkeley in 1996. For more information, visit [http://www.arijuels.com](http://www.arijuels.com/)

- Smart contract is applicaion on a blockchain.

  - What is Blockchain?
    - Fostering trust?
    - Mistrust?
    - Anarchist's battle cry?
    - New tool for mainstream FinTech? (Almost every bank has some polit blockchain running; 40 banks)

- Blockchains: Abstraction

  ![img](https://github.com/karlzhang-hhg/karlzhang-hhg.github.io/blob/master/images/blockchain/Blockchain_abstraction.png?raw=true)

  - Information in chuncks on 'bulletin board'
  - Linear structure and Fully orderred
  - Cannot be erased and modified once on blockchain
  - Who can write to blockchain?
    - Decentralized blockchain: anyone
  - Who can read blockchain?
    - Anyone

- How to transfer money on blockchain?

  - Alice write a statement on to blockchain (Alice shown in blockchain as a probulic key) that she sent 2 BTC to Bob.

- **What Bitcoin can offers uniquely?**

  - Anonymous (pseudonymous) transactions
  - Unstoppable payments
    - Irrevocable
    - No interference by authorities
  - Low transaction fees + no middlemen
  - Key-based bearer instrument (High portability; only need secret key)
  - Decentralized (cross-border remittance)

- Excellent for crime (anonymous and unstoppable)

  - Ransomware
  - **Hypothesis: Decentralized smart contract will amp this all up**

- What's a (decentralized) smart contract?

  - Executable object on blockchain
  - Scripted in Turing-complete language
  - Code can define arbitrarily rich functionalities
    - Szabo (1997)
  - Decentralized autonomously (unstoppable quality)

- **Abstraction: Smart contract = virtual trusted third-party with public state**

  ![img](https://github.com/karlzhang-hhg/karlzhang-hhg.github.io/blob/master/images/blockchain/Smart_contract.png?raw=true)

  - Need to information of real life input

  - Exmaple: Simple smart contract: lottery

    ![img](https://github.com/karlzhang-hhg/karlzhang-hhg.github.io/blob/master/images/blockchain/Lottery_smart_contract_code.png?raw=true)

  - Criminal Smart contract (CSC) solve two major (criminal) business problems

    - Dangerous trust model / reliance on reputation

      - DarkMarket.ws: Site admin Master Splyntr=FBI agent K. Mularski
      - Ross Ulbricht (DPR, Silk Road) solicited six murders for hire

    - Law enforcement can shut you down

    - CSCs solve both problems above by enforcing trust

      - Main mechanisms: anonymity and autonomous execution

      - Commission fairness

      - Example: Assassination contract

        - $1 million for assassination

        - How to verify assassination happened?

          Authenticated information feed / oracle

        - How to verify that perportrator is responsible?

          Calling card (exotic object left by a criminal at scene of crime) (hard to guess in advance; reportable by media)

        - How does perportrator, ***P***, use a calling card?

          ![img](https://github.com/karlzhang-hhg/karlzhang-hhg.github.io/blob/master/images/blockchain/Crime_smart_contract.png?raw=true)

          - ***P*** sends to contract enryption (commitment) **e.cc** to calling card **cc** before crime occurs.
          - After crime occus, ***P*** opens **e.cc**, revealing **cc**
          - Contract verifies that **cc** matches authenticated data feed (the **cc** matches details of the crime)
          - Then **cc** proves ***P*** committed crime!

  - CSC that we should worry about:

    - Arson, assault
    - Cybercirmes: leakage of data, theft of CA keys, website defacement
    - Vote buying
    - **Creators can walk away once they create it**

  - Defenses are hard problem.

- Town Crier

  - Bcakground

    - Smart contracts are data-hungry
    - Blockchain can't browse the internet (smart contracts can't query websites)
    - Data must be injected from user account
    - Trust small party
    - No existing oracle

  - Basic idea:

    - Town crier bridges the real world information (say flightware website) with the smart contract (the flight insurance) 

    - Why people trust Town crier? (we need authenticity property)

      SGX (software guarded extension, Intel)

    - SGX: allow you to run programs in protected environment (Enclave)

      - Integrity: Other processes, even OS, cannot tamper with control flow of X
      - Confidentiality: Other processes, even OS, learn nother about state of X
      - Remote attestation: 

    - Town crier goal / adversarial model

      - Relying contract sends query to TC
      - Goal: TC authenticity property for answer A to query Q
      - Assumption: TC code trustworthy (publicly verified)
      - Adversary controls TC node OS and the network

  - Interesting tripartite trust model

    - For example: Smart contract doesn't have confidentiality and very expensive to compute. TC enclave have confidentiality and cheap to compute but there is no network stack. **Harmonizing three trusted entities with different properties is a very interesting problem.**

  - Confidentiality problem: ![img](https://github.com/karlzhang-hhg/karlzhang-hhg.github.io/blob/master/images/blockchain/Town_crier.png?raw=true)

  - Applications: All manner of financial instruments; insurance; supply-chain management

  - **Fair marketplaces for bug-bounties**

  - **Town Crier Public Ethereum Launch: 15 May 2017**

- Q&A:

  - Zcash achieves fully anonymity
  - High entropy calling card and requires deposit (random guss is deterred)

##NSF 38th WATCH: Cyptocurrencies: the ideas behind the hype

http://www.tvworldwide.com/events/nsf/160721/default.cfm?action=2

Cryptocurrencies such as Bitcoin and Ethereum have been polarizing. Supporters claim that they will fundamentally alter payments, economics, and even politics around the world. Skeptics claim that they are inherently broken and will suffer an inevitable and spectacular collapse. In this talk I will present the key technical ideas behind the new generation of cryptocurrencies --- ideas that are novel, deep, and interesting, and span many subfields of computer science, including security, cryptography, distributed systems, game theory, and programming languages. Yet much remains unknown, and I will lay out the key research challenges.

**Bio**:

![img](http://www.tvworldwide.com/events/nsf/160721/images/Arvind_Narayanan.jpg)Arvind Narayanan is an Assistant Professor of Computer Science at Princeton. He leads a research team investigating the security, anonymity, and stability of cryptocurrencies as well as novel applications of block chains. He co-created an online course and textbook on Bitcoin and cryptocurrency technologies. He also leads the Princeton Web Transparency and Accountability Project to uncover how companies collect and use our personal information. His doctoral research showed the fundamental limits of anonymization, for which he received the Privacy Enhancing.



- Introduction:

  - Wall street journal saying: Why blockchains could transform how the economy works.

  - Blockchain is just a data structure. There was a fever pitch to the hype.

  - Modern academic world thinks blockchain skeptical.

  - Paper: Research Perspectives and Challenges for Bitcoin and Cryptocurrencies.

    ![img](https://github.com/karlzhang-hhg/karlzhang-hhg.github.io/blob/master/images/blockchain/Research_Blockchain.png?raw=true)

  - Three things about this talk:

    - The ideas are sound, have a rich history (trace back to CS 80's and 90's); yet novel
    - Cryptocurrencies face several crucial challenges
    - If these can be solved, big opportunities beyond payments

- The ideas:

  - Key idea 1: public keys as identities

    - Bitcoin is a peer-to-peer system; public ledger; paying as **broadcast the transaction**
    - Public keys are the only identities
      - To "speak for" *pk*, must use *sk*
      - Message *msg* signed by *sk* will be "*pk* says <message>"
      - New identities (addresses) at any time
      - No central point of coordination
      - Straight out of Chaum: *Security without identification*
      - Chaum also had *Blinding on signature*

  - Key idea 2: immutable ledger

    - What are put into ledger cannot be changed, neither do order
    - You don't need to remember the whole history of blockchain. You only need to remember the final Hash pointer
    - Jul 2016, the bitcoin has 77 GB data (the final hash pointer is just a few bits)
    - Optimization: Merkle trees (1979)
    - Goes to paper from Haber and Stornetta, 1991

  - Key idea 3: "One CPU one vote"-Proof of Work

    - Byzantine Fault Tolerance: not applied to the open internet (*Sybil attack*)

    - *Pricing via processing or combatting junk mail*

    - *Hashcash-a denial of service counter-measure*

    - There is a possibility of forking, but the probability of forking decreasing exponentially with the length of forks.

    - Evolution of mining: CPU->GPU->FPGA->ASIC

    - Nakamoto consensus: Proof of work, ledger, currency; all three components are necessary

      Nakamoto's genuine idea is connecting PoW to Ledger and to currency (Previous, people tried to connect PoW directly to Currency) ![img](https://github.com/karlzhang-hhg/karlzhang-hhg.github.io/blob/master/images/blockchain/Nakamoto_triangle.png?raw=tru)

  - New idea: scripts

    Ethereum![img](https://github.com/karlzhang-hhg/karlzhang-hhg.github.io/blob/master/images/blockchain/Ethereum_code.png?raw=true)

- Challenges:

  - Security:

    - Cryptocurrencies: an unmitigated security diaster

      ![img](https://github.com/karlzhang-hhg/karlzhang-hhg.github.io/blob/master/images/blockchain/Bitcoin_heist.png?raw=tru)

    - Idea: avoid single points of failure using threshold cryptography

    - Human-crypto interaction is an unsolved problem

    - Smart contracts: new insecurity

    - *Step by step towards creating a safe smart contract: lessons and insgihts from a cryptocurrency lab*

    - *Making smart contract smarter*

  - Incentives:

    - Stability / security of mining: two views:
      - Distributed systems view:
        - Some player are honest, some are not.
        - Player maximizes the rewards
    - Red balloons; Selfish mining; Miner's dilemma; Verifier's dilemma
    - Namecoin: a decentralized blockchain-based alternative (domain) name system
    - The price of anarchy
    - Mechanism design expertise is desperately needed

  - Privacy vs. regulation:

- Opportunities:

  - Algorithmic agent:
    - Agent's actions algorithmically specified, fixed
    - Decentralized: no mone controls it
    - Acts like a trusted third party
    - Markets without a marketpalce
    - Auctions without an auctioneer
  - Create your own markets:
    - Guaranteed Ponzi scheme
    - Prediction markt
    - Financial derivatives
  - Blockchain for internet security infrastructure:
    - Certificate transparency
    - Key transparency
    - Binary transparency
    - BGP security (replace RPKI)