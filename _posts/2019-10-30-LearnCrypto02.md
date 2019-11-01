---
layout: default
permalink: /CryptoLec02/
title: Intro to Cryptography 02:One Way Functions
tags: Cryptography
---

In this note we mainly discuss common cryptographic primitives: one-way functions (OWF), one-way permutations (OWP) and trapdoor functions (TDP).

## 1.One-Way Functions

Intuitively, a one-way function is a function that is easy to compute but difficulty to invert. Formally,

**Definition 1.1 (OWF)** A function $$f: \{0,1\}^* \rightarrow \{0,1\}^*$$ is one-way if  

1. For any $x$ that is in the domain of $f$, $f(x)=y$ can be computed in polynomial time.  
2. For any PPT algorithm $A$ and all suffciently large $n$ ($n>N_c$ for some $N_c$),  
$$\Pr[f(z) = y \mid x \leftarrow \{0,1\}^n,\ f(x) = y,\ z\leftarrow A(y, 1^n)\ ]\leq negl(n)$$  
where $negl(n)$ is the negligible function.

**Definition 1.2 (negligible function)** A function $negl(\cdot)$ is negligible if $\forall$ $c>0$ $\exists$ $N_c$ such that $\forall$ $n>N_c$, $negl(n)<\frac{1}{n^c}$.  

**Discussion.** We note that requiring the unary number $1^n$ as adversary's input is necessary. Consider the function $$f(x) = \lvert x\rvert$$. The adversary's input has length $log(\lvert x \rvert)$, while the output length is exponential in that. There function should be one-way because the adversary doesn't have enough time to write down the answer. But it is intuitively easy to invert. 

**Discussion.** The function that satisfies the above definition is called a **uniformly strong one-way** function. We will talk about weak one-way function later. It is *uniform* because we assume the adversary is a uniform algorithm that can take any input length. If in the second requirement above, we allow the adversary to use different algorithms for different lengths (i.e. it is a non-uniform circuits family), then we say the function is **non-uniform strong one-way**.   

We now introduce weak one-way functions. A weak one-way function is a function that is hard to invert with noticeable probability.

**Definition 1.3 (weak OWF)** A function is called (uniformly) weak one-way if  

1. For any $x$ that is in the domain of $f$, $f(x)=y$ can be computed in polynomial time.  
2. $\exists\ c$ such that for any PPT algorithm $A$ and all suffciently large $n$ ($n>N_c$ for some $N_c$) 
$$\Pr[f(z) = y \mid x \leftarrow \{0,1\}^n,\ f(x) = y,\ z\leftarrow A(y, 1^n)\ ]> \frac{1}{n^c}$$  
where $negl(n)$ is the negligible function.

However, there is a theorem due to Yao says that any weak one-way function can be transformed into a strong one-way function.  

**Theorem 1.4 (Yao)** There exists a weak one-way function iff there is a strong one-way function.  

**Proof** will complete later

## 2. Necessary Complexity Assumptions

We state necessary complexity assumptions for the existence of one-way functions.  

First of all, we should observe that  
 
**Theorem 2.1** If $P=NP$, then one-way functions don't exist.  

**Proof.** If $P=NP$, then the adversary can non-deterministically guess all values of $x$ and evaluate f(x).