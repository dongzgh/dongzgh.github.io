---
title: What is Transformer Network
permalink: /blogs/what-is-transformer-network
medium: blog
category: what-is
---

## 🔍 Overview

The Transformer Network is a deep learning architecture designed to handle sequential data without relying on recurrence or convolution. Introduced in 2017, it uses self-attention mechanisms to model relationships between all elements in a sequence simultaneously, making it highly parallelizable and effective for tasks like translation, summarization, and text generation.

---

## 🏗️ Architecture

A standard Transformer consists of two main components:

- Encoder: Processes the input sequence and generates contextual representations.
- Decoder: Generates the output sequence, using encoder outputs and previously generated tokens.

Each component is built from stacked layers of:
- Multi-head self-attention
- Feedforward neural networks
- Residual connections and layer normalization

---

## 🔬 Key Concepts

- Token Embedding: Text is tokenized and converted into dense vectors using an embedding layer.
- Positional Encoding: Since Transformers lack recurrence, positional encodings are added to embeddings to provide information about token order.
- Multi-Head Attention: Allows the model to attend to different parts of the sequence in parallel, capturing various types of relationships.
- Feedforward Layers: Each token’s representation is passed through a small neural network to refine its features.

---

## 💡 Training and Prediction

- Training: The model is trained using cross-entropy loss to predict the next token in a sequence or the entire output sequence.
- Inference: The decoder generates tokens one-by-one, using previously generated tokens as input.

---

## 🧠 Applications

### ✅ Sequence-to-Class Tasks (Encoder-only)
- Sentiment analysis
- Text classification
- Named entity recognition

### 🔁 Sequence-to-Sequence Tasks (Encoder-Decoder)
- Machine translation
- Text summarization
- Question answering
- Code generation

---

## 🧑‍💻 Example Code

### 1. Setup

```python
import torch
import torch.nn as nn
import torch.nn.functional as F

# Sample vocabulary and tokenized sentences
vocab = {'<pad>': 0, 'I': 1, 'love': 2, 'AI': 3, 'and': 4, 'coding': 5}
inv_vocab = {v: k for k, v in vocab.items()}
vocab_size = len(vocab)

# Example input: "I love AI"
input_ids = torch.tensor([[1, 2, 3]])  # shape: (batch_size=1, seq_len=3)
```

### 2. Transformer Model

```python
class MiniTransformer(nn.Module):
    def __init__(self, vocab_size, d_model=32, nhead=4, num_layers=2):
        super().__init__()
        self.embedding = nn.Embedding(vocab_size, d_model)
        self.pos_encoding = nn.Parameter(torch.randn(1, 100, d_model))
        encoder_layer = nn.TransformerEncoderLayer(d_model=d_model, nhead=nhead)
        self.encoder = nn.TransformerEncoder(encoder_layer, num_layers=num_layers)
        self.fc_out = nn.Linear(d_model, vocab_size)

    def forward(self, x):
        x = self.embedding(x) + self.pos_encoding[:, :x.size(1), :]
        x = x.permute(1, 0, 2)  # Transformer expects (seq_len, batch, d_model)
        encoded = self.encoder(x)
        out = self.fc_out(encoded)
        return out.permute(1, 0, 2)  # Back to (batch, seq_len, vocab_size)

model = MiniTransformer(vocab_size)
```

### 3. Run the Model

```python
output = model(input_ids) # Output predicts the next word probability
predicted_token = torch.argmax(output[0, -1])  # Get prediction for next word
print(f"Predicted next word: {inv_vocab[predicted_token.item()]}")
```

---

### 🧠 What’s Happening

- The model takes the input sequence `"I love AI"` and tries to predict the next word.
- It uses embeddings, positional encoding, and Transformer layers to process the sequence.
- The final output is a probability distribution over the vocabulary for each position.
- We take the last position’s output and pick the most likely next word.
