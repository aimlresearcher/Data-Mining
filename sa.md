# 🧠 Naive Bayes Sentiment Analysis 

## 📝 Outline of Steps

1. 📁 **Define a small dataset**  
   - Include labeled **positive** and **negative** sentences.

2. 🔧 **Preprocess the text**  
   - Convert text to **lowercase**  
   - Remove **stopwords**  
   - Apply **lemmatization**

3. 🧰 **Build the vocabulary**  
   - Create a set of all unique words from the dataset.

4. 📊 **Calculate word frequencies**  
   - Count word occurrences in **positive** and **negative** sentences separately.

5. 🧮 **Apply Laplace smoothing**  
   - Avoid zero probabilities by adding smoothing to frequency counts.

6. 📉 **Calculate prior probabilities**  
   - Compute the probability of each class:  
     $( P(\text{Positive}) )$, $( P(\text{Negative}) )$

7. 📐 **Calculate likelihood**  
   - For a given test sentence, calculate $( P(X \mid \text{class}) )$

8. 🧾 **Compute posterior probabilities**  
   - Use Bayes' Theorem:  
     $( P(\text{class} \mid X) \propto P(\text{class}) \times P(X \mid \text{class}) )$

9. 🏁 **Classify the test sentence**  
   - Choose the class with the **highest posterior probability**

---
## 📊 1. Sample Dataset

Below is a small dataset containing labeled **positive** and **negative** sentences:

| 🆔 | ✏️ Sentence                              | 😊 Sentiment |
|----|------------------------------------------|--------------|
| 1  | I love this amazing movie                | Positive     |
| 2  | What a great and exciting story          | Positive     |
| 3  | I hate this boring movie                 | Negative     |
| 4  | The plot was terrible and slow           | Negative     |
| 5  | It was a horrible experience             | Negative     |

---

## 🧹 2. Preprocessing

### 🔄 Steps:

- 🔡 **Lowercasing**  
- 🧱 **Removing stopwords**  
  *(i, this, and, was, a, it, the, what)*
- 🧬 **Lemmatization**  
  *(Convert words to their base form)*

### ✅ Preprocessed Dataset:

| 🆔 | 📝 Original Sentence                           | 🧹 Preprocessed Tokens         | 😊 Sentiment |
|----|-----------------------------------------------|-------------------------------|--------------|
| 1  | I love this amazing movie                     | love, amazing, movie          | Positive     |
| 2  | What a great and exciting story               | great, exciting, story        | Positive     |
| 3  | I hate this boring movie                      | hate, boring, movie           | Negative     |
| 4  | The plot was terrible and slow                | plot, terrible, slow          | Negative     |
| 5  | It was a horrible experience                  | horrible, experience          | Negative     |

---
## 🗂️ 3. Vocabulary

All unique words across all preprocessed sentences:

$\{love, amazing, movie, great, exciting, story, hate, boring, plot, terrible, slow, horrible, experience\}$


📦 **Vocabulary Size (V)** = **13**

---

## 📈 4. Word Frequencies by Sentiment

| 🧩 Word       | 😊 Count in Positive | 😠 Count in Negative |
|--------------|----------------------|----------------------|
| love         | 1                    | 0                    |
| amazing      | 1                    | 0                    |
| movie        | 1                    | 1                    |
| great        | 1                    | 0                    |
| exciting     | 1                    | 0                    |
| story        | 1                    | 0                    |
| hate         | 0                    | 1                    |
| boring       | 0                    | 1                    |
| plot         | 0                    | 1                    |
| terrible     | 0                    | 1                    |
| slow         | 0                    | 1                    |
| horrible     | 0                    | 1                    |
| experience   | 0                    | 1                    |

🧮 **Total words in Positive class** = **6**  
🧮 **Total words in Negative class** = **9**


---

## 🧮 5. Apply Laplace Smoothing

### 📐 Laplace Smoothing Formula:

$P(w \mid \text{class}) = \frac{\text{count}(w) + 1}{\text{total words in class} + |V|}$

Where:
- `count(w)` = frequency of the word in the given class
- `|V|` = vocabulary size (in our case, **13**)
- `total words in class` = total number of words in that class  
  - Positive = **6**
  - Negative = **9**

---
## ⚖️ 6. Prior Probabilities

To calculate prior probabilities, we use:

- 📊 **Total examples** = 5  
- 😊 **Positive examples** = 2  
- 😠 **Negative examples** = 3  

### 📌 Prior Probability Formula:

$P(\text{Positive}) = \frac{2}{5} = 0.4 \quad , \quad P(\text{Negative}) = \frac{3}{5} = 0.6$

---
## 🧪 7. Test Sentence

### 💬 Original Sentence:
> "Amazing and exciting movie"

### 🧹 After Preprocessing:
$amazing, exciting, movie$

---

