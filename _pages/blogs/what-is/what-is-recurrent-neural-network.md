---
title: What is Recurrent Neural Network
permalink: /blogs/what-is-recurrent-neural-network
medium: blog
category: what-is
---

## 🔍 Overview

An RNN, or Recurrent Neural Network, is a type of artificial neural network designed for processing sequential data—data where the order matters, like time series, text, or speech.

## 🔬 Key Concepts

- Memory of previous inputs: Unlike traditional neural networks, RNNs have loops that allow information to persist. This means they can "remember" previous inputs in the sequence, which is crucial for tasks like language modeling or predicting stock prices.
- Shared weights: The same weights are applied at each time step, making RNNs efficient and suitable for variable-length input sequences.
- Time-step processing: RNNs process one element of the sequence at a time, updating their internal state (or "memory") with each new input.

## 🧠 Applications

- Natural Language Processing (NLP): Text generation, sentiment analysis, machine translation.
- Speech Recognition
- Time Series Forecasting
- Music Generation

## ⚠️ Limitations:

- Vanishing and exploding gradients: RNNs can struggle with long sequences due to difficulty in learning long-term dependencies.
- Training complexity: They can be harder to train compared to other architectures.

## 🧬 Variants:

To address some of the limitations, more advanced versions of RNNs have been developed:
- LSTM (Long Short-Term Memory): Designed to remember information for long periods.
- GRU (Gated Recurrent Unit): A simpler alternative to LSTM with similar performance.

---

## 🧑‍💻 Example Code

### 1. Input at Time Step t
At each time step $$t$$, the RNN receives:
- The current input $$x_t$$ (e.g., a word or a feature vector)
- The previous hidden state $$h_{t-1}$$

### 2. Hidden State Update
The RNN updates its hidden state using a function like:

$$
h_t = \tanh(W_{xh} \cdot x_t + W_{hh} \cdot h_{t-1} + b_h)
$$

Where:
- $$W_{xh}$$ and $$W_{hh}$$ are weight matrices
- $$b_h$$ is a bias term
- $$\tanh$$ is an activation function

This new hidden state $$h_t$$ now contains information from both the current input and the past.

### 3. Output (Optional)
Depending on the task, the RNN may produce an output at each time step:

$$
y_t = W_{hy} \cdot h_t + b_y
$$

---

### 🔄 Example: Sentiment Analysis
For a sentence like "I love coding":
- The RNN reads "I" → updates hidden state
- Then "love" → updates hidden state again
- Then "coding" → final hidden state reflects the whole sentence
- The final output might be a sentiment score (positive/negative)

---
