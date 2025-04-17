# 🧠 Naive Bayes Sentiment Analysis — Step-by-Step with Preprocessing (Imbalanced Dataset)

---

## ✅ Outline

We'll walk through the following steps:

1. **Dataset Setup (Imbalanced)**
2. **Text Preprocessing**
   - Lowercasing
   - Removing punctuation
   - Removing stopwords
   - Tokenization
3. **Vocabulary Creation**
4. **Word Frequency Calculation per Class**
5. **Calculate Prior Probabilities**
6. **Apply Naive Bayes Formula**
7. **Make Prediction**

---

## 1. 📊 Dataset Setup (Imbalanced)

| Sentence                                 | Sentiment |
|------------------------------------------|-----------|
| I loved the visuals and the direction    | Positive  |
| The movie was heartwarming and sweet     | Positive  |
| A wonderful and delightful experience    | Positive  |
| It had charming characters and great music | Positive |
| The story was dull and boring            | Negative  |
| I hated the plot and the acting          | Negative  |

✅ Total: 6 sentences  
- Positive = 4  
- Negative = 2

---

## 2. 🧹 Text Preprocessing

### 🔧 Preprocessing Includes:
- Convert to **lowercase**
- **Remove punctuation**
- Remove **stopwords**
- Tokenize into **words**

### 🛑 Stopword List:
`["i", "the", "and", "was", "it", "had"]`

---

### ✅ Preprocessed Training Sentences

#### Positive:
1. `loved visuals direction`  
2. `movie heartwarming sweet`  
3. `wonderful delightful experience`  
4. `charming characters great music`

→ Positive Words =  
`["loved", "visuals", "direction", "movie", "heartwarming", "sweet", "wonderful", "delightful", "experience", "charming", "characters", "great", "music"]`  
🔢 Total = 13 words

#### Negative:
1. `story dull boring`  
2. `hated plot acting`

→ Negative Words =  
`["story", "dull", "boring", "hated", "plot", "acting"]`  
🔢 Total = 6 words

---

### 🎯 Test Sentence

**Original:** `"I loved the movie but the story was boring"`  
**Preprocessed:** `["loved", "movie", "story", "boring"]`

---

## 3. 📚 Vocabulary

All unique words:

```
["loved", "visuals", "direction", "movie", "heartwarming", "sweet", "wonderful", "delightful", 
 "experience", "charming", "characters", "great", "music", "story", "dull", "boring", "hated", 
 "plot", "acting"]
```

📦 Vocabulary size = **19**

---

## 4. 🔢 Word Frequencies

| Word        | Positive Count | Negative Count |
|-------------|----------------|----------------|
| loved       | 1              | 0              |
| visuals     | 1              | 0              |
| direction   | 1              | 0              |
| movie       | 1              | 0              |
| heartwarming| 1              | 0              |
| sweet       | 1              | 0              |
| wonderful   | 1              | 0              |
| delightful  | 1              | 0              |
| experience  | 1              | 0              |
| charming    | 1              | 0              |
| characters  | 1              | 0              |
| great       | 1              | 0              |
| music       | 1              | 0              |
| story       | 0              | 1              |
| dull        | 0              | 1              |
| boring      | 0              | 1              |
| hated       | 0              | 1              |
| plot        | 0              | 1              |
| acting      | 0              | 1              |

---

## 5. 📏 Prior Probabilities

- P(Positive) = 4/6 = **0.6667**
- P(Negative) = 2/6 = **0.3333**

---

## 6. 📐 Apply Naive Bayes Formula (with Laplace Smoothing)

Formula:

```
P(w|class) = (count(w) + 1) / (total_words_in_class + |V|)
```

---

### 🔹 Positive Class

- Total words = 13  
- Vocabulary size = 19  
- Denominator = 13 + 19 = 32

Test words: `["loved", "movie", "story", "boring"]`

| Word    | Count | P(w\|Positive) |
|---------|--------|---------------|
| loved   | 1      | 2/32  
| movie   | 1      | 2/32  
| story   | 0      | 1/32  
| boring  | 0      | 1/32  

```
P(X|Positive) = (2/32) × (2/32) × (1/32) × (1/32) = 4 / 1048576 ≈ 3.81 × 10⁻⁶
P(Positive | X) = P(X | Positive) × P(Positive)  
                = (2/32 × 2/32 × 1/32 × 1/32) × 0.6667  
                = (4 / 1048576) × 0.6667  
                ≈ 3.81 × 10⁻⁶ × 0.6667  
                ≈ 2.54 × 10⁻⁶
```

