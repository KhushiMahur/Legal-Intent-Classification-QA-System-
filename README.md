# Legal Intent Classification & QA System

A question-answering system for legal queries across three domains: **IPC, CrPC, and the Constitution**.

The system first identifies the legal domain of a user's question using a fine-tuned BERT classifier. It then retrieves a relevant answer from the corresponding legal dataset using sentence embeddings and cosine similarity. Finally, the retrieved context is passed to TinyLlama to generate a concise natural-language response.

---

## 🧠 Project Overview

The system follows a three-stage pipeline:

```text
User Question
      ↓
Legal Domain Classification
      ↓
BERT Classifier
      ↓
IPC / CrPC / Constitution
      ↓
Semantic Retrieval
      ↓
Sentence-BERT Embeddings + Cosine Similarity
      ↓
Relevant Legal Context
      ↓
TinyLlama
      ↓
Generated Answer
```
This approach combines **classification, semantic retrieval, and generative AI** to create a legal question-answering prototype.

---

## 📂 Legal Domains

The system works with three legal domains:

- **IPC** – Indian Penal Code
- **CrPC** – Code of Criminal Procedure
- **Constitution** – Constitutional law-related queries

The datasets are combined and labelled according to their respective domain before training the classifier.

---

## 🤖 Model Architecture

### 1. Legal Intent / Domain Classification

A pretrained **BERT (`bert-base-uncased`)** model is fine-tuned to classify incoming questions into one of the three legal domains.

The training process includes:

- Tokenization using the BERT tokenizer
- Train/test split
- Class-weighted loss to account for differences in class distribution
- Fine-tuning of BERT for sequence classification

---

### 2. Semantic Retrieval

After identifying the legal domain, the system searches the corresponding dataset for a relevant answer.

The retrieval process uses:

- **Sentence Transformer:** `all-MiniLM-L6-v2`
- Sentence embeddings
- **Cosine similarity** for comparing the user's question with stored questions

The answer associated with the most semantically similar question is selected as the retrieved context.

---

### 3. Answer Generation

The retrieved legal context is provided to:

**TinyLlama 1.1B Chat**

The model generates a concise response based on the retrieved context.

This allows the system to combine retrieval of existing legal information with natural-language answer generation.

---

## 🛠️ Technologies Used

- Python
- PyTorch
- Hugging Face Transformers
- BERT
- Sentence Transformers
- TinyLlama
- Pandas
- NumPy
- Scikit-learn

---

## 📁 Project Structure

```text
Legal-Intent-Classification-QA/
│
├── legal_chatbot.ipynb
└── README.md
```
The notebook contains the complete workflow, including:

- Dataset preparation
- Domain labelling
- BERT fine-tuning
- Semantic retrieval
- TinyLlama-based response generation
- Sample question testing

---

## 🚀 How It Works

1. A user enters a legal question.
2. BERT predicts whether the question belongs to IPC, CrPC, or Constitution.
3. The corresponding legal dataset is selected.
4. The question and stored questions are converted into sentence embeddings.
5. Cosine similarity is used to retrieve the most relevant legal answer.
6. The retrieved context is passed to TinyLlama.
7. TinyLlama generates the final response.

---

## 🧪 Testing

The chatbot was tested using sample questions from all three supported legal domains.

The test questions cover:

- IPC-related queries
- CrPC-related queries
- Constitutional queries

The system displays the generated response along with the similarity score associated with the retrieved result.

---

## 🔍 Limitations

This project is a prototype for educational and experimental purposes.

- The system retrieves answers from the available datasets and does not independently verify legal information.
- The current implementation does not provide formal end-to-end evaluation metrics for retrieval or generated responses.
- Model loading and embedding computation can be optimized for repeated queries.
- The system should not be treated as a substitute for professional legal advice.

---

## 🎯 Objective

The objective of this project is to explore how **NLP, semantic retrieval, and generative AI** can be combined to build a domain-specific question-answering system for legal queries.
