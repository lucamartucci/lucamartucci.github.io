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

Note that the computing process of PBP can be viewed as the composition of these permutations. we define that the PBP $B$ *$\alpha$-recognizes* a language $L$ if  there exists a 5-cycle $\alpha$ such that  $B(x)=\alpha \Longleftrightarrow x\in L$.

