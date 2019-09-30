---
layout: default
permalink: /ProofOfUndo/
title: Argument of Correctness of Undo Implementation
tags: Job
---

Recently I've implemented a simple project of text editor = =. One part of this project is to implement the undo functionality. In case the recuiter might be interested, I'd like to provide a proof here that my idea of implementation can correctly recover deleted characters in its original position, the potential problematic case won't happen.  

## Introduction
Undo is the operation that can undo the user's last $n$ operation(inserting/deleting characters). 

The difficulty lies in how can one keep track of the original position of the characters deleted. Well, in my implementation, nothing else is needed: just remove the node(which contains a character) and put it into a stack.

The data strucutre I used for text editor is a doubly linked list, each node has a value contains the specific character, and a **prev** pointer to the previous character node and a **next** pointer to the next character node. Visualized as following:  

<div>$$a\leftarrow s \rightarrow b$$  </div>

To recover the deleted node $s$, simply find its (relative) position by referring to its previous or next node, then insert it in.  While one thing might be problematic: **what if when (the deleted) $s$ is to recover, its previous nodes a or b are not in the data structure, i.e. a and b haven't been recovered**. Therefore we can't find its position. While I argue that this will not happen. 

## The Argument
I'd like to show the following: **when $s$ is to recover, its previous or next nodes must exist in the data structure**, which is a simple argument by contradiction:  
Suppose for the contradiction that $a$ and $b$ are not in the data structure, then $a$ and $b$ must be deleted before $s$ is deleted. However, in this case, by the time $s$ is deleted, its **prev** and **next** cannot be $a$ and $b$, which is a contradiction.

