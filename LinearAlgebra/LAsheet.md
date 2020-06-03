---
layout: default
permalink: /LAsheets/
title: Linear Algebra Review Sheets
tags: LinearAlgebra
---


**Lemma 2.21 (Linear Dependence Lemma)** Suppose $v_1, \ldots, v_m$ is a linear dependent list. Then there exists a $j\in \{1, \ldots, m\}$ such that,  

(a) $v_j\in span(v_1,\ldots, v_{j-1})$, and  
(b) If $v_j$ is removed from the list, then the remaining list spans $span(v_1, \ldots, v_m)$.

(b) is easy once we have proved (a). To prove (a), assume it is not the case. Then in particular $v_m$ is not a linear combination of $v_1,\ldots,v_{m-1}$, which means $v_1,\ldots ,v_m$ are linearly independent, a contradiction. 

In fact this lemma is very powerful.

