# Chunking Strategy V1

# Overview
This section outlines the rules and methodologies implemented in the Chunking Service, whose purpose is to optimize text segmentation for high-quality embedding generation and efficient retrieval within the vector store.
The strategy combines semantic, structural, and token-based criteria to ensure meaningful and context-rich chunks.

# Chunking Rules
1. Chunk Size
- Target: ~500 tokens
- Allowed variance: ±100 tokens
- Adjustment depends on document complexity, density, and structural patterns.

2. Overlap
- Sliding window: 50–100 tokens
- Ensures contextual continuity across chunks, improving semantic coherence.

3. Semantic Chunking
Chunks must prioritize logical and legal structure boundaries, splitting content using:
- Headings
- Sections
- Articles
- Sub-articles or subthemes (if applicable) -> in discussion

4. Metadata Propagation
Each chunk must retain and propagate document-level metadata, including:
- Article_number
- Jurisdiction
- Source
- ingested_at

5. Chunk-Level Metadata
- score_stimate - internal quality or relevance estimation
- chunk_id - unique identifier for traceability

# Chunking Example:

{
  "chunk_id": "law-123_article5_chunk_0001",
  "text": "...",
  "tokens": 512,
  "article_number": "5",
  "start_char": 0,
  "end_char": 512,
  "metadata": {
    "jurisdiction": "MX",
    "year": 2025
  }
}



