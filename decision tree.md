# 🌳 Decision Tree Classifier

A **Decision Tree** is a supervised machine learning algorithm used for **classification** and **regression** tasks. It splits the data into branches to make decisions based on certain features — like a **flowchart**, where each node represents a decision rule on a feature, and each **leaf node** represents an outcome (class label). 🧠📊

---

## 🧩 Key Concepts in Decision Trees:

- **🌱 Root Node**: Represents the entire dataset and splits into two or more branches.
- **🔀 Decision Node**: A node that splits further based on a condition.
- **🍃 Leaf Node**: A terminal node that holds a class label (final decision).
- **🌿 Branches**: Represent the outcome of a decision and connect nodes.
- **✂️ Splitting**: The process of dividing nodes into sub-nodes based on features.

---

## 📏 Criteria for Splitting:

To split the dataset effectively, we use statistical measures such as:

- 📘 **Information Gain**
- ⚖️ **Gini Index**
- 📊 **Gain Ratio**

# 🧠 ID3 Algorithm – Theoretical Explanation

**ID3 (Iterative Dichotomiser 3)** is an algorithm introduced by Ross Quinlan, used to generate a decision tree. It uses **Information Gain** as the splitting criterion. 🌳

---

## 🔁 Steps of the ID3 Algorithm:

### 1️⃣ Start at the Root Node:
- Take the **whole training dataset** as input.

### 2️⃣ Calculate Entropy for the Dataset:
- Entropy measures the **impurity** or **uncertainty** in the dataset. 🎲

#### 🔢 Formula:

$Entropy(S) = - \sum_{i=1}^{c} p_i \log_2(p_i)$

Where:
- $( p_i )$ is the **proportion** of class ( i ) in set ( S ).
- ( c ) is the number of classes.

---

### 3️⃣ Calculate Information Gain for Each Attribute:
- **Information Gain** measures the **reduction in entropy** after the dataset is split on an attribute. 📉

#### 🔢 Formula:

$Gain(S, A) = Entropy(S) - \sum_{v \in Values(A)} \frac{|S_v|}{|S|} \cdot Entropy(S_v)$

Where:
- \( Values(A) \) are the possible values of attribute \( A \).
- $( S_v )$ is the subset of \( S \) where attribute \( A = v \).

---

### 4️⃣ Choose the Attribute with the Highest Information Gain:
- This becomes the **decision node**. 🌐
- Create **branches** for each possible value of the chosen attribute.

---

### 5️⃣ Repeat the Process Recursively:
- For each branch (subset of data), **repeat** the process with the **remaining attributes**. 🔄

---

### 🛑 Stop When:
- ✅ All attributes are used.
- ✅ All data in the subset belong to the **same class**.
- ✅ The dataset is **empty** (in this case, assign the **majority class** of the parent node).

---

🔍 The ID3 algorithm is a fundamental building block in understanding how decision trees are constructed and why they work the way they do.

## 📌 Summary:

- **Decision Tree Classifier**:  
  A model that makes decisions by **splitting data** into subsets using **conditional rules**.

- **ID3 Algorithm**:  
  Builds decision trees using **Entropy** and **Information Gain** to select the **best attribute** at each step.

---
# Example-01
# 🌤️ Weather Dataset

| 📅 Day | 🌥️ Outlook  | 🌡️ Temperature | 💧 Humidity | 💨 Wind   | 🎾 PlayTennis |
|-------:|:-----------:|:--------------:|:-----------:|:--------:|:-------------:|
| D1     | Sunny       | Hot            | High        | Weak     | No            |
| D2     | Sunny       | Hot            | High        | Strong   | No            |
| D3     | Overcast    | Hot            | High        | Weak     | Yes           |
| D4     | Rain        | Mild           | High        | Weak     | Yes           |
| D5     | Rain        | Cool           | Normal      | Weak     | Yes           |
| D6     | Rain        | Cool           | Normal      | Strong   | No            |
| D7     | Overcast    | Cool           | Normal      | Strong   | Yes           |
| D8     | Sunny       | Mild           | High        | Weak     | No            |
| D9     | Sunny       | Cool           | Normal      | Weak     | Yes           |
| D10    | Rain        | Mild           | Normal      | Weak     | Yes           |
| D11    | Sunny       | Mild           | Normal      | Strong   | Yes           |
| D12    | Overcast    | Mild           | High        | Strong   | Yes           |
| D13    | Overcast    | Hot            | Normal      | Weak     | Yes           |
| D14    | Rain        | Mild           | High        | Strong   | No            |

## 🔶 Step 1: Calculate Entropy of Target (🎾 PlayTennis)

We have:
- ✅ "Yes" = 9  
- ❌ "No" = 5  

### 🧮 Entropy Formula:
$Entropy(S) = -p_+ \log_2(p_+) - p_- \log_2(p_-)$

Where:
- $( p_+ = \frac{9}{14} \approx 0.643 )$
- $( p_- = \frac{5}{14} \approx 0.357 )$

### 🔢 Substituting Values:
$Entropy(S) = -0.643 \cdot \log_2(0.643) - 0.357 \cdot \log_2(0.357)$

