<!-- TOC START min:1 max:6 link:true update:true -->
- [Week 1](#week-1)
  - [Section 1: What is cryptography about?](#section-1-what-is-cryptography-about)
    - [Course Overview:](#course-overview)
    - [What is Cryptograph?](#what-is-cryptograph)
    - [History of Cryptography](#history-of-cryptography)
  - [Section 2: crash course in discrate probability](#section-2-crash-course-in-discrate-probability)
  - [Stream Ciphers 1: the one-time pad and stream ciphers](#stream-ciphers-1-the-one-time-pad-and-stream-ciphers)
  - [Stream Ciphers 2: attacks and common mistakes](#stream-ciphers-2-attacks-and-common-mistakes)
  - [Stream Ciphers 3: real-world examples](#stream-ciphers-3-real-world-examples)
  - [Stream Ciphers 4: what is a secure cipher?](#stream-ciphers-4-what-is-a-secure-cipher)

<!-- TOC END -->

10-10-2017

<a name="week-1"></a>
# Week 1

<a name="section-1-what-is-cryptography-about"></a>
##Section 1: What is cryptography about?
<a name='course-overview'></a>
###Course Overview:

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

<a name="what-is-cryptograph"></a>
###What is Cryptograph?

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
      - Privately outsourcing computation: Alice can send encrypted query to Google and Google sends encrypted results back to Alice, but Google don't know what is encrypted (**very new technology, just 2-3 years ago said by the instructor; this course was created probably on 2015**).
      - Zero knowledge (proof of knowledge)
        - $N=p \cdot q$, and $p, q$ are very large prime, probably thousand of digits.
        - Alice knows $p, q$.
        - Bob knows $N$, but don't know $p,q$.
        - **Alice can prove to Bob that she knows the factorization, but Bob knows nothing about the factorization and he is convinced that Alice knows the factorization.**
- A rigorous science
  - Precisely specify threat model (e.g. a signature is unforgeable)
  - Propose a construction
  - Prove that breaking construction under threat mode will solve an underlying hard problem

<a name='history-of-cryptography'></a>
###History of Cryptography

- David Kahn, "The code breakers"

- Several ciphers that have been broken before

  - Symmetric Ciphers

    ![img](https://github.com/karlzhang-hhg/karlzhang-hhg.github.io/blob/master/images/CS_courses/Intro_cryptography/Sym_cipher.png?raw=true)

    - Substitution cipher
      - $26!$ space size
      - $26! \approx 2^{88}$
      - Still terribly insecure
      - How to break it:
        - The most common letter in English text is *e* ($12.7\%$)
          - Match *E* to the most frequent letters from the target text
          - Then do the same thing for *t* ($9.1\%$)
          - *a* ($8.1\%$)
        - Then use frequency of pairs of letters (diagrams)
          - *he*, *an*, *in*, *th*
      - Vulnerable to *cipher-text only attack*
    - Caesar Cipher
      - Move letter to constant number of position in the alphbetic table
    - Vigener cipher (16'th century, Rome)
      - *key = CRYPTO*
      - *message = WHATANICEDAYTODAY*
      - Replicate the *key*, and then move 26 and take module
      - How to break it?
        - Assume we know the length of *key*
        - Break the *message* into group with length of *key*
        - Look the first letter in each group. Suppose the most common letter is *e*, and match the most common letter in the first letters in all groups. Then break the first letter in the *key*. Then can do the same thing for the rest of letters.
        - If we don't know the length of *key*, we run this procedure assuming the length of *key*, as 1, 2, 3, ...
        - Cipher-text only attack
    - Rotor Machine (1870-1943)
      - There is a rotor
      - Each time hit a letter, rotor rotates one notch and *key* changed. It was broken by using letter frequency, diagram frequency.
      - The most famous: the Enigma (3-5 rotors). The sercet key is the initial setting of 4 rotors ($2^{18}$ keys).
      - British cryptographer Bletchley Park used CT attack to break it.
    - Data Encryption Standard (1974)
      - DES: #keys = $2^{56}$, block size = 64 bits. Not insecure anymore. Still used in some lagacy system.
      - Today: AES (2001), Salsa20 (2008)

<a name='section-2-crash-course-in-discrate-probability'></a>
##Section 2: crash course in discrate probability

- Deterministic algorithm: same input, same output

- Randomized algorithm: same input, randomized output

- **Thm: Y is a rand. var. over $\{0,1\}^n$, X is an indep. uniform var. on $\{0,1\}^n$. Then $Z:=Y \bigoplus X$ ($\bigoplus$ is XOR) is uniform var. on $\{0,1\}^n$.**

- The birthday paradox: Let $r_1, \dots, r_n \in U$ be iid rand. vars.

  **Thm: when $n=1.2 \times |U|^{1/2}$, then $Pr[\exists i\neq j : r_i = r_j] \geq 1/2$**

  Example1: Let $U=\{0,1\}^{128}$. After sampling about $2^{64]}$ random messages from $U$, some two sampled messages will likely be the same.

  Example2: It is likely that when $1.2\times \sqrt{365}\approx 24$ people are in a room, two of them has the same birthday. However, birthday is not uniformly distributed among 365 days and biased towards September. I think this would lower the number of people we need to get two people having the same birthday.

  ![img](https://github.com/karlzhang-hhg/karlzhang-hhg.github.io/blob/master/images/CS_courses/Intro_cryptography/Colli_prob.png?raw=true)

  ​
<a name="stream-ciphers-1-the-one-time-pad-and-stream-ciphers"></a>
##Stream Ciphers 1: the one-time pad and stream ciphers

- Information Theoretic Security and The One Time Pad

  - __Def__: a **cipher** defined over $(\mathcal{K}, \mathcal{M}, \mathcal{C})$ (where $\mathcal{K}$ is the set of *all possible keys*, $\mathcal{M}$ the set of *all possible messages*, and $\mathcal{C}$ the set of *all possible cipher-text*) is a pair of "efficient" algs $(\mathbf{E}, \mathbf{D})$ (where $\mathbf{E}$ is the encrypting all, $\mathbf{E}:\mathcal{K}\times \mathcal{M} \rightarrow \mathcal{C}$, and $\mathbf{D}$ the decrypting alg, $\mathbf{D}:\mathcal{K}\times \mathcal{C} \rightarrow \mathcal{M}$), s.t. (correctness property) $\forall m \in \mathcal{M}, k \in \mathcal{K}: \mathbf{D}(k,\mathbf{E}(k,m))=m$ (consistency equation).

    - Efficiency has different meanings: in theoretical, running in polynomial time; in practical, concrete time constrains.
    - **$\mathbf{E}$ is often randomized**: generates random bits used to encrypt messages
    - **$\mathbf{D}$ is always randomized**

  - The One Time Pad (Vernam 1917)

    - 1st example of a "secure" cipher

      - $\mathcal{M}=\mathcal{C}=\{0,1\}^n$

      - $\mathcal{K}=\{0,1\}^n$

      - Key=rand. bit string as long as meg

      - $c:=\mathbf{E}(k,m)=k\bigoplus m$

      - $\mathbf{D}(k,c)=k\bigoplus c$

      - Indeed (note there is a exchange and associative rule for $\bigoplus$):

        $$\begin{aligned}&\mathbf{D}(k,\mathbf{E}(k,m)) =\mathbf{D}(k,k\bigoplus m)=k\bigoplus (k \bigoplus m)\\=&(k\bigoplus k)\bigoplus m = \mathbf{0} \bigoplus m = m\end{aligned}$$

    - **Very fast encoding/decoding!! … but long keys (as long as plaintext)**: if you have way to secertly send secret key as long as the message, we may just send the message without sending the key, from the first place.

    - But idea behind is very useful.

    - Why OTP a good cipher?

    - Information Theoretic Security (Sannon 1949)

      - Basic idea: CT (cipher-text) should reveal no "info" about PT (plain-text)

      - __Def__: A cipher $(\mathbf{E},\mathbf{D})$ over  $(\mathcal{K}, \mathcal{M}, \mathcal{C})$ has __perfect secrecy__ if $\forall m_0, m_1 \in \mathcal{M}$ $(|m_0|=|m_1|)$ and $\forall c\in \mathcal{C}$, s.t.

        $Pr[\mathbf{E}(k,m_0)=c]=Pr[\mathbf{E}(k,m_1)=c]$

        where $k$ is uniform in $\mathcal{K}$ where $k\xleftarrow{R}  \mathcal{K}$

      - In other words, given CT, one cannot tell if msg is $m_0$ or $m_1$, for all $m_0$ and $m_1$.

      - The most powerful adversary learns nothing about PT from CT.

      - Not CT only attack!! (but other attacks may be possible).

      - __Lemma__: OTP (One Time Pad) has perfect secrecy.

        __Proof__: $\forall m,c:Pr[\mathbf{E}(k,m)=c] = \frac{|\{k\in \mathcal{K}: \mathbf{E}(k,m)=c\}|}{|\mathcal{K}|}$.

        so, "$\forall m,c: |\{k\in \mathcal{K}: \mathbf{E}(k,m)=c\}|=const$" $\implies$ "cipher has perfect secrecy".

        Actually, the $const=1$. For OTP, $\mathbf{E}(k,m)=c$ $\Rightarrow$ $k=m\bigoplus c$ $\Rightarrow$ $k=m\bigoplus c$ $\Rightarrow$ $|\{k\in \mathcal{K}: \mathbf{E}(k,m)=c\}|=1, \forall m,c$ $\Rightarrow$ OTP has perfect secercy. $\Rightarrow$ OTP has no CT only attack! $\blacksquare$

      - The bad news:

        __Thm__: perfect secrecy $\Rightarrow$ $|\mathcal{K}|\geq |\mathcal{M}|$.

        This theorm means OTP is the optimal keys for perfect secrecy, but in practical it is very hard to use.

- Steam Ciphers and Pseudo Random Generators

  - Stream Ciphers: making OTP practical

    - Idea: replace "random" key by "pseudorandom" key

    - Pseudo Random Generator (PRG): a function, $G:\{0,1\}^s \rightarrow \{0,1\}^n$ (seed space $\rightarrow$ random variable space), where $n \gg s$, and $\{0,1\}^s$ is the seed space.

    - "Efficient" computable by deterministic algorithm. $G$ is a deterministic function.

    - The output should look random.

    - The procedure:

      - Expand the pseudo random key, $k$, into much larger key, $G(k)$ (pseudoranom key).
      - XOR the $G(k)$ with the message.
      - $c=\mathbf{E}(k,m):=m\bigoplus G(k)$
      - $\mathbf{D}(k,c):=c\bigoplus G(k)$
      - Not perfect secrecy.

    - Need a different definition of security.

    - Security will depend on specific PRG.

    - PRG must be unpredictable.

      - Suppose PRG is predictable.

        $\exists i: G(k)|_{1,\dots,i} \xrightarrow{alg.} G(k)|_{i+1,\dots,n}$

      - Even $G(k)|_{1,\dots,i} \xrightarrow{alg.} G(k)|_{i+1}$, it is already a problem

      - Use the prefix of message, we can get the first $i$ letters of crypto-text, $G(k)|_{1,\dots,i}$, which can be used to predict the rest of crypto-text (small prefix can give away the entire messages).

      - __Def__: $G:\mathcal{K}\rightarrow \{0,1\}^n$ is said predictable if there exists an "efficient" alg. $\mathcal{A}$ and $\exists 1 \leq i \leq n-1$, s.t.

        $Pr[\mathcal{A}(G(k)|_{1,\dots,i})=G(k)|_{i+1}]\geq 1/2+\epsilon$,

        where $k\xleftarrow{R}\mathcal{K}$, for some non-negliable $\epsilon$ ($\epsilon \geq 1/2^{30}$)

      - __Def__: PRG is **unpredictable** if it is not predictable $\implies$ $\forall i$: no "efficient" adversary alg. can predict bit ($i+1$) for "non-negliable" $\epsilon$.

      - Weak PRGs (**do not use for crypto; easy to predict!!!**)
        - Linear congressional generator with parameters $a,b$ as intergers and $p$ as a prime.
          - Step1: $r[0]=seed$
          - Step2: $r[i] \leftarrow (a\times r[i-1] + b) \% p$
          - Step3: Output few bits of $r[i]$
          - Step4: $i++$ and go to Step1
        - glibc random():
          - $r[i] \leftarrow (r[i-3]+r[i-31])\% 2^{32}$
          - output $r[i] \gg 1$
          - **Never ever use glibc random() for crypto**, because it is very easy to predict and doesn't provide cryptographical randomness
  - Negligible and non-negligible
    - In practice: $\epsilon$ is a scalar and
      - $\epsilon$ non-neg: $\epsilon \geq 1/2^{30}$ (likely to happen over 1GB of data)
      - $\epsilon$ negligible: $\epsilon \leq 1/2^{80}$ (won't happen over life of key)
    - In theory: $\epsilon$ is a function $\epsilon: Z^{\geq 0}\rightarrow R^{\geq 0}$ and
      - $\epsilon$ non-neg: $\exists d: \epsilon(\lambda) \geq 1/\lambda^d$ infinitely often ($\epsilon \geq 1/poly(\lambda)$, for many $\lambda$)
      - $\epsilon$ negligible: $\forall d, \lambda \geq \lambda_d: \epsilon(\lambda) \leq 1/\lambda^d$ ($\epsilon \leq 1/poly(\lambda)$, for large $\lambda$)
    - Examples:
      - $\epsilon(\lambda)$: negligible
      - $\epsilon(\lambda)$: non-negligible
      - $\begin{align} \epsilon(\lambda)= \left\{ \begin{matrix} 1/2^{\lambda} & for~odd ~\lambda \\ 1/\lambda^{1000} & for~even~\lambda\end{matrix} \right. \end{align}$: non-negligible

<a name="stream-ciphers-2-atttacks-and-common-mistakes"></a>
##Stream Ciphers 2: attacks and common mistakes
- Review:
  - OTP: $\mathbf{E}(k,m)=m \bigoplus k$, $\mathbf{D}(k,c) = c \bigoplus k$
  - Making OTP practical using a PRG: $G:K\rightarrow \{0,1\}^n$
    - Stream cipher: $\mathbf{E}(k,m)=m \bigoplus G(k)$, $\mathbf{D}(k,c) = c \bigoplus G(k)$
    - Security: PRG must be unpredictable (better def in two segments)
- Attack 1: **two time** pad is insecure !!
  - Never use stream cipher key more than once!!
  $\begin{align} C_1 & \leftarrow m_1 \bigoplus PRG(k)\\ C_2 & \leftarrow m_2 \bigoplus PRG(k) \\
   \end{align}$
  - Eavesdropper does:
  $C_1  \bigoplus C_2 \rightarrow m_1 \bigoplus m_2$
  - Enough redundancy in English and ASCII encoding that:
  $m_1 \bigoplus m_2 \rightarrow m_1, m_2$
  - Real world examples:
    - Project Venona (1941-1946): Russian used dice to produce pad, and use one pad in multiple messages and got decrypted by the US
    - MS-PPTP (windows NT):
      - Client and server both share a secret key $k$
      - Client's all messages are concatenated and encrypted
      - Server decrypted the cipher using the same OTP
      - **Need different keys for $C\rightarrow S$ and $S\rightarrow C$**
      - $k = (k_{S\rightarrow C},k_{C\rightarrow S})$, both client and server know the pair of keys
    - 802.11b WEP:
      - Client and access point both share a secret key $k$
      - PRG(IV || $k$)
      - Length of IV: 24 bits
        - Repeated IV after $2^{24}\approx 16M$ frames
        - One some 802.11 cards: IV resets to $0$ after power cycle
      - For PRG in WEP (RC4), there was an attack (FMS 2001): after $10^6$ frames, key can be recovered
      - After 2001 attacks, $40000$ frames are sufficient
    - Disk encryption: relieve the information about where does change happen
  - Two time pad: summary
    - Never use stream cipher key more than once!!!
    - Network traffic: negotiate new key for every session (e.g. TLS)
    - Disk encryption: typically do not use a stream cipher
- Attack 2: no integrity (OTP is malleable)
  - $m \xrightarrow{enc(\bigoplus k)} m \bigoplus k$
  - Cipher attacks: $(m \bigoplus k) \bigoplus p \xrightarrow{dec(\bigoplus k)}(m \bigoplus p)$
  - Modification to ciphertext are undetected and have predictable impact on plaintext
  - Suppose there is a encrypted message from Bob, but some attack, the message looks like coming from Eve after decryption.  

<a name='stream-ciphers-3-real-world-examples'></a>
## Stream Ciphers 3: real-world examples
- Old example (software): RC4 (1987)
  - 128 bits seed -> 2048 bits -> iteration loop (1 byte per round)
  - Used in HTTPS and WEP
  - Weaknesses:
    - Bias in initial output: $Pr[n^{nd}~byte=0]=2/256$
    - Actually in practice in using RC4, we should ignore the first $256$ bit
    - Prob. of (0,0) is $1/256^2+1/256^3$
    - Related key attacks
- Old example (hardware): CSS (content scrambling system) (badly broken)
  - Linear feedback shift register (LFSR): seed is the initial state of LFSR
  ![img](https://github.com/karlzhang-hhg/karlzhang-hhg.github.io/blob/master/images/CS_courses/Intro_cryptography/LFSR_CSS.png?raw=true)
  - All broken:
    - DVD encryption (CSS): 2 LFSRs
    - GSM encryption (A5/1,2): 3 LFSRs
    - Bluetooth (E0): 4 LFSRs
  - CSS: seed(key) = 5 bytes = 40 bits
  ![img](https://github.com/karlzhang-hhg/karlzhang-hhg.github.io/blob/master/images/CS_courses/Intro_cryptography/LFSR_CSS1.png?raw=true)
- Modern stream ciphers: eStream(2008, qualify 5 stream cipher, but here only one will be talked about)
  - PRG: $\{0,1\}^s \times R \rightarrow \{0,1\}^n$
  - $n \gg s$
  - $\{0,1\}^s$: seed
  - $R$: nonce (a non-repeating value for a given key)
  - $\mathbf{E}(k,m;r)=m\bigoplus PRG(k;r)$
  - The pair $(k,r)$ is never used more than once $\implies$ re-use the key because $(k,r)$ unique
  - Example: eStream (Salsa 20) (SW+HW)
    - Designed both for software and hardware
    - $\{0,1\}^{128~or~256} \times \{0,1\}^{64} \rightarrow \{0,1\}^n$ (max $n=2^{73}$ bits)
    - $Salsa20(k;r):=H(k,(r,0))||H(k,(r,1))||\dots$
    ![img](https://github.com/karlzhang-hhg/karlzhang-hhg.github.io/blob/master/images/CS_courses/Intro_cryptography/Salsa_20.png?raw=true)
    - Performance:
      - Crypto++ 5.6.0 [Wei Dai]
      - On AMD Opteron, 2.2 GHz (Linux)
      - RC4: 126 MB/sec
      - Salsa20/12: 643 MB/sec
      - Sosemanuk: 727 MB/sec

<a name='stream-ciphers-4-what-is-a-secure-cipher'></a>
##Stream Ciphers 4: what is a secure cipher?












  ​

  ​

  ​
