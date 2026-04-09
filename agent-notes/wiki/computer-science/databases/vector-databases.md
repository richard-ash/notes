---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/databases/2021-12-23-gentle-intro-vector-databases.md
compiled_at: 2026-04-09
model: claude-opus-4-6
confidence: medium
---

# Vector Databases

A **vector database** is a purpose-built data system for storing, indexing, and querying high-dimensional embedding vectors — the numerical representations that [[llm-knowledge-bases|machine learning models]] produce from unstructured data like text, images, audio, and video.

## Why not a relational database?

Relational databases organize data into rows and columns with rigid schemas. This works well for structured records (names, dates, prices) but breaks down for unstructured content. You cannot write a SQL `WHERE` clause that captures "shoes that look like this photo" or "sentences that mean something similar to this query." The gap between structured queries and unstructured understanding is what embedding models and vector databases bridge together.

## Embedding vectors

Machine learning models convert unstructured inputs into fixed-length floating-point vectors (embeddings) such that **semantically similar inputs map to nearby points** in the vector space. Classic demonstrations include:

- **Word2vec** (2013): word embeddings where vector arithmetic captures semantic relationships — the famous "king" - "man" + "woman" ≈ "queen" example.
- **Image embeddings**: CNNs or vision transformers produce vectors where visually similar images cluster together. Liu demonstrates that two dog images have a Euclidean distance of 0.809 while a dog-to-car pair measures 1.281.

These embeddings are the currency that vector databases store and search over.

## How vector search works

The core operation is **nearest-neighbor search**: given a query vector, find the _k_ vectors in the database closest to it by some distance metric (typically cosine similarity or Euclidean distance). Exact nearest-neighbor search is O(n) and impractical at scale, so vector databases use **approximate nearest neighbor (ANN)** algorithms — trading a small accuracy loss for orders-of-magnitude speedups. Common ANN index types include HNSW (hierarchical navigable small worlds), IVF (inverted file index), and product quantization.

## Production requirements

Liu identifies three pillars for production-grade vector databases:

1. **Scalability** — billions of vectors require horizontal sharding across machines.
2. **Reliability** — replication and fault tolerance to prevent data loss.
3. **Speed** — real-time insertion and query latency for high-throughput applications.

These requirements parallel traditional database concerns but are complicated by the high dimensionality of the data and the computational cost of distance calculations.

## Applications

Vector databases underpin a wide range of modern ML-powered systems:

- **Semantic search** — retrieval based on meaning rather than keyword matching
- **Recommendation systems** — finding similar items or users in embedding space
- **Retrieval-augmented generation (RAG)** — grounding LLM responses in relevant documents retrieved via vector similarity
- **Drug discovery** — searching molecular embedding spaces for candidate compounds
- **Image/audio search** — content-based retrieval without manual tagging

## Temporal notes

This article was published in December 2021, before the LLM explosion of 2023. The vector database landscape has evolved significantly since then:

- **RAG** has become the dominant use case, driven by ChatGPT and enterprise LLM adoption.
- **Pinecone** (closed-source, not mentioned by Liu) became the most prominent managed vector database.
- **pgvector** brought vector search into PostgreSQL, blurring the line between relational and vector databases.
- **Milvus** (recommended by Liu) remains actively developed; **Vespa** and **Weaviate** also grew substantially.
- Debate has emerged over whether purpose-built vector databases are necessary versus vector extensions to existing databases (Postgres, Redis, Elasticsearch).

## Sources

- Liu, Frank (2021). "A Gentle Introduction to Vector Databases." <https://frankzliu.com/blog/a-gentle-introduction-to-vector-databases> — [[2021-12-23-gentle-intro-vector-databases|local copy]]
