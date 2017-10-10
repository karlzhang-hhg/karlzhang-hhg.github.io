2017-10-10T05:48:09.582-05:00

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Watch series about distributed system:](#watch-series-about-distributed-system)
	- [Address: https://www.youtube.com/watch?v=7VbL89mKK3M&list=PLOE1GTZ5ouRPbpTnrZ3Wqjamfwn_Q5Y9A&index=1](#address-httpswwwyoutubecomwatchv7vbl89mkk3mlistploe1gtz5ourpbptnrz3wqjamfwnq5y9aindex1)
	- [L1: What is a distributed system?](#l1-what-is-a-distributed-system)
	- [L2: Why build a distributed system?](#l2-why-build-a-distributed-system)
	- [L3: How to learn distributed systems?](#l3-how-to-learn-distributed-systems)
	- [L4: What could go wrong?](#l4-what-could-go-wrong)
	- [L5: The many types of fail](#l5-the-many-types-of-fail)
	- [L6: Byzantine Fault Tolerance](#l6-byzantine-fault-tolerance)
	- [L7: SLIs, SLOs, and SLAs](#l7-slis-slos-and-slas)

<!-- /TOC -->

# Watch series about distributed system:

## Address: https://www.youtube.com/watch?v=7VbL89mKK3M&list=PLOE1GTZ5ouRPbpTnrZ3Wqjamfwn_Q5Y9A&index=1

## L1: What is a distributed system?

- Centralized sys: State stored on a single computer: simpler; easier to understand; faster for single user
- Distributed sys: State divided over multiple computers: more robust (tolerate failures); more scalable (more users); more complex
- Important; worth the trouble
- Examples:
  - Domain Name System (DNS): hostname->IP addresses
  - FB & Google
  - Email servers (SMTP)
  - Phone networks
  - A car
- Conclusion: they are everywhere.

## L2: Why build a distributed system?

- Reasons you need to build a distributed system.
  - Legal/privacy/politics
  - Aligning cost incentives
  - Uptime requirements
  - Performance (latency/bandwidth) (New York-China servers)
  - Dependency on cloud
  - Reliability (you can only get limited reliability you can get from a single machine.)
  - Scaling
  - **Always know why before desiging a distributed system**

## L3: How to learn distributed systems?

- Learn by doing!
- Topics in Distributed Systems:
  - How systems fail
  - How to express your goals: SLI (server-level indicators); SLO (server-level objectives); SLA (SLO + concequences)
  - How to combine unreliable components to make a more reliable system
  - How nodes communicate — RPCs (remote procedure calls)
  - How nodes find each other — naming (how to assign names to your machines so that when a machine boot up, other machines can find it and talk to it)
  - How to use time in a distributed world (watches are not necessarily synchronized; when you care about order of events happening on different machines) (virtual clocks)
  - How to get agreement — consensus (stock trading on distributed system) (Paxos; Raft)
  - How to persist data — distributed storage (rotating disks are the most frequent failing parts)
  - How to secure your system
  - How to operate your distributed system — the art of SRE

## L4: What could go wrong?

- Incomplete list of issues:

  ![img](https://github.com/karlzhang-hhg/karlzhang-hhg.github.io/blob/master/images/CS_courses/Distributed_System/Issues_Dist_Sys.png?raw=true)

  - Crashloop
  - Data corruption
  - Server down
  - Query of death
  - Broken dependency
  - DoS attack
  - Cascading failure
  - Heisenbug
  - Customer reported failure
  - Data loss
  - Time travel
  - Owned
  - Natural disaster
  - Cause infrastructure failure
  - Police raid
  - Operator error
  - Runaway automation
  - Certificate expires
  - Fail to pay bills
  - Performance cliffs
  - Vary important User
  - Non-hermetic builds
  - Firewalls
  - Kernel memory leak
  - Isolation failure
  - Hash collision
  - Incorrect algorithm

## L5: The many types of fail

- Divide and conquer:
  - What are useful categories?
- Network failure vs. Node failure
  - Network failure:
    - Protocols provide useful abstraction
    - TCP/IP: a pair of nodes can communicate, or not
    - SSH: guards against corruption, interception, and impersonation (node-to-node secure connection)
    - Loss of connectivity
    - Network not fast enough
    - Backhoe fade
    - Network partition: Why do we care about partitions?
      - Two nodes write to same data item in different subgraphs
      - Shared state diverges
      - Maintain consistency (at the cost of availability)
      - This trade-off is the CAP (consistency, availiability, partition) principle
      - Detecting partitions: magic number floor(N/2)
  - Node failure:
    - Fail stop: Crash, Power outage, Hardware failure, Out of memory/disk full
    - Strategies: Checkpoint state and restart (High latency), Replicate state and fail over (Hot spare, High cost)
    - Byzantine failure
      - Everything that is not fail stop
        - Bit flip in memory or on disk corrupts data
        - Older version of code on one node sends (now) invalid messages
        - Node starts running malicious version of softare
      - Too many failures == solution impossible
      - Hard to write Byzantine tolarent program
      - Goal: turn into fail stop
        - Checksums/ECC
        - Assertions
        - Timeouts

![img](https://github.com/karlzhang-hhg/karlzhang-hhg.github.io/blob/master/images/CS_courses/Distributed_System/Failure_matrix.png?raw=true)

## L6: Byzantine Fault Tolerance

- Byzantine failure

  - Not fail stop
  - Trator nodes send conflicting messages: incorrect result
  - Cause:
    - Flaky nodes
    - Malicious nodes

- Why study Byzantine failure?

  - Extreme fault tolerance:
    - Bitcoin
    - Boeing 777 & 787 flight controls
  - A research area since the 1980's

- Different assumptions:

  - Can all nodes see all message? Some? None?
  - Do nodes fail? How about the network?
  - Finite computation?
  - Static or dynamic adversary?
  - Bounded communication time?
  - Fully connected network?
  - Randomized algorithms?
  - Quantum or binary computers?

- The two generals problem:

  - Deals with network failure

  - A consensus problem

  - Two nodes have to agree

  - General A,B,C. C is larger than A or B, but if A or B both attack or both retreat, A and B can succeed or survive, otherwise A and B will lose. A and B can only communicate through carrier through terriotory of C.

    ![img](https://github.com/karlzhang-hhg/karlzhang-hhg.github.io/blob/master/images/CS_courses/Distributed_System/Two_generals.png?raw=true)

    No matter what messages we come up with, and how many messages we exchange, we always have inconsistent state until one last message get through. **There is no perfect solution for two generals problem!**

  - One practical solution: A sends 100 carriers to send messages, if one get through, we attack. Work for most situations.

  - If Byzantine failure happens to network, there is no way we can solve this.

- The Byzantine Generals Problem:

  - Deals with node failure

  - Paper: *The Byzantine Generals Problem, Leslie Lamport*

  - How many byzantine node failure can a system survive?

  - How might you build such a system?

  - Is it worth doing it at all?

  - **Goal: Reach a consensus among all loyal generals**

    - **We care what loyal generals think about those traitor generals said (we don't care what traitor generals said).**

    - Communicate one general's decision to the rest of generals.

    - We don't know who is traitor generals

    - *How many traitors can you have and still solve BGP?*

    - Assume: point-ot-point ('oral') message; no crypto

      ![img](https://github.com/karlzhang-hhg/karlzhang-hhg.github.io/blob/master/images/CS_courses/Distributed_System/BGP.png?raw=true)

      We cannot tell difference of the two cases.

    - **How many traitors can be tolerated?**

      - **Lemma: No solution for 3m+1 generals with >m traitors**

  - Assume:

    - Less than 1/3 of generals are traitors
    - Oral messages
    - No crypto
    - OM(m): solution to BGP for <m traitors
    - Inductive solution

  - BGP solution is a very expensive solution. Not always necessary.

    Runtime:

    ![img](https://github.com/karlzhang-hhg/karlzhang-hhg.github.io/blob/master/images/CS_courses/Distributed_System/BGP_runtime.png?raw=true)

  - Many extensions on this problem.

## L7: SLIs, SLOs, and SLAs
