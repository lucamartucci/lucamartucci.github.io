---
layout: default
permalink: /wowftosowf/
title: Hardness Amplification for weak O.W.Fs
---

We prove that if there exists a weak one-way function, then there exists a strong one-way functions, in the sense that the weak o.w.f can be converted into a strong o.w.f. We call this transformation as **Hardness Amplification**.

**Theorem 1.** For any weak one-way function $$f:\{0,1\}^*\to \{0,1\}^*$$, **there exists a polynomial** $m(\cdot)$ such that $$f^\prime (x_1,\ldots ,x_{m(n)})= f(x_1), \ldots, f(x_{m(n)})$$ is a strong one-way function.  

**Proof.**  

Suppose $f$ is $q(n)$-weak, we show that there exists a polynomial $m(\cdot)$ such that if $f^\prime$ as above is not a strong o.w.f, we can invert $f(x)$ with probability greater than $2q(n)$ for random input $x$.  

Assume $f^\prime$ is not a strong o.w.f, there exists $A^\prime$ s.t  

$$\Pr \left[\vec{x} \leftarrow \{0,1\}^{m\cdot n}, \vec{y}=f^\prime(\vec{x}): A^\prime(1^{mn}, \vec{y})= \vec{x} \right] \geq 1/p(mn)$$  

for some polynomial polynomial $p(mn)$. In fact, we'll show that $m= 2n q(n)$ suffices for our purpose.  

We next present algorithms for inverting $f(x)$.  

***

$A_0(y, f, A^\prime)$:  

* Choose $i\in [m]$ uniformly at random.  
* Choose $$x_j\in \{0,1\}^n $$ for $$j\in[m] \backslash \{i\}$$ at random.  
* $y_i \leftarrow y$, $y_j \leftarrow f(x_j)$, we get $\vec{y}$. Then compute $A^\prime (\vec{y})$.  
* Output $x_i$ if $f(x_i) = y$. Otherwise output fail.  

***

We also would like to amplify our probability for success by repeating $A_0$ as many times as possible  (as long as it is in p.p.t). We define $A$ which repeats $A_0$ for $2nm^2 p(mn)$ times.  We'll show that $A$ inverts $f$ with good probability.  

For our analysis of $A$, we say $x$'s are "good" if  

$$\Pr \left[y\leftarrow f(x) : A_0(1^n, y) = x  \right] \geq \frac{1}{2m^2p(mn)}$$  

We next show that  

1. On those good $x$'s, $A$ can invert $f(x)$ with good probability.  
2. There are sufficiently many good $x$'s.  

Finally we can show it contradicts the fact that $f$ is $q(n)$-weak one-way.  

On these good $x$'s, we know that the probability that $A$ fails to invert $f(x)$ is at most  

$$(1-\frac{1}{2m^2p(mn)})^{2nm^2 p(mn)} \leq e^{-n}$$  

which is negligible.  

We'll now show there are at least $2^n(1-\frac{1}{2q(n)})$ good $x$'s. We prove this by contradiction.  

Assume there are at most $2^n(1-\frac{1}{2q(n)})$ good $x$'s, we show (1) does not hold.  

$$\begin{align*}
  \Pr \left[\vec{x} \leftarrow \{0,1\}^{m\cdot n}, \vec{y}=f^\prime(\vec{x}): A^\prime(1^{mn}, \vec{y})= \vec{x} \right] &\leq \Pr \left[\vec{x} \leftarrow \{0,1\}^{m\cdot n}, \vec{y}=f^\prime(\vec{x}): A^\prime(1^{mn}, \vec{y}) \text{ succeeds} \land \text{all } x_i \text{'s are good} \right]\\  
  &+ \Pr \left[\vec{x} \leftarrow \{0,1\}^{m\cdot n}, \vec{y}=f^\prime(\vec{x}): A^\prime(1^{mn}, \vec{y}) \text{ succeeds} \land \text{some } x_i \text{'s are bad} \right]\\   
 \end{align*}$$  
 



**References**  

[1] R.Pass & A.Shelat. A Course in Cryptography.  
