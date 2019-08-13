---
layout: default
permalink: /LearningCrypto01/
title: Intro to Cryptography Lecture 1
tags: Cryptography
---
I'm starting to study cryptography by reading Yevgeniy Dodis' notes at this [link](https://cs.nyu.edu/courses/fall08/G22.3210-001/index.html), and would like to make some interesting notes. 

Today I've read the notes of lecture 1. I want to explain the argument for the necessity of secret, which I spent some time thinking about and had fun playing with.

## **The Scenario of the Problem**

The scenario involves three agents, Alice, Bob and Eve. Bob wants to send a message $m$ to Alice that **only** Alice can read. Therefore Bob would like to encrypt $m$ making it the ciphertext $c$ and send $c$ to Alice. Eve is the third party (adversary) who can see $c$ and wants to know $m$. We name Bob's encryption function as $Enc:$ $Enc(m, ???) \rightarrow c$ and Alice's decryption function as $Dec:$ $Dec(c, ???) \rightarrow m$. The pair $(Enc, Dec)$ constitutes the communication scheme they use.

Initial assumptions we made are:

* The encryption and decryption functions (algorithms) are known by all agents (in particular, Eve).
* Alice must always be able to recover $m$ (deterministially).
* Eve has unbounded computational power.

## **The Necessity of Secret**

Base on the initial assumption, Do Alice and Bob necessarily need secret in order to achieve their private communication? The answer is yes, the following arguments establish the necessity.

1. **Alice must have a secret from Eve.**  
If Alice doesn't have a secret, then Alice should be no different from Eve, while by assumption Eve is even computationally stronger than Alice (Eve has unbounded computationl power). Therefore what Alice can do can also be done by Eve, the communication scheme must fail.

2. **Bob must have a secret from Eve. In fact, Alice and Bob must share a secret $s$ not known to Eve.**  
Since Eve has unbounded computational power, she can iterate (try) all the message $m$ and (possibly) other information $X$ used by Bob to produce $c$, which is the ciphertext sent by Bob. She can claim that the message $m$ she had tried so that $Enc(m, X)\rightarrow c$ is exactly the message sent by Bob. Why?   
The reason is that, if otherwise Bob has sent a different $m^{\prime} \neq m$ and $Enc(m^\prime, X^\prime)=c$, (Here $X^\prime$ is not necessarily different from $X$. In fact X can be viewed as the same thing as $m$ plus $X$ together, so does $X^\prime$. They all represent the information Bob/Eve used to encrypt message) then how can Alice know which of $m$ and $m^\prime$ was sent by Bob? As we discussed above, Alice holds a secret $s$, which is a part of $m$ plus $X$ and enables her to differentiate $(m, X)$ and $(m^\prime, X^\prime)$. Also, Bob must know this secret in order to send his message (express his intention) correctly. On the other hand, Eve cannot distinguish $(m, X)$ and $(m, X^\prime)$ because of the lack of the secret key $s$.

## **Other Summary**
In the lecture 1 notes we can see that the above initial assumptions give negative results. Shannon's theorem says that perfect security against adversary with unbounded computational power needs that the secret $s$ has at least the same length as message communicated, which is not practical. (I think I also saw somewhere that secret sharing is expensive?).  

In real world we may not want to assume Eve has unbounded computational power, because Eve is just a human being like us all! While Eve does have the ability to guess. We can now relax the assumption and assume Eve is in *Probabilistic Polynomial Time (PPT)*. This actually makes a big difference. Let's re-examine the two necessity above.

1. **Alice must have a secret from Eve.**  
Well this should still hold because the same reason as above.

2. **Bob must have a secret from Eve. In fact, Alice and Bob must share a secret $s$ not known to Eve.**  
This may not hold as previous. Why? Because now Eve is bounded in PPT, she is not allowed to do the previous iterative method. For now I think this is intuitive, maybe we can see more formal arguments (proofs) in later notes.

In summary, two things might be improved from the relaxation of assumptions. First, Bob may not need a secret from Eve. Second, the length of secret key may be shorter than message length (overcoming shannon's barrier). 