## 📊 8. Likelihoods with Laplace Smoothing

We compute the likelihoods $( P(X \mid \text{class}) )$ using the **Laplace smoothing formula** for each word in the test sentence:  
**"amazing, exciting, movie"**

---

### 😊 P(X | Positive):

| 🧩 Word    | 🔢 Count in Positive | 🔍 P(w \| Positive)                             |
|-----------|----------------------|-----------------------------------------------|
| amazing   | 1                    | $( \frac{1+1}{6+13} = \frac{2}{19} \approx 0.105 )$ |
| exciting  | 1                    | $( \frac{2}{19} \approx 0.105 )$             |
| movie     | 1                    | $( \frac{2}{19} \approx 0.105 )$              |

$P(X \mid \text{Positive}) = 0.105 \times 0.105 \times 0.105 \approx 0.001157625$

---

### 😠 P(X | Negative):

| 🧩 Word    | 🔢 Count in Negative | 🔍 P(w \| Negative)                             |
|-----------|----------------------|-----------------------------------------------|
| amazing   | 0                    | $( \frac{0+1}{9+13} = \frac{1}{22} \approx 0.0455 )$ |
| exciting  | 0                    | $( \frac{1}{22} \approx 0.0455 )$             |
| movie     | 1                    | $( \frac{1+1}{22} = \frac{2}{22} \approx 0.0909 )$ |

$P(X \mid \text{Negative}) = 0.0455 \times 0.0455 \times 0.0909 \approx 0.0001883$

---
## 🧠 9. Posterior Probabilities

We use the full formula to calculate posterior probabilities:

### 📐 Formula:
$P(\text{class} \mid X) = P(\text{class}) \times P(X \mid \text{class})$

---

### 😊 Positive Class:

$P(\text{Positive} \mid X) = 0.4 \times 0.001157625 \approx 0.00046305$

---

### 😠 Negative Class:

$P(\text{Negative} \mid X) = 0.6 \times 0.0001883 \approx 0.00011298$

---

### ✅ Final Decision:

Since:

$P(\text{Positive} \mid X) > P(\text{Negative} \mid X)$

🔍 **The test sentence is classified as: `Positive`**

# Example 01
## 🧩 1. Dataset 

| 🆔 | ✏️ Sentence                                      | 😊 Sentiment |
|----|--------------------------------------------------|--------------|
| 1  | The acting was good but not great               | Positive     |
| 2  | I enjoyed the plot and direction                | Positive     |
| 3  | The movie had a boring and slow plot            | Negative     |
| 4  | Poor acting and terrible direction              | Negative     |
| 5  | Good visuals but horrible storyline             | Negative     |

## 🧪 Test Sentence 

### 💬 Original Sentence:
> "Good plot but horrible direction"
---

# Example 02
## 🧾 1. Dataset 

| 🆔 | ✏️ Sentence                                                   | 😊 Sentiment |
|----|---------------------------------------------------------------|--------------|
| 1  | I absolutely loved the movie, it was fantastic                | Positive     |
| 2  | What a great and touching storyline                           | Positive     |
| 3  | The cast delivered an excellent performance                   | Positive     |
| 4  | A beautiful experience with amazing direction                 | Positive     |
| 5  | I hated the film, it was awful and boring                     | Negative     |
| 6  | The acting was weak and the story lacked depth                | Negative     |
| 7  | A dull movie with terrible pacing and bad script              | Negative     |
| 8  | Poor plot and disappointing characters                        | Negative     |

## 🧪 Test Sentence

### 💬 Original Sentence:
> "The film had a great plot but weak acting"


# Example 03
## 🌤️ "Commute Decision"


| 📅 Day | 🌦️ Weather   | 🚗 Traffic | ⏱️ Time   | 🔥 Urgency | 🚶 Commute |
|--------|--------------|------------|-----------|-------------|-------------|
| 1      | Sunny        | Low        | Short     | Low         | Yes         |
| 2      | Rainy        | High       | Long      | High        | No          |
| 3      | Sunny        | Medium     | Medium    | Low         | Yes         |
| 4      | Overcast     | Low        | Short     | Medium      | Yes         |
| 5      | Rainy        | High       | Long      | Medium      | No          |
| 6      | Sunny        | Medium     | Medium    | High        | No          |
| 7      | Overcast     | Low        | Short     | Low         | Yes         |
| 8      | Rainy        | Medium     | Medium    | High        | No          |
| 9      | Overcast     | High       | Long      | Low         | Yes         |
| 10     | Sunny        | Low        | Medium    | Medium      | Yes         |

## 🔍 Classify New Instance

Classify the following **new instance** using the dataset:

### 🆕 New Instance:

| 🌦️ Weather | 🚗 Traffic | ⏱️ Time | 🔥 Urgency |
|------------|------------|--------|------------|
| Sunny      | Medium     | Medium | High       |

---

