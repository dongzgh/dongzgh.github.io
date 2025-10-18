---
title: What is Pointer Network
permalink: /blogs/what-is-pointer-network
medium: blog
category: what-is
tags:
  - ai
---

## The Core Problem: Why Pointer Nets Were Needed

Before Pointer Networks, sequence-to-sequence (seq2seq) models with attention were very successful for tasks where the output vocabulary was fixed and known in advance, like machine translation (the output is words from a target language).

However, many problems involve creating an output sequence that is composed of elements from the **input sequence itself**. The key challenge is that the size of the "output dictionary" is **variable** and depends entirely on the length of the input.

**Classic Example Problems:**
*   **Convex Hull:** Output a subset of the input points that form the hull.
*   **Travelling Salesperson Problem (TSP):** Output an ordering (a permutation) of the input cities.
*   **Text Summarization:** Output a sequence of words that are copied from the input text.

A standard seq2seq model would struggle with these because it has to choose from a fixed vocabulary. It cannot "point" to a specific item in the input.

## The Intuitive Idea

The fundamental idea of a Pointer Network is simple and elegant:

> **Instead of using attention to create a "context vector" that helps generate a word from a fixed vocabulary, use the attention weights themselves AS the output probabilities. The "output" is the act of pointing to (selecting) a position in the input sequence.**

At each decoder step, the model calculates attention scores over the input elements. The element with the highest attention score is chosen as the output for that step.

---

## The Technical Architecture

Pointer Networks build upon the sequence-to-sequence with attention framework. Let us define the model mathematically.

### 1. Encoder

The encoder is a Recurrent Neural Network (e.g., an LSTM or GRU) that processes an input sequence of vectors $X = (x_1, x_2, \dots, x_n)$, where $n$ is the variable-length input size.

The encoder computes a sequence of hidden states $(e_1, e_2, \dots, e_n)$:

$$
e_t = f_\text{enc}(x_t, e_{t-1})
$$

where $f_\text{enc}$ is the recurrent cell function. These encoder states $e_i$ serve as a transformed representation of the input, akin to "keys" and "values" for the subsequent attention mechanism.

### 2. Decoder

The decoder is another RNN that generates an output sequence $(y_1, y_2, \dots, y_m)$, where $m$ is the variable-length output size. At each time step $t$, the decoder updates its hidden state $d_t$ based on the previous state $d_{t-1}$, the previous output $y_{t-1}$, and a context vector.

$$
d_t = f_\text{dec}(y_{t-1}, d_{t-1}, c_t)
$$

The initial decoder state $d_0$ is typically initialized as a function of the final encoder state (e.g., $d_0 = \tanh(W e_n)$).

The decoder state $d_t$ is then passed through a fully connected (linear) layer to produce a vector of **logits** (unnormalized scores), one for each word in the **fixed output vocabulary**.

$$
\mathbf{o}_t = W_o d_t + b_o
$$

Here, $\mathbf{o}_t$ is a vector of length $\|V\|$, where $V$ is the output vocabulary.

These logits are passed through a softmax function to convert them into a probability distribution. This distribution represents the model's belief about the next word.

$$
P(\text{next word} = w_i) = \frac{\exp(o^i_t)}{\sum_{j=1}^{|V|} \exp(o^j_t)}
$$

The result is a vector $\mathbf{p}_t$ where each element $p^i_t$ is the probability of the $i$-th word in the vocabulary being the next output $y_t$.

The final output $y_t$ is chosen from this distribution.

$$
y_t = \arg \max_i (p^i_t)
$$

The newly generated output $y_t$ is fed back as the input for the next time step $t+1$. The cycle repeats until the decoder generates a special **`<END>`** (or end-of-sequence) token, signifying that the output sequence is complete.

### 3. The Pointer Mechanism: Attention as Output

This is the core innovation. Instead of using the decoder state to predict a token from a fixed vocabulary, it is used to point back to the input sequence.

**Step 1: Calculate Unnormalized Attention Scores (Logits)**

For each decoder step $t$, we compute a score $u^i_t$ for every input element $i$. This score measures the compatibility between the current decoder state $d_t$ and the encoder state $e_i$.

$$
u^i_t = v^T \tanh(W_1 e_i + W_2 d_t) \quad \in \mathbb{R}
$$

Here, $v$, $W_1$, and $W_2$ are learnable parameters. $u^i_t$ is a scalar score for the $i$-th input element at decoding time $t$. We compute this for all $i \in \{1, \dots, n\}$, resulting in a vector $\mathbf{u}_t = (u^1_t, u^2_t, \dots, u^n_t)$.

**Step 2: Normalize Scores into a Pointer Distribution**

The scores $\mathbf{u}_t$ are passed through a softmax function to produce a probability distribution over the input positions. This distribution $\mathbf{a}_t$ is the output of the pointer.

$$
a^i_t = \frac{\exp(u^i_t)}{\sum_{j=1}^{n} \exp(u^j_t)} \quad \text{for } i = 1, \dots, n
$$

$$
\mathbf{a}_t = (a^1_t, a^2_t, \dots, a^n_t) \quad \text{where } \sum_{i=1}^n a^i_t = 1
$$

**Step 3: Generate the Output**

The predicted output $y_t$ is the input element with the highest probability under this distribution. This is an argmax operation.

$$
y_t = \arg \max_i (a^i_t)
$$

The entire model is trained end-to-end by minimizing the negative log-likelihood of the true pointer locations. For a target sequence $(y^\*_1, \dots, y^\*_m)$, the loss at each step is $-\log a^{i^\*}_t$, where $i^\*$ is the index of the true input element $y^\*_t$.

**Crucial Difference from Standard Seq2Seq:** In a standard model, the attention distribution $\mathbf{a}_t$ is used to compute a **context vector**

$$
c_t = \sum_{i=1}^n a^i_t e_i
$$,

which is then fed into a softmax output layer over a fixed vocabulary. In a Pointer Network, the distribution $\mathbf{a}_t$ **is** the final output, and no context vector is used for vocabulary generation.
