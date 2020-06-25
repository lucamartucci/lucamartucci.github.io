---
layout: default
permalink: /owfowptdp/
title: Part 2: One Way Functions
tags: Cryptography
---

In this note we mainly discuss common cryptographic primitives: one-way functions (OWF), one-way permutations (OWP) and trapdoor functions (TDP).

## 1.One-way functions and relatives

**Definition 1.1 (negligible function)** A function $\epsilon(\cdot)$ is negligible if $\forall$ $c>0$ $\exists$ $N_c$ such that $\forall$ $n>N_c$, $\epsilon(n)<\frac{1}{n^c}$.  

For picture examples of **negligible/non-negligible/noticeable** functions, see [this post](https://jiyuzhang1994.github.io/negligible/).

Intuitively, a one-way function is a function that is easy to compute but difficult to invert. Formally,

**Definition 1.2 (uniform OWF)** A function $$f: \{0,1\}^* \rightarrow \{0,1\}^*$$ is said to be one-way if  

1. For any $x$ that is in the domain of $f$, $f(x)=y$ can be computed in polynomial time.  
2. For any PPT algorithm $A$ and all suffciently large $n$ ($n>N_c$ for some $N_c$),  
$$\Pr \left[ x \leftarrow \{0,1\}^n,\ f(x) = y :\ z\leftarrow A(y, 1^n),\ f(z) = y \right]\leq \epsilon(n)$$  

**Discussion.** Note that requiring the unary number $1^n$ as adversary's input is necessary for excluding pathetic functions. For example, consider the function $$f(x) = \lvert x\rvert$$. The adversary's input has length $log(\lvert x \rvert)$, while the original $x$ has length exponential in that. This function should be one-way because the adversary doesn't have enough time to write down the answer. But it is intuitively easy to invert. 

**Discussion.** The function that satisfies the above definition is called a **uniformly strong one-way** function. We will talk about weak one-way function later. It is *uniform* because we assume the adversary is a uniform algorithm that can take any input length. If in the second requirement above, we allow the adversary to use different algorithms for different lengths (i.e. it is a non-uniform circuits family.), then we say the function is **non-uniformly strong one-way**.   

In the rest of these notes we will assume the adversary (instand call it a single algorithm) $$A = \{A_1, A_2, \ldots\} $$ is non-uniform. When we talk about OWFs, OWPs and TDPs, we implicitly talk about non-uniform primitives, i.e. the adversary is non-uniform.  

We now introduce weak one-way functions. A weak one-way function is a function that is hard to invert with noticeable probability.

**Definition 1.3 (weak OWFs)** A function is called weak one-way if  

1. For any $x$ that is in the domain of $f$, $f(x)=y$ can be computed in polynomial time.  
2. $\exists\ c$ such that for any PPT adversary $A$ and all suffciently large $n$ ($n>N_c$ for some $N_c$) 
$$\Pr\left[x \leftarrow \{0,1\}^n,\ f(x) = y:\ z\leftarrow A(y, 1^n),\ f(z) = y\right]\geq \frac{1}{n^c}$$  
where $negl(n)$ is the negligible function.

However, there is a theorem due to Yao says that any weak one-way function can be transformed into a strong one-way function.  

**Theorem 1.4 (Yao)** There exists a weak one-way function iff there is a strong one-way function.  

**Proof** See [this post](https://jiyuzhang1994.github.io/wowftosowf/).

We now introduce one-way permutations,  trapdoor permutations.  

**Definition 1.5 (OWP)** A function $f$ is a one-way permutation if 
1. It satisfies all requirements of one-way function.
2. It is a permutation.

Trapdoor functions are OWPs that, given auxiliary information, can easily invert $f(x)$.  

**Definition 1.6 (TDP)** A function $f$ is a TDP if  
1. It satisfies all requirements in Definition 1.5  
2. There is a polynomial-time algorithm $I$, a constant $c$ and a string $t_k$ such that, for all large enough $k$, $t_k$ is of length at most $O(k^c)$, and for any $x\in \{0,1\}^k$, $I(f(x), t_k) = z$ where $f(z) = f(x)$.

**Remark.** The above definition of OWFs might be inconvenient for practically cryptographical use. We'll give some informal reasons:
 
1. The definition is hard to extend to permutations.  
2. The definition is $$\{0,1\}^*$$, and it doesn't allow us to sample (i.e. randomly choose) inputs according our security parameters $n$.  

**Definition 1.7 (Collection of OWFs)**  A set of functions $$\{f_i:D_i \to R_i\}_{i\in I}$$ is a collection of one-way functions if  

1. $\exists$ an efficient algorithm $Gen$ that on $1^n$ samples an index $i\in I$.  
2. $\exists$ an efficient algorithm $Samp$ that on $i$ samples an element $x$ in the domain $D_i$ of $f_i$.  
3. $\exists$ an efficient algorithm that on $i, x$ evaluates $f_i(x)$.  
4. it's hard to invert, i.e. for $n$ and any p.p.t $A$ 

$$\Pr[i\leftarrow Gen(1^n), x\leftarrow D_i, y\leftarrow f_i(x):A(1^n, y) = x]\leq negl(n)$$

## 2. Complexity Assumptions

We state necessary complexity assumptions for the existence of one-way functions. These assumptions are useful for us to argue in the form: a protocol $A$ is not secure because it can break our complexity assumptions.  

First of all, we should observe that  
 
**Theorem 2.1** If $P=NP$, then one-way functions don't exist.  

**Proof.** If $P=NP$, then the adversary can non-deterministically guess all values of $x$ and evaluate f(x) to verify the answer.  

Since we assume (in the uniform model) that the adversary is a PPT (i.e. in BPP), we should see that even $BPP = NP$ will imply the non-existence of uniform OWF. 

In summary, our two basic assumptios will be: $P\subseteq BPP \not\subseteq NP$.

While we don't know whether $BPP \neq NP$ or $P/poly \neq NP$ hold, we can show that $BPP \subseteq P/poly$.  

**Theorem 2.2 (Adleman)** $BPP\subseteq P/poly$  

**Proof.** For a language $L$ in BPP that can be recognized by a Turing machine $M$, it can be shown that by repeatedly running $M$ many (at most polynomial) times and taking the majority vote, we can reduce the error probability to arbitrary exponentially small value. Let's assume the error probability on both sides is $2^{-r}$ for some $r>n$, so the number of coin flips used by the new Turing machine $M^\prime$ is at most $r$.  
    According to the above, its' equivalent to say that for any fixed $x$, for a random string of length $r$, the probability that $M^\prime(x, r)$ accepts is at most $2^{-r}$. We use the union bound to bound that, for all possible inputs $$x\in \{0,1\}^n$$, the probability that $M^\prime$ rejects at least one of these $x$ is at most $2^{n-r} < 1$. Therefore, for a random string, there is a positive probability (greater than $1-2^{n-r}$) that can make all $x$ be accepted by $M^\prime$. We take the existence of such a string and hardwire it into our circuit. By doing this the circuits family can decide $L$ without any randomness.  
    
## 3. Candidates Functions for OWFs, OWPs and TDPs  

In this section we introduce specific problems and assumptions and give explicit candidates for OWFs, OWPs, and TDPs.

**Definition 3.1 (Integer Multiplication)** $$f: \mathbb{N}^2 \to \mathbb{N}$$ is defined by:  

$$f(x,y) = x\cdot y$$  

Denote the set of all $n$-bit prime numbers as $\Pi_n$  
**Assumption 3.2 (Factoring Assumption)** $\forall$ adversary $A$, $\exists$ an $\epsilon(\cdot)$ such that  

$$\Pr \left[ p,q\leftarrow \Pi_n, N = pq: A(1^n, N)\in \{p, q\}  \right] \leq \epsilon(n)$$  

**Theorem 3.3** If the factoring assumption is true, then integer multiplication is a weak one-way function.

**Proof.** Suppose it's not weak one-way, show that you can break the factoring assumption.  

**Assumption 3.4** (Discrete log) Let $G_q$ be a group of **prime order** $q$ and $Gen_q$ be the set of generators of $G_q$ , $\forall$ adversary $A$, $\exists$ an $\epsilon(\cdot)$ such that  

$$\Pr \left[ q\leftarrow \Pi_n, g\leftarrow Gen_q, x\leftarrow \mathbb{Z}_q: A(g^x) = x \right]\leq \epsilon(n)$$  

**Discussion.** $G_q$ being a prime order is essential, and we usually choose a prime $q = 2p +1$, which is called a Sophie Germain prime or a "safe" prime. Otherwise, there are known efficient algorithms for solving discrete log in some special cases. See discussion in this [page](https://www.doc.ic.ac.uk/~mrh/330tutor/ch06s02.html).  

**Discussion.** However, as noted in P&S, there are several problems of using Sophie Germain primes. Some basic theoretical properties are unknown: it is not known (a) whether there are infinite number of SG primes, and (b) the procedure: picking a random $p$ then check whether $q=2p+1$ is a prime is not known to be efficient as the size of $q$ increases.  

