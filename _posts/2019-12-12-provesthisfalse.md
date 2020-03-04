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

\begin{bmatrix}
2 & 1 \\
0 & 2 
\end{bmatrix}

and 

\begin{bmatrix}
1 & 0 \\
0 & 2 
\end{bmatrix}  

has the same eigenvalues but are not similar.

