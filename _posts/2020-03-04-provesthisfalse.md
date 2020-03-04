---
layout: default
permalink: /provesthisfalse/
title: how to prove sth is wrong
tags: Proof
---

Reading linear algebra and its application 4th ed by David C. Lay, on page 294 there is a theorem like this:  

**Theorem 4.** If $n\times n$ matrices $A$ and $B$ are similar, then they have the same characteristic polynomial and hence the same eigenvalues (with the same multiplicities). 

**Proof.** The proof uses multiplicative property of determinants.

$det(B-\lambda I) = det(P^{-1}AP-\lambda I) = det(P^{-1}AP-\lambda P^{-1}IP) = det(P^{-1}(A-\lambda I)P) = det(P^{-1})\cdot det(A-\lambda I)\cdot det(P)= det(A-\lambda I)$  

So **similarity implies the same eigenvalues**.

Does the converse hold? There is a warning below:

The matrices 

$$
A= \begin{bmatrix}
2 & 1\\
0 & 2 
\end{bmatrix}
$$
and 
$$
B = \begin{bmatrix}
2 & 0\\
0 & 2 
\end{bmatrix}  
$$
has the same eigenvalues but are not similar.

OK, it's easy to verify that they have the same eigenvalues, but how to prove they are not similar?

A first thought in mind is, we want to prove there does not exist $P$ such that $P^{-1}AP = B$. Well this seems to be hard.  

Then you google "how to prove two matrices are not similar". You find a [post](https://math.stackexchange.com/questions/1288904/show-that-matrices-are-not-similar) on math stackexchange. One answer says:"$det(A) \neq det(B)$ and similar matrices must have the same determinants."

Indeed, $det(B) = det(P^{-1}AP) = det(P^{-1})\cdot det(A) \cdot det(P) = det(A)$.  

Actually, this gives us a general strategy to prove some statement $p$ is false: **by showing some necessary property $q$ of $p$ does not hold**.  

If you want to prove $p$ is false, you first show that $p\Rightarrow q$, then you show that $q$ is false.

Another example: Ryan Williams' proof for $NEXP\not\subseteq ACC_0$ goes like this:  

$NEXP$ has poly-size $ACC_0$ circuits $\Rightarrow$ NEXP has small witness circuits in $ACC_0$ $\Rightarrow$ Faster satisfiability algorithm $\Rightarrow$ which is wrong due to nondeterministic time hierarchy theorem.  