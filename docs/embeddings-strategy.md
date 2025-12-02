# Embedding Strategies V1

## Overview 
This section outlines the initial strategy used to generate, store, organize, and maintain vector embeddings for legal documents within the system. The objective is to ensure high-quality semantic representations while maintaining consistency, extensibility, and operational reliability across the ingestion and retrieval pipelines.

## Coverage
1. Model Choices

- Primary model: amazon.titan-embed-text-v2
Selected for its performance, multilingual capabilities, and stability.

- Batching:
Embeddings are generated in batched requests to optimize throughput and reduce API overhead.

- Dimensionality:
Determined by the embedding model (baseline Titan dimensions used in V1).

- Normalization:
Embeddings are L2-normalized before storage to ensure vector distance stability across different databases and search methods.

2. Metadata Stored With Embeddings
Each embedding vector include structured metadata for indexing, retrieval, filtering, and auditing
- id - unique vector identifier
- article -article number (if applicable)
- chunk_id -chunk identifier from the chunking service
- year -publication or enactment year
- jurisdiction -geographic or governmental scope
metadata follows the same contract used in the chunking pipeline

3. Vector Database Options
V1 supports multiple vector storage backends:
- pgvector - Postgres-native vector storage, suitable for structured queries + embeddings
- Chroma - Lightweight, fast vector store for expermientation and loscal workflows (use in production still in dicussion)

4. Upser Strategy & Namespace Usage
- Upsert Behavior :
Existing vectors for the same chunk_id are replaced in case of reprocessing migration.
- Namespaces:
A separate namespace is assigned per law/year to ensure isolation, traceability, and compatibility with future versioned embeddings.
- Example: [ley_ingresos_amealco_2025]

This structure supports multi-jurisdictional ingestion without colissions.

5. Embeding Versioning & Migration Plan
- Versioning
Every embedding batch is tagged with an embedding_version to ensure backward compatibility
- Migration
A structured migration workflow is defined:
    1- Generate embeddings with the new version
    2- Store them in a parallel namespace
    3- Validate retrieval quality throught benchmark queries
    4- Promote new version to production namespace
    5- Deprecate old vectors
    
This ensures safe, traceable upgrades as the system evolves.