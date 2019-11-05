---
layout: default
permalink: /derandbpl/
title: BPL and Fooling BPL
tags: Study
---

Starting from this post I will discuss about the $BPL\ vs.\ L$ problem and write notes about some known, important result. This post is an introduction to this problem.

* [Log-space computation and BPL](#bpl)
* [ROBP](#robp)
* [Fooling BPL](#fool)
  

## <a name="bpl"></a> 1. Log-space Computation and the class BPL  

We are interested in space-bounded probabilistic computation, specifically, on Turing machines that have logarithmic working space. We start by describing such machines.
### Log-space Probabilistic Turing Machine

A log-space probabilistic turing machine(PTM) consists of the following parts:  a two-way read-only input tape, assuming that the input is of size $n$; a normal read-write working tape of size $O(\log n)$, a finite state control that has a finite number of states, a output tape that is write-only. In addition, we need to model the condition that the machine has access to infinite randomness. That is, every time the machine doesn't know what to do, it flips a coin and decides its next step. We model this by giving it access to an infinite one-way random tape, it reads the next random bit when it is needed. It must write the random bit down (in the work tape) if it wants to retrieve it later. 

![log-space PTM](/assets/L-PTM.jpg)  

In the execution of this TM, a *configuration* consists of the position of read head on the input tape plus the contents on it, the position of read-write head on the working tape plus the contents, the specific state on the finite state control. We should see that the total number of configurations is $O(\log n) \cdot 2^{O(\log n)}$(# of possible work tape configuration) $\cdot \lvert \Delta \rvert$(# of states which is finite) $\cdot n$ (# of possible input tape configuration) $=2^{O(\log n)}$.  

### BPL  

$BPL$ can be written as $BP_HL$ or $BP_HSPACE(\log n)$. It refers to *Bounded-error Probabilistic Log-space* that halts absolutely (hence the sub "H"). Formally, we say a language $L$ is in $BPL$ if there is a log-space PTM recognizes it and satisfies the following:  

* it always halts.  
* if $x\in L$, it accepts with probability at least 2/3.  
* if $x\not\in L$, it rejects with probability at least 2/3.  
* the probability is taken over the coin flips of the TM.  

We emphasize that in the definition of $BPL$ the PTM halts absolutely, which is the case we're interested in. For discussion on other PTMs(e.g. PTM that halts almost surely) , readers should refer to the survey [1]. We now state some observations:  

* The PTM runs in time at most $2^{O(\log n)}$, otherwise the PTM falls in loop and never halts.
* Since it runs in time at most $2^{O(\log n)}$, it uses at most $2^{O(\log n)}$ random bits.  

In fact, restricting a PTM to use at most $2^{O(\log n)}$ randomness is equivalent to say it halts absolutely. Consider the following: the PTM uses space $O(\log n)$ to maintain a counter, every time the PTM flips a coin, the counter is reset to 0, if the counter reaches $2^{O(\log n)}$, then it halts and reject. It can be seen that this halting PTM recognizes the same language.  

## <a name="robp"></a> 2. Read-once Branching Program

In this section we introduce a (non-uniform) computational model that simulates space-bounded computation. A branching program (in our interest) is a layed acyclic graph, each layer has a total number of $2^{O(\log n)}$ nodes. You can think of each of these nodes as a configuration in the execution of the above BPL machine on a given input, so each layer has the same nodes and, since it's halting, the same node isn't entered twice. For each input, there is a starting node in the first layer that represents the starting configuration. In the last layer there are only 2 nodes, one represents the "accept" state and the other represents the "reject" state. Between the $i$th and $i+1$th layer there are transition edges mapping from nodes in the $i$th layer to the nodes in the $i+1$th layer. Each of these edges is labeled a string $$r_i \in\{0,1\}^m$$. You should think of this string as the $m$ coin flips tossed by the machine to decide which configuration to enter in the next step (tossing $m$ coins just generalizes the case of tossing one coin). A computation on a branching program with input $r_n$ is just a path from a node in the first layer to the Accepting/Rejecting node in the last layer, between it reads $r_i$ and chooses the edge accordingly. We say a branching program is ROBP (Read Once Branching Program) if it reads its input in a one-way fashion.

For a computation on the BPL machine with input $x$, you can think of a ROBP simulates the computation by:  

1. picking a node in the first layer as starting node according to the input $x$; 
2. read the sequence of random bits on the original random tape as input and execute accordingly.  
3. note that it reads the input in a streaming (one-way) fashion.

The picture below represents a branching program using $r_n$ randomness and has $2^{O(\log n)}$ nodes in each layer.  

For convenience, we denote that maximum number in a layer of the (RO)BP the *width* of it. We denote the length of the (RO)BP as the number of layers in it.

![ROBP](/assets/ROBP.jpg)

## <a name="fool"></a> 3. Fooling BPL  

From the previous sections, we can see that to fool every language in BPL, it suffices to fool all ROBPs that have width at most $2^{O(\log n)}$. We formally define what we mean by fooling a ROBP.    

**Definition 3.1** For a ROBP $B: \{0,1\}^{n} \rightarrow \{0,1\}$, we say a pseudorandom generator $$G: \{0,1\}^{r} \rightarrow \{0,1\}^{n}$$  where $r<n = 2^{O(\log n)}$ $\epsilon$-fools $B$ if  

$$\lvert \Pr \left[ B(G(U_{r}))\right] - \Pr\left[B(U_n) \right]\rvert < \epsilon$$

**References**  

[1] Michael Saks, "Randomization and Derandomization in Space-Bounded
Computation" http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.17.1185&rep=rep1&type=pdf


 
