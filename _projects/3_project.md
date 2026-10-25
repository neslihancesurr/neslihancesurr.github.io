---
layout: page
title: FrameNet Semantic Frame Classification
description: Sentence embedding-based semantic frame retrieval for Turkish lexical concepts using English FrameNet
img: assets/img/framenet_classification.jpg
importance: 2
category: work
related_publications: false
---

This Python project explores **semantic frame identification for Turkish lexical concepts** by matching Turkish synsets and definitions to English semantic frames from [FrameNet](https://framenet.icsi.berkeley.edu/).

**[View the Project on GitHub](https://github.com/neslihancesurr/framenet_classification)**

Unlike traditional classification approaches that require a dedicated classifier, this project uses **sentence embeddings and semantic similarity** to retrieve candidate frames. It embeds English FrameNet frame definitions and translated Turkish lexical entries into a shared vector space, then ranks frames according to their semantic similarity to each query.

## Embedding Models

The project implements two sentence embedding models from [Sentence Transformers](https://www.sbert.net/):

- **MiniLM (`all-MiniLM-L6-v2`):** A lightweight model for efficient semantic similarity search.
- **MPNet (`all-mpnet-base-v2`):** An alternative embedding model for comparing retrieval results.

Both models are used to identify candidate frames for each input record, allowing their ranked predictions to be compared.

## Input Format

The file-prediction scripts expect a JSON array containing Turkish lexical entries and their English translations. Each record includes the fields `synset_english` and `definition_english`, which are combined to form the semantic search query.

For example:

```json
{
  "synset_english": "run",
  "definition_english": "To move swiftly on foot."
}
```

The system compares this query against the embedded FrameNet frame definitions to identify semantically related frames.

## Semantic Retrieval & Prediction

The prediction scripts calculate semantic similarity between the query embedding and the precomputed FrameNet frame embeddings.

1. **Frame Embedding:** FrameNet frame definitions are encoded using a selected Sentence Transformer model.
2. **Query Representation:** The English synset and definition are combined and converted into an embedding.
3. **Similarity Ranking:** Candidate frames are ranked by semantic similarity to the query.
4. **Candidate Generation:** The file-prediction scripts return the top 10 candidate frames for each record, while the interactive terminal interface returns the top five candidates for a user-provided phrase or sentence.

The resulting predictions are stored in JSON format, preserving the original input records alongside the ranked frame candidates.

## Interactive Search

The project also provides an interactive terminal interface through `prediction_terminal.py`, allowing users to explore FrameNet without preparing an input file.

```bash
python prediction_terminal.py
```

Enter an English phrase or sentence to retrieve the five most semantically similar FrameNet frames. Type `exit` or `quit` to terminate the session.

## Technologies

**Python · Sentence Transformers · MiniLM · MPNet · PyTorch · FrameNet · Semantic Similarity · Sentence Embeddings**

The project investigates how embedding-based retrieval can support **semi-automatic semantic frame annotation** by leveraging English semantic resources for Turkish lexical-semantic analysis. The retrieved frames serve as candidate annotations for further examination rather than definitive predictions validated against gold-standard labels.
