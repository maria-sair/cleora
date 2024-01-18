---
Title: Cleora Embeddings Features
Weight: 10
---

## Key technical features of Cleora embeddings

The embeddings produced by Cleora differ significantly from those produced by systems like Node2vec, Word2vec, DeepWalk, and others. 
They are characterized by several key properties characterized by
 several key properties:

- **Efficiency** - Cleora is two orders of magnitude faster than Node2Vec or DeepWalk.
- **Inductivity** - Cleora's embeddings of an entity are defined only by interactions with other entities, allowing vectors for new entities to be computed on-the-fly.
- **Stability** - All starting vectors for entities are deterministic, meaning, that Cleora embeddings on similar datasets will be similar. Methods like Word2vec, Node2vec, or DeepWalk yield different results with each run.
- **Cross-dataset compositionality** - Due to the stability of Cleora embeddings, embeddings of the same entity on multiple datasets can be combined by averaging, yielding meaningful vectors.
- **Dim-wise independence** - The process producing Cleora embeddings ensures that every dimension is independent of others. This allows for an efficient and low-parameter method for combining multi-view embeddings with Conv1d layers.
- **Extreme parallelism and performance** - Cleora is written in Rust, utilizing thread-level parallelism for all calculations except input file loading, often making the embedding process faster than loading the input data.

## Key usability features of Cleora embeddings

The technical properties described above translate into excellent production-readiness of Cleora, which, from an end-user perspective, can be summarized as follows:

- Heterogeneous relational tables can be embedded without any artificial data pre-processing.
- Mixed interaction + text datasets can be embedded easily.
- The cold start problem for new entities is non-existent.
- Real-time updates of the embeddings do not require any separate solutions.
- Multi-view embeddings work out of the box.
- Temporal, incremental embeddings are stable out of the box, with no need for re-alignment, rotations, or other methods.
- Extremely large datasets are supported and can be embedded within seconds/minutes.

