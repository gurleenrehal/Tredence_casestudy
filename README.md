# 🚀 Self-Pruning Neural Network  
### Tredence AI Engineering Case Study

![Python](https://img.shields.io/badge/Python-3.10-blue)
![PyTorch](https://img.shields.io/badge/PyTorch-DeepLearning-red)
![Status](https://img.shields.io/badge/Status-Completed-success)
![Model](https://img.shields.io/badge/Model-Self%20Pruning-green)

---

## 📌 Problem Overview

Modern neural networks are often **over-parameterized**, making them inefficient for real-world deployment.

This project implements a **Self-Pruning Neural Network** that learns to **remove unnecessary weights during training itself**, instead of relying on post-training pruning. :contentReference[oaicite:0]{index=0}

---

## 🧠 Core Idea

Each weight is paired with a **learnable gate**:

**W_effective = W × G**

Where:
-**G = sigmoid(gate_scores), G ∈ [0,1]**


| Gate Value | Meaning |
|-----------|--------|
| ≈ 1       | Important connection |
| ≈ 0       | Pruned connection |

---

## ⚙️ Model Architecture

- Input: CIFAR-10 (32×32×3)
- Fully Connected Network:
  - 3072 → 512 → 256 → 10
- Custom Layer: **PrunableLinear**

---

## 📉 Loss Function

**Total Loss = CrossEntropyLoss + λ × SparsityLoss**

### Sparsity Loss:

Sum of all gate values
Encourages gates to move toward zero
---

## ❓ Why L1 Regularization Produces Sparsity

- L1 applies a **constant gradient pressure**
- Pushes values **directly toward zero**
- Unlike L2, it does not weaken near zero
- Forces many gate values → **exactly 0**

👉 This effectively removes weights → **automatic pruning**

---

## 📊 Results

| Lambda | Test Accuracy (%) | Sparsity (%) |
|--------|------------------|--------------|
| 0.0001 |       51.61      |     72.03    |
| 0.001  |       48.23      |     83.25    |
| 0.01   |       38.63      |     85.77     |
---

## 📉 Gate Value Distribution

![Gate Distribution](gate_distribution.png)


### 🔍 Observations

- Extremely large spike at **0**
- Very few values away from 0

### ✅ Interpretation

- Majority of weights are **successfully pruned**
- Only important connections remain active
- Clear evidence of **self-pruning behavior**

---

## 🔄 Sparsity vs Accuracy Trade-off

| λ Increase | Sparsity | Accuracy |
|-----------|---------|----------|
| Low λ     | Low     | High     |
| Medium λ  | Medium  | Balanced |
| High λ    | High    | Lower    |

👉 Demonstrates expected trade-off between **efficiency and performance**

---


## 🚀 Conclusion

This project demonstrates that neural networks can **adaptively learn their own optimal structure**, resulting in:

- Reduced model size  
- Efficient computation  
- Minimal performance degradation  

---

## 👨‍💻 Author

**Gurleen Rehal**