### 🧠 Final Answer:
$Entropy(S) \approx 0.940$

## 🔶 **Step 2: Calculate Information Gain for Each Attribute**

### 🅰️ Outlook

- **Sunny** → [D1, D2, D8, D9, D11] → 5 samples → ✅ 2 Yes, ❌ 3 No  
- **Overcast** → [D3, D7, D12, D13] → 4 samples → ✅ 4 Yes, ❌ 0 No  
- **Rain** → [D4, D5, D6, D10, D14] → 5 samples → ✅ 3 Yes, ❌ 2 No

---

📌 **Formula:**  
`Gain(S, Outlook) = Entropy(S) - ∑ (|Sᵥ| / |S|) * Entropy(Sᵥ)`

---

🔸 **Entropy of subsets:**

- **Sunny:**  
  `Entropy = −(2/5)log₂(2/5) − (3/5)log₂(3/5) ≈ 0.971`

- **Overcast:**  
  All "Yes" → `Entropy = 0`

- **Rain:**  
  `Entropy = −(3/5)log₂(3/5) − (2/5)log₂(2/5) ≈ 0.971`

---

🔸 **Information Gain (Outlook):**  
`Gain(Outlook) = 0.940 − [(5/14 × 0.971) + (4/14 × 0) + (5/14 × 0.971)]`  
`= 0.940 − (0.347 + 0 + 0.347)`  
`= 0.940 − 0.694`  
🎯 `= 0.246`


### 🟠 B. Temperature

- **Hot** → [D1, D2, D3, D13] → 4 samples → ✅ 2 Yes, ❌ 2 No  
  ➤ Entropy = **1.0**

- **Mild** → [D4, D8, D10, D11, D12, D14] → 6 samples → ✅ 4 Yes, ❌ 2 No  
  ➤ Entropy =  
  $-\frac{4}{6} \log_2\left(\frac{4}{6}\right) - \frac{2}{6} \log_2\left(\frac{2}{6}\right) ≈ 0.918$

- **Cool** → [D5, D6, D7, D9] → 4 samples → ✅ 3 Yes, ❌ 1 No  
  ➤ Entropy =  
  $-\frac{3}{4} \log_2\left(\frac{3}{4}\right) - \frac{1}{4} \log_2\left(\frac{1}{4}\right) ≈ 0.811$

---

🔸 **Information Gain (Temperature):** 

$\text{Gain(Temperature)} = 0.940 - \left( \frac{4}{14} \cdot 1.0 + \frac{6}{14} \cdot 0.918 + \frac{4}{14} \cdot 0.811 \right)$

$= 0.940 - (0.286 + 0.393 + 0.232)$

$= 0.940 - 0.911 = \boxed{0.029}$

### 🌫️ C. Humidity

- **High** → [D1, D2, D3, D4, D8, D12, D14] → 7 samples → ✅ 3 Yes, ❌ 4 No  
  ➤ Entropy =  
  $-\frac{3}{7} \log_2\left(\frac{3}{7}\right) - \frac{4}{7} \log_2\left(\frac{4}{7}\right) ≈ 0.985$

- **Normal** → [D5, D6, D7, D9, D10, D11, D13] → 7 samples → ✅ 6 Yes, ❌ 1 No  
  ➤ Entropy =  
  $-\frac{6}{7} \log_2\left(\frac{6}{7}\right) - \frac{1}{7} \log_2\left(\frac{1}{7}\right) ≈ 0.591$

---

🔸 **Information Gain (Humidity):** 

$\text{Gain(Humidity)} = 0.940 - \left( \frac{7}{14} \cdot 0.985 + \frac{7}{14} \cdot 0.591 \right)$

$= 0.940 - (0.492 + 0.296)$

$= 0.940 - 0.788 = \boxed{0.152}$

### 🌬️ D. Wind

- **Weak** → [D1, D3, D4, D5, D8, D9, D10] → 7 samples → ✅ 6 Yes, ❌ 1 No  
  ➤ Entropy =  
  $-\frac{6}{7} \log_2\left(\frac{6}{7}\right) - \frac{1}{7} \log_2\left(\frac{1}{7}\right) ≈ 0.591$

- **Strong** → [D2, D6, D7, D11, D12, D13, D14] → 7 samples → ✅ 3 Yes, ❌ 4 No  
  ➤ Entropy =  
  $-\frac{3}{7} \log_2\left(\frac{3}{7}\right) - \frac{4}{7} \log_2\left(\frac{4}{7}\right) ≈ 0.985$

---

🔸 **Information Gain (Wind):** 

$\text{Gain(Wind)} = 0.940 - \left( \frac{7}{14} \cdot 0.591 + \frac{7}{14} \cdot 0.985 \right)$

$= 0.940 - (0.296 + 0.492)$

$= 0.940 - 0.788 = \boxed{0.152}$

### 🔶 **Best Attribute to Split On:**

✅ **Outlook** has the highest information gain of **0.246**, so it is the best attribute to split on.

---
📊 **Decision:**
The first node of the decision tree will be based on the **Outlook** attribute, as it provides the most useful split in terms of Information Gain.



