---
layout: default
permalink: /barrington/
title: Barrington's Theorem
tags: Complexity
---

In this post we prove Barrintong's theorem.  

Barrington's theorem implies that the complexity class NC1 is equal to the class of constant width branching program.  

**Theorem 1.** (Barrington) For any general circuit of fan-in 2 and depth $d$, there is a constant width (actually, width 5) branching program of length $4^d$ that simulates it. Especially when $d=O(\log n)$, then the branching program is of length at most $n^{O(1)}$.