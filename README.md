# Graph-Analysis-on-Text-Data
NLP and graph analysis on text data, including: extracting entities from text using NLP; building a graph using relationships between entities; computing graph metrics; visualizing ego graphs; and performing entity resolution using fuzzy matching.

## # NLP-Driven Text Graph Analysis & Entity Resolution

This repository features an end-to-end Python pipeline that applies Natural Language Processing (NLP) and Network Analysis to unstructured text data. The system automatically extracts named entities, models their co-occurrence relationships as a weighted network graph, calculates advanced graph metrics, and implements fuzzy string matching for entity resolution.

---

## 🚀 Key Features & Learning Outcomes

*   **Named Entity Recognition (NER):** Extracted key entities from raw text documents utilizing `nltk` chunking structures.
*   **Graph Network Modeling:** Built a directional/undirectional graph model using `networkx`, translating concurrent entity mentions into weighted edges.
*   **Network Topology & Centrality:** Evaluated structural significance across nodes utilizing Degree, Betweenness, and Closeness Centrality measures.
*   **Fuzzy Entity Resolution:** Leveraged string similarity via `fuzzywuzzy` to group and resolve naming variations or abbreviations across text datasets.
*   **Sub-network Visualization:** Visualized specific Ego Graphs alongside full structural network layouts via `matplotlib`.

---

## 🛠️ Tech Stack & Libraries

*   **Language:** Python 3.x
*   **NLP Processing:** `nltk` (word_tokenize, pos_tag, ne_chunk)
*   **Network Analysis:** `networkx`
*   **Visualization:** `matplotlib`
*   **String Matching:** `fuzzywuzzy` / `Levenshtein`
*   **Pipeline Framework:** `scikit-learn` (`BaseEstimator`, `TransformerMixin`)

---

## 📋 Pipeline Architecture

The workflow is constructed via custom, modular Scikit-Learn transformers to ensure reproducibility:

1.  **`EntityExtractor`:** Tokenizes, tags parts-of-speech (POS), and chunks text to filter for specific named entities (e.g., `PERSON`, `GPE`).
2.  **`EntityPairs`:** Utilizes `itertools.permutations` to compute structural pairs representing contextual connections within single document entries.
3.  **`GraphExtractor`:** Initializes a `networkx.Graph()`, mapping unique entities to nodes and incrementing edge weights based on repeated concurrent associations.

---

## 💻 Code Snippet: Advanced Logic Modifications

### 1. Target Entity POS Filtering
Filters text strictly for `PERSON` and geographic/location (`GPE`) entities:
```python
if isinstance(chunk, Tree) and chunk.label() in ["PERSON", "GPE"]:
    entities.append(" ".join([token for token, pos in chunk.leaves()]))
