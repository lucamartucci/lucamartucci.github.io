---
layout: default
title: The Halting Problem
permalink: /halting/
---
This is the manuscript I worte in an email to explain the halting problem to my group partners in UCSB's language class. It is intended for audience with zero background. 

Warm-ups: I want you to be comfortable with/ believe the following set-up.

1. A computer program takes as input a string and outputs an answer, in this case we say it halts. However it may fall in loops on this input and runs forever, we say it doesn't halt in this case.

2. Computer programs themselves are represented as (binary) strings in the computer.

3. Therefore, it is important to get comfortable with the idea that a computer program can take as input a description (string) of another computer program, and answer something accordingly, or it never halts.

The Halting Problem asks:

Does there exist a computer program D that can do the following? 

-----D's description-----

D(D1,x):

D takes as input a pair (D1, x), and determines whether D1 will halt on x or not.

If D1 halts on x, D outputs YES. If D1 doesn't halt on x, D outputs NO.

-----END of D's description-----

The answer to the Halting Problem is no. i.e. there doesn't exist such a computer program D.


Proof: assume there exists such a D, we show a contradiction.

We use D as a subroutine to build a computer program D2. (This is possible because D is just a string description, we can embed this string into D2's description).

D2 does the following:

-----D2's description-----

D2(D1)

D2 takes as D1 as input, it utilizes the subroutine D to decide whether D1 will halt on D1 (itself).

if D claims D1 will halt on D1, i.e. D(D1,D1) = YES,  then D2 doesn't halt.

if D claims D1 doesn't halt on D1, i.e. D(D1,D1) = No, then D2 halts and outputs YES.

-----END of D2's description-----

Now what will happen when D2 takes as input itself's description?

if D claims D2 will halt on D2, i.e. D(D2, D2) = YES, then D2 doesn't halt.

if D claims D2 won't halt on D2, i.e. D(D2, D2) = NO, then D2 halts and answers YES.

You should see that we have reached a contradiction.