---

### 🔻 Negative Class

- Total words = 6  
- Denominator = 6 + 19 = 25

Test words: `["loved", "movie", "story", "boring"]`

| Word    | Count | P(w|Negative) |
|---------|--------|---------------|
| loved   | 0      | 1/25  
| movie   | 0      | 1/25  
| story   | 1      | 2/25  
| boring  | 1      | 2/25  

```
P(X|Negative) = (1/25) × (1/25) × (2/25) × (2/25) = 4 / 390625 ≈ 1.02 × 10⁻⁵
P(Negative | X) = P(X | Negative) × P(Negative)  
                = (4 / 390625) × 0.3333  
                ≈ 1.02 × 10⁻⁵ × 0.3333  
                ≈ 3.41 × 10⁻⁶

```

---

## ✅ 7. Final Prediction

| Sentiment | Posterior Probability |
|-----------|------------------------|
| Positive  | ≈ 2.54 × 10⁻⁶          |
| Negative  | ≈ 3.41 × 10⁻⁶ ✅        |

### ✅ Final Result: **Negative**

Even though the dataset had more positive sentences, the test sentence had strong negative indicators like “story” and “boring” which were **never seen in positive class** — so Naive Bayes leaned negative.

---

## 📝 Summary Table

| Step              | Action                                               |
|-------------------|-----------------------------------------------------|
| Preprocessing     | Lowercase, remove punctuation/stopwords, tokenize   |
| Vocabulary        | Extracted from training set                         |
| Frequencies       | Count words in each class                           |
| Priors            | Based on class distribution                         |
| Naive Bayes       | With Laplace smoothing                              |
| Prediction        | Posterior probabilities determine final class       |

---



# ❓ Why Use Laplace Smoothing Instead of Just Bayes’ Theorem?

---

## 📘 What Is Bayes’ Theorem?

Bayes' Theorem is the **core formula** used in Naive Bayes classification:

$
P(C_k \mid X) = \frac{P(X \mid C_k) \cdot P(C_k)}{P(X)}
$

Where:
- \( P(C_k \mid X) \) is the **posterior** probability of class \( C_k \) given input \( X \)
- \( P(X \mid C_k) \) is the **likelihood** of observing \( X \) given class \( C_k \)
- \( P(C_k) \) is the **prior** probability of class \( C_k \)
- \( P(X) \) is the probability of input \( X \) (same across all classes)

---

## 🧠 How Naive Bayes Uses It

In text classification:

$
P(X \mid C_k) = P(w_1 \mid C_k) \cdot P(w_2 \mid C_k) \cdot \ldots \cdot P(w_n \mid C_k)
$

We multiply the probabilities of all words \( w_1, w_2, \dots, w_n \) in the sentence.

---

## ❌ The Problem: Zero Probability

Let’s say the test sentence contains a word that **never appeared** in class \( C_k \):

Example:
- Word **"awesome"** appears in a test sentence
- It never occurred in **Negative** training examples

Then:
$
P(\text{"awesome"} \mid \text{Negative}) = 0
$

So:
$
P(X \mid \text{Negative}) = 0
\Rightarrow P(\text{Negative} \mid X) = 0
$

**Even if all other words strongly support the Negative class, the entire probability becomes zero!**

---

## ✅ The Solution: Laplace Smoothing

To fix this, we apply **Laplace Smoothing** (also called **Add-One Smoothing**):

$
P(w_i \mid C_k) = \frac{\text{count}(w_i \text{ in class}) + 1}{\text{total words in class} + |V|}
$

Where:
- \( |V| \) is the **vocabulary size** (total unique words across all classes)

This means:
- Every word has **at least a small non-zero probability**
- Even **unseen words** are assigned a small probability

---

## 📝 Summary Table

| Concept                 | Explanation                                                                 |
|-------------------------|-----------------------------------------------------------------------------|
| Bayes’ Theorem          | Calculates posterior using prior and likelihood                            |
| Why smoothing?          | Avoids multiplying by zero when a word doesn’t exist in training data       |
| Laplace Smoothing       | Adds 1 to each word count so unseen words still have small probability      |
| Impact                  | Makes Naive Bayes **robust** to new/unseen words in test data               |

---

## 💬 Teaching Tip

You can demonstrate this with a small example:

- Train one class with: `["happy", "smile"]`
- Test with: `["happy", "awesome"]`

Without smoothing → result = 0  
With smoothing → result > 0

