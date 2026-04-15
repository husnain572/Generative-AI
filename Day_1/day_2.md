
# Data Representation & Vectorization

## Why do we need Vectorization?

Machines **cannot understand text directly**.

So we convert text into:

> Numbers (Vectors)

This process is called:

> **Text Vectorization**

---

# 1. One-Hot Encoding

## Concept:

Each word is represented as a vector where:

* Only **one position is 1**
* All others are 0

## Example Corpus:

```
I love AI
I love ML
```

### Step 1: Vocabulary creation

Vocabulary =

```
[I, love, AI, ML]
```

### Step 2: One-hot encoding

| Word | Vector    |
| ---- | --------- |
| I    | [1,0,0,0] |
| love | [0,1,0,0] |
| AI   | [0,0,1,0] |
| ML   | [0,0,0,1] |

### Step 3: Sentence representation

“I love AI”
→ [1,1,1,0] (sum of word vectors conceptually)

## Problems with One-Hot Encoding

### 1. Out of Vocabulary (OOV)

If a new word comes:

Example:
Training vocab:

```
[I, love, AI, ML]
```

New sentence:

> “I enjoy DL”

Problem:

* “enjoy” and “DL” not in vocabulary 

Model cannot represent them


### 2. Sparsity Problem

Vectors are mostly zeros.

Example:
[0,0,0,1,0,0,0,0,0,0]

Waste of memory + inefficient

### 3. No Fixed Meaning Relationship

* “king” and “queen” are completely different vectors
* No similarity captured

No semantic understanding

### 4. No Semantic Meaning

Words like:

* “good” and “excellent”

Treated as totally unrelated

## Conclusion:

> One-hot encoding is simple but NOT useful for NLP in real-world AI systems.

---

# 2. Bag of Words (BoW)

## Concept:

BoW counts **how many times each word appears**.

It ignores grammar and order.

## Example Corpus:

```
Doc1: I love AI
Doc2: I love ML
```

### Step 1: Vocabulary

```
[I, love, AI, ML]
```

### Step 2: Word count vectors

| Document | I | love | AI | ML |
| -------- | - | ---- | -- | -- |
| Doc1     | 1 | 1    | 1  | 0  |
| Doc2     | 1 | 1    | 0  | 1  |

## Working Idea:

* Count words
* Create vector based on frequency

## Where BoW Works Well

- Sentiment Analysis
- Spam detection
- Positive/Negative classification

## Example:

Review:

> “This movie is good”

Model learns:

* “good” → positive sentiment

## Drawbacks of Bag of Words

### 1. No Semantic Meaning

* “good” ≠ “excellent” (treated same importance individually)


### 2. Word Order is Lost

* “not good” vs “good not”
* Both same vector

### 3. Large Sparse Matrix

Many zeros → inefficient

### 4. Context Ignorance

* “bank” (river bank vs financial bank) same meaning
---

# 3. TF-IDF (Term Frequency - Inverse Document Frequency)

## Concept:

TF-IDF improves BoW by giving **importance to words**

## Formula:

### TF (Term Frequency):

How often word appears in a document

### IDF (Inverse Document Frequency):

How rare a word is across all documents


## Intuition:

* Common words → less important (“the”, “is”)
* Rare words → more important

## Example:

Corpus:

```
Doc1: AI is good
Doc2: AI is powerful
```

Words like:

* “AI” → appears in both → less unique
* “good”, “powerful” → more important
## Advantages of TF-IDF

- Reduces importance of common words
- Highlights important words
- Better than BoW for ranking tasks

## Limitations

* Still no semantic meaning
* Still no context understanding
* Still sparse vectors

---

# 4. Word2Vec 

## Concept:

Word2Vec converts words into **dense vectors (embeddings)**.

It captures **meaning + relationships**


## Key Idea:

Words used in similar context have similar meaning.

## Example:

Sentence:

* “King is a man”
* “Queen is a woman”

Word2Vec learns:

```
King → vector
Queen → vector
Man → vector
Woman → vector
```

And:

king - man + woman = queen

## Why Word2Vec is Powerful

- Captures semantic meaning
- Dense vectors (not sparse)
- Solves similarity problem



## Example similarity:

| Word Pair        | Similarity |
| ---------------- | ---------- |
| king - queen     | high       |
| car - vehicle    | high       |
| good - excellent | high       |

## Limitations

* Cannot understand full sentence context
* Same word = same vector always

---

# 5. Transformers (Modern AI - GAME CHANGER)


## Concept:

Transformers understand:

> Context of words in a sentence

## Key Innovation:

Unlike Word2Vec:

* Meaning depends on sentence context

## Example:

Word: “bank”

Sentence 1:

> I went to the bank to deposit money
> financial bank

Sentence 2:

> I sat near the river bank
> river bank

## Transformer Advantage:

Same word → different meaning depending on context

## How Transformers work (simple idea):

They use:

* Attention mechanism
* Focus on important words in sentence

## Example:

Sentence:

> “I love AI because it is powerful”

Model focuses on:

* AI
* powerful

# Why Transformers are Best

- Understand context
- Capture semantic meaning
- Handle long sentences
- Power behind GPT, BERT, Gemini

# Evolution Summary 

| Method           | Meaning   | Context | Sparsity | Use             |
| ---------------- | --------- | ------- | -------- | --------------- |
| One Hot Encoding | No      | No    | High   | Not used        |
| Bag of Words     | No      | No    | High   | Basic NLP       |
| TF-IDF           | Partial | No    | High   | Search, ranking |
| Word2Vec         | Yes     |  No    | Dense  | Embeddings      |
| Transformers     | Strong | Yes   | Dense  | Modern LLMs     |

# Final Summary

- Text must be converted into vectors
- Simple methods = One-hot, BoW
- Improved method = TF-IDF
- Semantic understanding = Word2Vec
- Context understanding = Transformers
