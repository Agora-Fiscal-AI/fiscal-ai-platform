# Rag Architecture V1

## Overflow
This section provides a high-level description of the Retrieval-Augmented Generation (RAG) architecture implemented in the system. The goal is to ensure accurate, traceable, and context-aware responses by combining vector-based retrieval, structured filtering, reranking, context assembly, and controlled LLM generation.

## RAG Pipeline Components

1. Retriever
- Performs Approximate Nearest Neighbor (ANN) vector search over the selected vector store
- Applies metadata filtering (e.g., jurisdiction, year, article number, document ID) to ensure domain-relevant retrieval
- Supports multi-namespace querying where applicable

2. Reranker
- Optional secondary ranking layer for enhanced precision.
- Can utilize:
- A lightweight transformer-based reranker (cross-encoder style), or
- Lexical re-ranking methods(BM25 Algorithm, keyword scoring) for hybrid retrieval
- Ensures that the final context passed to the LLM prioritizes semantic relevance and factual alignment.

3. Context builder
- Assembles the final prompt context snet to the LLM.
- Implements:
- Token budget management to prevent exceding model limits
- Chunk selection strategy based on relevance score references directly into the context 
Ensures that the LLM receives structured and clean evidence

4. LLM Connector
- Integration layer built using LangChain with an AWS Bedrock wrapper
- Provides:
- Consistent invocation interface
- Model selection abstraction
- Retry logic, timeouts, and throughput controls
- Supports multiple Bedrock-hosted models as the system evolves

5. Response Template & Provenance
- All generated outputs follow a controled response template ensuring:
- Clear citations, referencing chunk IDs and/or S3 resource links
- Separation between retrieved context and generated reasoning
- Deterministic formatting for downstream evaluation or audit modules.
Provenance metadata is retained to support traceability and legal compliance.

6. Guardrails
The system incorporates protective layers to ensure safe and compliant generation:
- Maximum generation lenght to control verbosity
- Refusal and safety rules for unsupported or disallowed queries
- PII sanitization to prevent exposure of sensitive information. (in case)
These guardrails maintain reliability, auditability, and ethical compliance.


