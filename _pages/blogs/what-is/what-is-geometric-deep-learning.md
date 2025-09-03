---
title: What is Geometric Deep Learning
permalink: /blogs/what-is-geometric-deep-learning
medium: blog
category: what-is
---

## 🔍 Overview

Geometric Deep Learning (GDL) is a subfield of machine learning that generalizes deep learning methods to non-Euclidean domains, such as graphs, manifolds, and other geometric structures. Traditional deep learning models (like CNNs and RNNs) work well on data with a regular grid-like structure (e.g., images, sequences), but many real-world data types—like social networks, molecules, 3D shapes, and traffic systems—are better represented as graphs or other irregular structures.

## 💡 Core Idea

GDL aims to respect and leverage the underlying geometry of the data. Instead of assuming data lies in flat Euclidean space, it adapts models to work on:

- Graphs (e.g., social networks, molecular structures)
- Manifolds (e.g., surfaces of 3D objects)
- Point clouds (e.g., LiDAR scans)
- Meshes (e.g., 3D models)

## 🔬 Key Concepts

- Graph Neural Networks (GNNs): Learn representations from graph-structured data by aggregating information from neighboring nodes.
- Manifold Learning: Embeds high-dimensional data into lower-dimensional curved spaces.
- Equivariance and Invariance: Models are designed to be invariant or equivariant to transformations like rotation, translation, or permutation.
- Message Passing: A common framework in GNNs where nodes exchange information with neighbors to update their representations.

## 🧠 Applications

- Drug discovery (molecular graphs)
- Recommendation systems (user-item graphs)
- Computer vision (3D shape analysis)
- Physics simulations (particle interactions)
- Autonomous driving (road networks and sensor data)

## 🧑‍💻 Example Code

```python
import torch
import torch.nn.functional as F
from torch_geometric.nn import GCNConv
from torch_geometric.datasets import Planetoid

# Load the Cora dataset (citation network)
dataset = Planetoid(root='/tmp/Cora', name='Cora')
data = dataset[0]  # Cora has only one graphimport torch
import torch.nn.functional as F
from torch_geometric.nn import GCNConv
from torch_geometric.datasets import Planetoid

# Load the Cora dataset (citation network)
dataset = Planetoid(root='/tmp/Cora', name='Cora')
data = dataset[0]  # Cora has only one graph

# Define the GCN model
class GCN(torch.nn.Module):
    def __init__(self):
        super(GCN, self).__init__()
        self.conv1 = GCNConv(dataset.num_node_features, 16)
        self.conv2 = GCNConv(16, dataset.num_classes)

    def forward(self, data):
        x, edge_index = data.x, data.edge_index
        x = self.conv1(x, edge_index)
        x = F.relu(x)
        x = F.dropout(x, training=self.training)
        x = self.conv2(x, edge_index)
        return F.log_softmax(x, dim=1)

# Train the model
device = torch.device('cuda' if torch.cuda.is_available() else 'cpu')
model = GCN().to(device)
data = data.to(device)
optimizer = torch.optim.Adam(model.parameters(), lr=0.01, weight_decay=5e-4)

model.train()
for epoch in range(200):
    optimizer.zero_grad()
    out = model(data)
    loss = F.nll_loss(out[data.train_mask], data.y[data.train_mask])
    loss.backward()
    optimizer.step()

# Evaluate the model
model.eval()
pred = model(data).argmax(dim=1)
correct = (pred[data.test_mask] == data.y[data.test_mask]).sum()
acc int(correct) / int(data.test_mask.sum())
print(f'Accuracy: {acc:.4f}')

# Define the GCN model
class GCN(torch.nn.Module):
    def __init__(self):
        super(GCN, self).__init__()
        self.conv1 = GCNConv(dataset.num_node_features, 16)
        self.conv2 = GCNConv(16, dataset.num_classes)

    def forward(self, data):
        x, edge_index = data.x, data.edge_index
        x = self.conv1(x, edge_index)
        x = F.relu(x)
        x = F.dropout(x, training=self.training)
        x = self.conv2(x, edge_index)
        return F.log_softmax(x, dim=1)

# Train the model
device = torch.device('cuda' if torch.cuda.is_available() else 'cpu')
model = GCN().to(device)
data = data.to(device)
optimizer = torch.optim.Adam(model.parameters(), lr=0.01, weight_decay=5e-4)

model.train()
for epoch in range(200):
    optimizer.zero_grad()
    out = model(data)
    loss = F.nll_loss(out[data.train_mask], data.y[data.train_mask])
    loss.backward()
    optimizer.step()

# Evaluate the model
model.eval()
pred = model(data).argmax(dim=1)
correct = (pred[data.test_mask] == data.y[data.test_mask]).sum()
acc int(correct) / int(data.test_mask.sum())
print(f'Accuracy: {acc:.4f}')
```