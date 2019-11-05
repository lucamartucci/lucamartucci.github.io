---
layout: default
permalink: /derandbpl/
title: BPL, Derandomize BPL
tags: Study
---

Starting from this post I will discuss about the $BPL\ vs.\ L$ problem and write notes about some known, important result.

* [BPL](#bpl)
  

## <a name="bpl"></a> 1. Log-space Computation and the class BPL  

We will be interested in space-bounded probabilistic computation and specifically, on Turing machines that have logarithmic working space. We start by describing such machines.
### Log-space Probabilistic Turing Machine

A log-space probabilistic turing machine consists of the following part:  a two-way read-only input tape, assuming that the input is of size $n$; a normal read-write working tape of size $O(\log n)$, a finite state control that has a finite number of states, a output tape that is write-only. In addition, we need to model the condition that the machine has access to infinite randomness. That is, every time the machine doesn't know what to do, it flips a coin and decides its next step. We model this by giving it access to a infinite one-way random tape, it reads the next random bit when it is needed. It must write the random bit down (in the work tape) if it wants to retrieve it later. 

![log-space PTM](/assets/L-PTM.jpg)  

In the execution of this TM, a *configuration* consists of the position of read head on the input tape plus the contents on it, the position of read-write head on the working tape plus the contents, the specific state on the finite state control. We should see that the total number of configurations is $\log n \cdot 2^{O(\log n)}$(# of possible work tape configuration) $\cdot \lvert \Delta \rvert$(# of states which is finite) $\cdot n$ (# of possible input tape configuration) $=2^{O(\log n)}$.  



![ROBP](/assets/ROBP.jpg)






 
