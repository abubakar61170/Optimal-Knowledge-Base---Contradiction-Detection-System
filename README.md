# Knowledge Base Contradiction and Redundancy Detection

This project implements a system to build and validate a knowledge base by detecting contradictions and redundancies. It is based on the [DIALFACT framework](https://aclanthology.org/2022.acl-long.263/) for evidence retrieval and NLI validation.

## Features

* **Contradiction Detection**: Uses a `KnowledgeGraph` to find semantically similar claims and a `NLIValidator` (using `roberta-large-mnli`) to verify contradictions.
* **Redundancy Detection**: Uses high-threshold cosine similarity (via `all-MiniLM-L6-v2`) to find duplicate or semantically identical claims.
* **Synthetic Contradiction Generation**: Includes a module to generate and validate new contradictory statements for testing and data augmentation.
* **Evidence-Based**: Implements an `EvidenceRetriever` to find supporting sentences for claims from a large corpus (e.g., Wikipedia).

## How It Works

The system is built from several key components:

* **`Utility`**: A helper class to centralize common functionalities like loading the spaCy model and extracting entities.
* **`KnowledgeGraph`**: The core data structure that stores claims as nodes and relationships as edges. It also manages claim embeddings.
* **`EvidenceRetriever`**: Loads a subset of Wikipedia, builds an index, and retrieves relevant sentences as evidence for new claims.
* **`NLIValidator`**: Uses a `roberta-large-mnli` model to perform Natural Language Inference (NLI) to confirm if two statements are a `contradiction`.
* **`SyntheticContradictionGenerator`**: Creates new, negated versions of claims and validates them using the `NLIValidator`.


## Usage

All steps are contained within the `hard_RI.ipynb` notebook.

1.  Open the notebook in Jupyter or Google Colab.
2.  Run the cells from top to bottom.
3.  The script will:
    * Load all models (this may take a few minutes on the first run).
    * Load and index a small slice of the Wikipedia dataset.
    * Process and add 9 example claims to the knowledge graph.
    * Detect and print redundancies.
    * Detect and print NLI-validated contradictions.
    * Generate and print a synthetic contradiction.

    * Save the final graph to `output/knowledge_graph.json`.
