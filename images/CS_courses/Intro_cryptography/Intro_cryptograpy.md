[TOC]

# Section 1: What is cryptography about?

## Course Overview:

- Secure communictaion
  - Example
    - web traffic: HTTPS
    - wireless traffic: 802.11i WPA2, GSM, Bluetooth
  - HTTP, SSL/TLS: no eavesdropping, no tamper
  - Secure Sockets Layer/TLS: 
    - Handshake Protocal: shared secret key using public-key crypto
    - Record Layer: Transmit data using shared secret key
- Encrypting files on disk: EFS, TrueCrypt
  - Store and encrypto files on disks is same as sending info from today to tomorrow
  - Building block: symmetric encryption
    - cipher
    - plaintext, ciphertext
    - secret key (only thing to keep secret)
    - Encryption algorithm is **publicly known**
      - **Never use a proprietary cipher**
  - Single use key (one time key): encrypted email
  - Multi use key (many time key): encrypted files; need more machinery to be safe
- Content protection (e.g. DVD, Blu-ray): CSS, AACS
- User authentication
- Things to remember
  - A tremendous tool
  - Basis for many security mechanisms
  - Not sol to all security prob (software bugs; social eng. attack)
  - Not reliable unless properly used
  - Don't invent yourself; many examples of broken ad-hoc designs

## What is Cryptograph?

- Crypto core:
  - *sk* establishment
  - Secure communication
  - Digital signatures (make signature as a function of the content one signed)
  - Anonymous communication
    - Anonymous digital cash
      - How to be anonymous
      - How to prevent double spending
      - Sol: If Alice spends one digital cash once, the transaction would be anonymous; but if she spends it twice, her idendity would be completely exposed
  - Protocols
    - Elections: 
      - Goal: only calculate majority of votes, but not revealed anything else (individual votes)
      - Votes are sent to an election center with encryption; the election center validate the votes; the election center output majority votes
    - Private auctions:
      - Victory auction: second-highest bid payment
      - Compute the second-highest bid and the winner, but reveal nothing else
      - Similar, there is an auction center, like election center
    - Secure multi-party computation:
      - Goal: compute $f(x_1, x_2, x_3, x_4, \dots)$
      - Nothing else is revealed
      - We could use a trusted authority
      - **Thm.: Anything that can be done with trusted auth. can also be done without it.**
      - Individuals just talk to each other, and finally results are revealed. No trusted authority.
    - Crypto magic:
      - Privately outsourcing computation: Alice can send encrypted query to Google and Google sends encrypted results back to Alice, but Google don't know what is encrypted (**very new technology, just 2-3 years ago**).