# Word2Vec on Dialogue Data

This project explores **Word2Vec word embeddings** using a dialogue-based corpus from the TV series **Friends**.  
The goal is to examine how different training choices affect the semantic relationships learned by the model.

The project was developed as part of a university NLP assignment and focuses on:

- preprocessing a custom text corpus
- training Word2Vec models with **Gensim**
- exploring learned embeddings through common semantic tests
- comparing the effect of different parameter settings

## Project Overview

Two Word2Vec models were trained on the same preprocessed dialogue corpus:

### Model 1
- **Architecture:** CBOW
- `vector_size=100`
- `window=10`
- `min_count=2`
- `epochs=10`
- negative sampling enabled

### Model 2
- **Architecture:** Skip-gram
- `vector_size=200`
- `window=5`
- `min_count=3`
- `epochs=10`
- negative sampling enabled

After training, the models were explored using:

- **most similar words**
- **word similarity scores**
- **odd-one-out detection**
- **analogy-style queries**

## Dataset

The corpus used in this project is a **Friends dialogue dataset** sourced from **Kaggle**.

This repository does **not** include the dataset file itself.  
To run the notebook, download the dataset from Kaggle and place the text file locally before execution.

> Note: The notebook keeps the original workflow used in the assignment, including the way the dataset is loaded.

## Preprocessing

The corpus was preprocessed using standard text-cleaning steps:

- sentence tokenization
- lowercasing
- tokenization into words
- stopword removal
- filtering of punctuation and non-alphabetic symbols

The result is a cleaned list of tokenized sentences used as input for Word2Vec training.

## Main Findings

The experiments show that parameter choices affect the kinds of semantic relationships captured by the embeddings.

- The **CBOW** model produced broader and more general associations between words and character names.
- The **Skip-gram** model captured more local and context-sensitive relationships, especially in conversational patterns.
- The quality of some semantic relations was influenced by the size and nature of the dialogue corpus.

Overall, the project demonstrates how Word2Vec can learn meaningful word associations even from a relatively focused conversational dataset.

## Files

- `Word2Vec_Friends.ipynb` — main notebook with preprocessing, training, experiments, and conclusions
- `word2vec_friends.py` — Python version of the notebook
- `requirements.txt` — required Python packages

## How to Run

### Option 1: Run in Google Colab
1. Open the notebook in Colab.
2. Upload the dataset file when prompted.
3. Run the cells in order.

### Option 2: Run locally
1. Create and activate a virtual environment.
2. Install the dependencies:

```bash
pip install -r requirements.txt
```

3. Open the notebook with Jupyter or run the Python script.

## Skills Demonstrated

- NLP preprocessing
- Word embeddings with Gensim
- parameter tuning and comparison
- exploratory semantic evaluation
- analysis of model behavior

## Notes

This project is intended as a **learning and portfolio project** in Applied NLP / Computational Linguistics.  
It focuses on experimentation and interpretation rather than production deployment.
