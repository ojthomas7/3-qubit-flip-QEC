# The Three Qubit Repeition Code

## Overview

Quantum information stored as a qubit is inherently unstable, and prone to error. The key idea behind quantum error correction (QEC) is that we may encode information to protect it from noise, allowing us to detect when an error has occured (in this context an unintentional bit-flip) and allowing us to decode this error to retrieve our initial state.

## The classical error correction

One way of preventing this kind of error within classical communication channels is via repetition code. Say we are sending a bit with the value $1$: we simply replicate this, such that $1 \to 111$, and send this information through our system. The effect of noise within our system is to flip a bit, and this error occurs with probability $p$. It is therefore clear why repetition of the same bit reduces our uncertainty when an error occurs. Suppose the signal $110$ was recieved at the other end of our communication channel - we can deduce with high certainty that the information that was originally sent was in the form $111$, and hence we can re-translate (decode) the information $111 \to 1$.

## Quantum error correction

This procedure is not quite as simple in quantum systems, for a few reasons:

- The no cloning theorem: Cloning a quantum state to produce an identical copy is forbidden.
- Errors in quantum mechanics are continuous: Given this, determining which error had occured in order to correct it would require infinite precision.
- Measurement destroys quanutm information

## The Solution

Fortunately, there are ways we can work around these problems.

Consider the arbitrary qubit $| \Psi \rangle = \alpha |0 \rangle + \beta |1 \rangle$, which we are going to send through our system. We can encode this into three qubits as $|\Psi_2 \rangle = \alpha |000 \rangle + \beta |111 \rangle$ in the following manner:

<p align="center">
  <img src="isometry.jpeg" alt="Image 1" width="400"/>
</p>
<p align = "center">
</p> 
