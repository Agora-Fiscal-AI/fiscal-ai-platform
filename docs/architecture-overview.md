# Architecture Overview V1

Goal: Provide an auditable, treaceable and scalable pipeline for processing fiscal legislation and related documents to feed RAG/LLM analyses.

## Main Components:
- Ingestion Service: PDF/DOCX/HTML/XML extraction & normalization.
- Document Store: raw + normalized artifacts (AWS S3).
- Chunking Service: semantic + sliding window chunk generation.
- Embedding Service: Bedrock / Titan embeddings -> Vector DataBase.
- Vectorestore & Database Service: PostgreSQL + pgvector 
- LLMs Service: Planning to use QWeen 271B LLM.
- RAG Engine: Retriever, re-ranker, LLM orchestation.

# Future reqs:
- Auditable logs.
- User Interface.
- DevOps implementation.
