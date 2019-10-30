---
layout: default
permalink: /CryptoLec01/
title: Intro to Cryptography Lecture 1
tags: Cryptography
---
I'm starting to study cryptography by following Yevgeniy Dodis' notes at this [link](https://cs.nyu.edu/courses/fall08/G22.3210-001/index.html), and would like to make some summary notes. The notes will mostly focus on proofs. I will also use other material as references [1][2][3] in order to make notes about additional details.


## 1. The Basic Scenario in Cryptography

The scenario involves three agents, Alice, Bob and Eve. Alice and Bob want to chat on a channel by sending messages to each other. Moreover, they would like to do this secretly so that only they know the (even partial) contents. In the basic model, Eve is the adversary who can observe whatever texts that are sent on the channel. Therefore Alice and Bob would like to encrypt their messages $m$ into a ciphertext $c$ that (as a goal) only they can decrypt. The goal of Eve is to infer the contents of $m$ based on $c$. WLOG, we assume Bob is the sender and Alice is the receiver. We name Bob's encryption function as $Enc:$ $Enc(m, ???) \rightarrow c$ and Alice's decryption function as $Dec:$ $Dec(c, ???) \rightarrow m$. The pair $(Enc, Dec)$ constitutes the communication scheme they use.

Initial assumptions we made are:

* The encryption and decryption functions (algorithms) are known by all agents (in particular, Eve).
* Alice must always be able to recover $m$ (deterministially).
* Eve has unbounded computational power.

## 2. The Necessity of Secret

Base on the initial assumption, Do Alice and Bob necessarily need secret in order to achieve their private communication? The answer is yes, the following arguments establish the necessity.

1. **Alice must have a secret from Eve.**  
If Alice doesn't have a secret, then Alice should be no different from Eve, while by assumption Eve is even computationally stronger than Alice (Eve has unbounded computationl power). Therefore what Alice can do can also be done by Eve, the communication scheme must fail.

2. **Bob must have a secret from Eve. In fact, Alice and Bob must share a secret $s$ not known to Eve.**  
Suppose Bob doesn't have a secret, since Eve has unbounded computational power, she can iterate (try) all the message $m$ and other information $X$ used by Bob to produce $c$, which is the ciphertext sent by Bob. She can claim that the message $m$ she had tried so that $Enc(m, X)\rightarrow c$ is exactly the message sent by Bob. Why?   
The reason is that, if otherwise there is a different $m^{\prime} \neq m$ such that $Enc(m^\prime, X^\prime)=c$, (Here $X^\prime$ is not necessarily different from $X$, as long as we have $(m, X) \neq (m^\prime, X)$) then how can Alice know which of $m$ and $m^\prime$ was sent by Bob? As we discussed above, Alice holds a secret $s$, which is a part of $m$ plus $X$ and enables her to differentiate $(m, X)$ and $(m^\prime, X^\prime)$. Also, Bob must know this secret in order to send his message (express his intention) correctly. On the other hand, Eve cannot distinguish $(m, X)$ and $(m, X^\prime)$ because of the lack of the secret key $s$.

## 3. Perfect Security

We formally define what we mean by a scheme is secure. Ideally, we want that the event Eve seeing the ciphertext $c$ does not increase her chance to guess the message $m$. We denote $M$ as the random variable of message, $C$ for ciphertext accordingly.    

**Definition 3.1 (Perfect Security)** We say a system is secure if for any message $m$, $c = Enc_s(m)$ where $s$ is chosen uniformly at random. $$\Pr(M=m) = \Pr(M=m\mid C=c)$$

One-Time Pad (OTP) is a perfectly secure system.  

**Definition 3.2 (One-Time Pad)** One-Time Pad is the the system $(Enc, Dec)$ where $Enc$ gets $c$ by XOR a random key $s$ with message $m$ and $Dec$ decrypts by XOR the same key $s$ with $c$:  

$$Enc(m, s) = m\oplus s $$  

$$Dec(c, s) = c\oplus s $$  

**Exercise.** Prove that OTP is perfectly secure.

**Discussion.** **1.** Although OTP is perfectly secure, as its name suggests, the same key mustn't be used twice. Indeed if we XOR $m \oplus s$ and $m^\prime \oplus s$ we get $m \oplus m^\prime$. **2.** In fact the following theorem due to Shannon says that perfect security under our initial assumptions requires that the secret $s$ has at least the same length as message communicated, which is not practical.  

**Theorem 3.1**  (Shannon) For any perfectly secure system where Alice and Bob share a key $s$ from space $S$ assume messages $m$ are from space $M$, we must have $\mid S \mid \geq \mid M\mid$.   

**Proof** 
Fix any ciphertext $c$ and key $s$, since $Dec_s$ is deterministic, $c$  must be decrypted into at most message. Therefore, the number of possible one messages resulted from all $s\in S$, we denote by $A$, should satisfy $A\leq \mid S\mid$. On the other hand, we should have $A = \mid M\mid$. Otherwise for some $m$ $Pr[M=m \mid C=c] = 0$, which contradicts the perfect security.


## 4. More Discussion
In real world we may not want to assume Eve has unbounded computational power, because Eve is just a human being like us all! While Eve does have the ability to guess. We can now relax the assumption and assume Eve is in *Probabilistic Polynomial Time (PPT)*. This actually makes a big difference. Let's re-examine the two necessity above.

1. **Alice must have a secret from Eve.**  
Well this should still hold because the same reason as above.

2. **Bob must have a secret from Eve. In fact, Alice and Bob must share a secret $s$ not known to Eve.**  
This may not hold as previous. Why? Because now Eve is bounded in PPT, she is not allowed to do the previous iterative method. For now I think this is intuitive, maybe we can see more formal arguments (proofs) in later notes.

In summary, two things might be improved from the relaxation of assumptions. First, Bob may not need a secret from Eve. Second, the length of secret key may be shorter than message length (overcoming shannon's barrier). 

## References

[1] Rafail Ostrovsky. Foundation of Cryptography. http://web.cs.ucla.edu/~rafail/PUBLIC/OstrovskyDraftLecNotes2010.pdf  
[2] R. Pass and A. Shelat. A Course in Cryptography. http://www.cs.cornell.edu/courses/cs4830/2010fa/lecnotes.pdf
[3] Shafi Goldwasser, Mihir Bellare. Lecture Notes on Cryptography. https://cseweb.ucsd.edu/~mihir/papers/gb.pdf