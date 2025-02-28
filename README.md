# The Three Qubit Repeition Code

## Overview

Quantum information stored as a qubit is inherently unstable, and prone to error. The key idea behind quantum error correction (QEC) is that we may encode information to protect it from noise, allowing us to detect when an error has occured (in this context an unintentional bit-flip) and allowing us to decode this error to retrieve our initial state.

## The classical error correction

One way of preventing this kind of error within classical communication channels is via repetition code. Say we are sending a bit with the value $1$: we simply replicate this, such that $1 \to 111$, and send this information through our system. The effect of noise within our system is to flip a bit, and this error occurs with probability $p$. It is therefore clear why repetition of the same bit reduces our uncertainty when an error occurs. Suppose the signal $110$ was recieved at the other end of our communication channel - we can deduce with high certainty that the information that was originally sent was in the form $111$, and hence we can re-translate (decode) the information $111 \to 1$.

<p align="center">
  <img src="deutch.jpeg" alt="Image 1" width="600"/>
</p>
<p align = "center">
<i>Circuit implementing Deutch's algorithm from Nielsen and Chuangs 'Quantum Computation and Quantum Information'</i>
</p> 

## The Algorithm:

Consider a case where we want to determine wether a function is constant or balanced. We have a binary function:

$$f: [0, 1] \to [0, 1]$$

Which takes an input of either 0 or 1 and returns either 0 or 1.

If this function were balanced, it would have as many outputs for 0 as it did for 1, and if it were constant it would either output only 0 or only 1. A classical computer would need two queries to this function to determine wether $f(0) = f(1)$ amd that the function is therefore constant, whilst a quantum computer would require a single query.

This is done by implementing a reversible oracle function - essentially a 'black-box' - which takes an input, performs a specific operation, and returns an output.

## Circuit Implementation:

We start in the state 

$$|\Psi\rangle = |00\rangle$$

apply a CNOT gate:

$$|\Psi_0\rangle = |01\rangle$$

and then a Hadamard gate:

$$|\Psi_1\rangle = |+-\rangle = \frac{1}{\sqrt{2}} (|0\rangle|-\rangle + |1\rangle|-\rangle)$$

Which is where we query our oracle, $U_f$. We find that this is in the form of a phase oracle with phase kickback:

$$U_f|x\rangle|-\rangle = (-1)^{f(x)}|x\rangle|-\rangle$$

So therefore:

$$|\Psi_2 = \frac{1}{\sqrt{2}}((-1)^{f(0)}|0\rangle|-\rangle + (-1)^{f(1)}|1\rangle|-\rangle)$$

We simplify this by factoring out and omitting our $|-\rangle$ state as it is not required form here on.

## Results:

We now consider our two cases: where $f(0) = f(1)$ or $f(0) \neq f(1)$.

We find that our state $|\Psi_2\rangle$ state becomes $|\Psi_2\rangle = \pm |+\rangle$ for $f(0) = f(1)$, and $|\Psi_2\rangle = \pm |-\rangle$ for $f(0) \neq f(1)$.

A Hadamard gate is then applied to the first qubit, and we make our measurement. Then:

- if we measure 0, then the function must be balanced as $f(0) = f(1)$
- if we measure 1, the function must be constant, as $f(0) \neq f(1)$

And using a single query, we have shown that a function is either constant or balanced.

Deutch's algorithm is a specific case of the Deutch-Josza algorithm, which is concerned with a similar probem: determining wether a function is constant or balanced for an $n$ qubit register:

$$f: [0, 1]^n = [0, 1]$$
