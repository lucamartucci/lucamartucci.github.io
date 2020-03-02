---
layout: default
permalink: /barrington/
title: Barrington's Theorem
tags: Complexity
---

In this post we prove Barrintong's theorem.  

Barrington's theorem implies that the complexity class NC1 is equal to the class of constant width branching programs. Since we know that constant width branching program can be computed by NC1 circuits.  

**Fact.** Constant width branching programs can be computed by general fan-in 2 circuits with $O(\log n)$ depth. 

The idea is to compute recursively using divide and conquer (divide the branching program into the first half and the second half).



**Theorem 1.** (Barrington) For any general circuit of fan-in 2 and depth $d$, there is a constant width (actually, width 5) branching program of length $4^d$ that simulates it. Especially when $d=O(\log n)$, then the branching program is of length at most $n^{O(1)}$.

Recall that a width $w$ branching program has layers of the same vertices. Each vertex in the $i$-th layer has two out edges (labeled 0 and 1) mapping to two vertices in the next layer, depending on the input $$x_i\in \{0,1\}$$. So essentially between every two consecutive layers there are two mappings $f, g : [w] \rightarrow [w]$.  We consider a special branching program called **Permutation Branching Program (PBP)** where $f,g$ are permutations.  

Note that the computing process of PBP can be viewed as the composition of these permutations.  We say a permutation in $S_5$ is a 5-cycle if it is exactly a cycle of length 5. For example, $1\rightarrow 3\rightarrow 5\rightarrow 4 \rightarrow 2 \rightarrow 1$. We denote it as $(13542)$ for convenience.   

we define that the PBP $B$ *$\sigma$-computes* a language $L$ if  there exists a 5-cycle $\sigma$ such that  $B(x)=\sigma\Rightarrow x\in L$ and $B(x) = e \Rightarrow x\not\in L$ where $e\in S_5$ is the identity.  

We proceed to prove a few lemmas, then we will prove that $O(\log n)$-depth circuit can be recognized by a 5-cycle PBP.

**Lemma 1.** Let $\sigma, \tau$ be any two 5-cycle. If there is a PBP $B_1$ $\sigma$-computes a language $L$, then there is a PBP $B_2$ of the same length that $\tau$-computes $L$.  

**Proof.**  

Let $\sigma = (\sigma_1\sigma_2\sigma_3\sigma_4\sigma_5)$ and $\tau = (\tau_1\tau_2\tau_3\tau_4\tau_5)$. Consider the permutation $\theta = (\tau_1\rightarrow \sigma_1)$, then $\theta^{-1} \sigma \theta$ = $\tau$. To see why this holds, consider $\tau_i$,  

$\theta^{-1} \sigma \theta(\tau_i): \tau_i\rightarrow \sigma_i \rightarrow \sigma_{i+1}\rightarrow\tau_{i+1}$  

Therefore $B_1(x) = \sigma \Rightarrow B_2(x) = \tau$ and $B_1(x) = e \Rightarrow B_2(x) = e$.

So basically to construct $B_2$ all we need is to "embed" a $\theta^{-1}$ at the front and a $\theta$ at the end.

**Lemma 2.** If a language $L$ can be $\sigma$-computed  by a PBP for a 5-cycle $\sigma$, then its complement can be $\tau$-computed by a PBP of the same length for a 5-cycle $\tau$. 

**Proof.** 

We just embed a $\sigma^{-1}$ at the end of the PBP, so that it outputs $e$ if the original PBP outputs $\sigma$ and it outputs $\sigma^{-1}$ if the original PBP outputs $e$.


**Lemma 3.** There exists 5-cycles $\sigma, \tau$ such that $\sigma \tau \sigma^{-1} \tau^{-1}$ is also a 5-cycle. 

**Proof.**  

A concrete example is $\sigma = 12345$ and $\tau=13542$. Then $(12345)(13542)(54321)(24531) = (13254)$.  


Note that, Lemma 3 basically gives us an $AND$ gate. We can concatenate the four PBPs $B_1, B_2, B_3, B_4$ recognizes $\sigma,\tau,\sigma^{-1},\tau^{-1}$ respectively. If either $B_1(x)=e$ or $B_2(x)=e$, then $B_1B_2B_3B_4(x) = e$.  If both $B_1(x)=e$ and $B_2(x)=e$, then it outputs $e$. Otherwise it outputs $\sigma \tau \sigma^{-1} \tau^{-1}$. Combining with Lemma 2, we can also get $OR$ gate, by negating the previous outputs and applying $AND$ on them.  


**Proof of Theorem 1**  

The proof goes by induction:  

If the depth of the circuit is 0 then there is a length-1 PBP. Assume the depth of the circuit is $d-1$ and has length $4^{d-1}$ PBP and, assume WLOG, that at the top is an AND gate. The inputs of it are computed by $B_1$ and $B_2$. Then we concatenate $B_1B_2B_1^{-1}B_2^{-1}$, and now the theorem follows by lemma 3. The depth is $4^{d-1} \cdot 4 = 4^d$.

**References**  

[1] David A. Barrington. "Bounded-width polynomial-size branching programs recog- 1 nize exactly those languages in NC". https://people.cs.umass.edu/~barring/publications/bwbp.pdf


