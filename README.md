# Word2Vec on Dialogue Data

This project explores **Word2Vec word embeddings** using a dialogue-based corpus from the TV series **Friends**.  
The goal is to examine how different training choices affect the semantic relationships learned by the model.

The project was developed as part of a university NLP assignment and focuses on:

* preprocessing a custom text corpus
* training Word2Vec models with **Gensim**
* exploring learned embeddings through common semantic tests
* comparing the effect of different parameter settings

## Project Overview

Two Word2Vec models were trained on the same preprocessed dialogue corpus:

### Model 1 — CBOW

* **Architecture:** CBOW (`sg=0`)
* `vector_size=100`
* `window=10`
* `min_count=2`
* `epochs=10`
* negative sampling enabled (`negative=5`)

### Model 2 — Skip-gram

* **Architecture:** Skip-gram (`sg=1`)
* `vector_size=200`
* `window=5`
* `min_count=3`
* `epochs=10`
* negative sampling enabled (`negative=5`)

After training, the models were explored using:

* **most similar words** — e.g. `most_similar('rachel', topn=10)`
* **word similarity scores** — e.g. cosine similarity between *ross–rachel* and *monica–chandler*
* **odd-one-out detection** — e.g. `doesnt_match(['ross', 'rachel', 'joey', 'milk'])`
* **analogy-style queries** — e.g. `most_similar(positive=['rachel', 'monica'], negative=['joey'])`

## Dataset

The corpus used in this project is a **Friends dialogue dataset** sourced from **Kaggle**.

This repository does **not** include the dataset file itself.  
To run the notebook, download the dataset from Kaggle and upload the text file when prompted in Google Colab.

> Note: The notebook keeps the original workflow used in the assignment, including the way the dataset is loaded.

## Preprocessing

The corpus was preprocessed using standard text-cleaning steps:

* sentence tokenization via `sent_tokenize`
* lowercasing and word tokenization via `simple_preprocess`
* stopword removal (English stopwords via NLTK)
* filtering of punctuation and non-alphabetic symbols

The result is a cleaned list of tokenized sentences used as input for Word2Vec training.

## Main Findings

### CBOW (Model 1) — broad character associations

With `window=10` and `vector_size=100`, CBOW captured **wide co-occurrence patterns** across sentences.  
The nearest neighbors of words like *rachel* were predominantly other main characters (*ross*, *monica*, *joey*, *chandler*, *phoebe*), reflecting the model's tendency to group words that appear in similar narrative contexts rather than similar local contexts.

Similarity scores also reflected known relationships in the show:

| Word Pair | Cosine Similarity |
|---|---|
| *ross* – *rachel* | higher |
| *monica* – *chandler* | higher |

The `doesnt_match` queries returned expected outliers:
- `['ross', 'rachel', 'joey', 'milk']` → **milk** (not a character name)
- `['joey', 'phoebe', 'chandler', 'hair']` → **hair** (not a character name)

### Skip-gram (Model 2) — local conversational context

With `window=5` and `vector_size=200`, Skip-gram shifted toward **local, context-sensitive patterns**.  
Instead of mainly returning character names, the nearest neighbors of the same words included terms related to emotions, conversational states, and speaking style — reflecting the model's focus on what words appear *close together* in dialogue rather than broadly across the corpus.

This contrast is a direct result of the architecture difference:
- **CBOW** predicts a word from its surrounding context → learns what words share similar contexts
- **Skip-gram** predicts context from a word → learns fine-grained local usage patterns

### Effect of corpus domain

The dialogue-based nature of the corpus influences results in a notable way: because Friends dialogue is dominated by character names and conversational phrases, the embeddings reflect that distribution. Some semantic relations that would appear in a larger general-purpose corpus (e.g. standard semantic analogies) are harder to capture here. This is expected and instructive — it illustrates how corpus domain shapes what a model can and cannot learn.

## Files

* `Word2Vec_Friends.ipynb` — main notebook with preprocessing, training, experiments, and conclusions
* `requirements.txt` — required Python packages

## How to Run

1. Open the notebook in Google Colab.
2. Install the required packages if needed:

```bash
pip install -r requirements.txt

## Skills Demonstrated

* NLP preprocessing (tokenization, stopword removal, corpus cleaning)
* Word embeddings with Gensim (CBOW and Skip-gram)
* Parameter tuning and architectural comparison
* Semantic evaluation: similarity scores, odd-one-out, analogy queries
* Analysis of how training choices and corpus domain shape model behaviour

## Notes

This project is intended as a **learning and portfolio project** in Applied NLP / Computational Linguistics.  
It focuses on experimentation and interpretation rather than production deployment.

A natural next step would be adding a **t-SNE or UMAP visualization** of the learned embeddings to make the semantic clusters visible — this is planned as a future addition.
