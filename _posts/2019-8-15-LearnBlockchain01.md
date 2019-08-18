---
layout: default
permalink: /LearningBlockchain01/
title: Hash Function for Cryptocurrency
tags: Cryptography
---
Cryptocurrency relies on special cryptographic hash functions with nice properties. Today I'd like to explain these properties and discuss their applications.  This notes refered to < Bitcoin And Cryptocurrency Technologies A Comprehensive Introduction > by Bonneau et al.

A *hash function* is an efficiently computable function $$H: \{0,1\}^*\rightarrow \{0,1\}^k$$ where $k$ is a fixed parameter. That is  
1. Its input can be of string of any size.  
2. Its output is of fixed length, usually set to be 256 bits.  
3. It is efficiently computable.

While to be useful for cryptocurrency, it requires the hash function to be of special *cryptographic* hash function. Specifically, the following three properties hold: (1) Collision resistant;  (2) Hiding; (3) Puzzlefriendliness.  

I'll explain these properties in detail.  

## Property 1: Collision Resistant

**Definition.** *(Collision Resistant)* A hash function $H$ is said to be *Collision Resistant* if it is **infeasible to find** two values $x$ and $y$, such that $x\neq y$ yet $H(x) = H(y)$.

The following notes are made:  
1. Collision exists as long as the input set size is larger than the output set size.  
2. There is a trivial algorithm to find a collision for a (say) 256-bit output: pick $2^{256}+1$ distinctive values, compute the hashes for each of them and check equivalence for each pair. However, this method will take more than octillion years before finding such a pair. And we consider this method **not feasible**.  
3. No hash functions have been proved to be collision resistant. i.e, there is possibility that there exists efficient (feasible) algorithm to find collisions. The hash functions we rely on in practice are those people have tried very very hard to find a method to break (i.e. find an efficient algorithm to compute collisions).   

### Application: Online File Storage
The collision resistant property can be used in the following logic: If one knows $x$ and $y$ are different, then it's safe to say $H(x)$ and $H(y)$ are different. This can be confirmed by a contradictory argument. If one knows/can find/can compute a pair of $x$ and $y$ s.t $x\neq y$ and $H(x) = H(y)$, this violates our assumption that $H$ is collision resistant.  

Now one application of this logic is *Online File Storage*. Suppose you have a very large file and would like to upload it to a online file storage system so that you can download it later, possibly on another computer. How can you be sure that the file you download later is the same as you uploaded. One way is to store the file locally and compare it with the downloaded version bit by bit. Well, this may not be efficient since the file is very large. However, if you only store the hash of the file locally, and compare it with the hash of the file you downloaded, it is much more efficient. And the collision resistant property guarantees that, the system is hard to find a different file and its hash is the same as that of the one you uploaded.  

This is like you're memorizing a specifc sign of your item while no one can find a fake item that has the sign as yours. When you get it back, you just examine this sign and figure out whether it is indeed the item you stored.  

## Property 2: Hiding  

Informally the hiding property says that if one is given the output of the hash function $y=H(x)$, he is infeasible to find the value of $x$. Again, there is a trivial way to find $x$, just try all the possible $x$ and compute $H(x)$ to find the specific $x$ with $y=H(x)$. Note here we don't take the case where $x\neq x^\prime$ and $y=H(x)=H(x^\prime)$ into consideration.  

So one way to implement this property is to make the input set large enough so it takes "infeasible" time to use the above algorithm. But we want to do this with a small input set, and this can be done by concatenating the input with a random string. Formally,  

**Definition.** *(Hiding)* A hash function $H$ is said to be *Hiding* if when a secret value $r$ is chosen from a probability distribution that has *high min-entropy*, then given $H(r\|\|x)$, it's infeasible to find $x$.

The definition of min-entropy can be found in many text books , for example, at [here](http://people.seas.harvard.edu/~salil/pseudorandomness/). Informally, a distribution with *high min-entropy* means that the distribution is close to "flat", i.e. each of the event has almost identical chance to happen.  

### Application: Commitment (Digital Envelope)  

A commitment, also called a digital envelope, is the abstraction of taking a value $x$ and put it into an envelope then send it to a receiver. Later the sender can reveal the value in the envelope to the receiver. Informally, two properties are required for a commitment:  

1. Hiding. No one is able to figure out the value $x$ when the value is not revealed.  
2. Binding. After the sender has made a commitment, he is not able to change the value in the envelope. 

Formally, a commitment scheme consists of two algorithms:  

* commit(msg, nonce) The commit function takes as input a message and a secret random value nonce then return a commitment.
* verify(com, msg, nonce) The verify function takes as input a commitmentm, a message and a nonce. It return true iff com == commit(msg, nonce).

The hiding and binding property can be formalized as following:

1. Hiding. Given $com$, it is infeasible to find $msg$. 
2. Binding. It is infeasible to find two pairs $$(msg, nonce)$$ and $(msg^\prime, nonce^\prime)$ such that $msg\neq msg^\prime$ and $commit(msg, nonce) == commit(msg^\prime, nonce^\prime)$.  

Note that the $nonce$ and $nonce^\prime$ is not necessarily the same. Also $nonce$ can only be used once.

To use a commitment scheme, the sender first generate a random $nonce$, then apply $commit$ to $msg$ and $nonce$ and return $com$. Later when the sender wants to reveal $msg$, he publishes the $nonce$ and the $msg$, others can verify $msg$ is indeed what the sender has commited using $verify$.  

**Implementation**

Commitment can be implemented using cryptographic hash function.   

* $commit(msg, nonce) = H(msg\|\|nonce) = com$
* $verify(com, msg, nonce) = (boolean)\ (H(msg\|\|nonce) == com)$

It is an easy practice to check that the *Hiding* property of $H$ implies the hiding property of the commitment. The *Binding* property is implied by the *Collision Resistant* property of $H$.  

## Property 3: Puzzle Friendliness  

sdf