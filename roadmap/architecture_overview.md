´´´psql
┌────────────────────────────┐
│        INGESTA             │
│────────────────────────────│
│ • PDF / DOCX / XML         │
│ • Fuentes oficiales        │
└─────────────┬──────────────┘
              │
              ▼
┌────────────────────────────┐
│   EXTRACCIÓN Y LIMPIEZA    │
│────────────────────────────│
│ • OCR / parsing            │
│ • Normalización textual    │
│ • Eliminación de ruido     │
└─────────────┬──────────────┘
              │
              ▼
┌────────────────────────────┐
│  NORMALIZACIÓN JURÍDICA    │
│────────────────────────────│
│ • Detección estructura     │
│ • Construcción NormNodes   │
│ • Árbol normativo lógico   │
└─────────────┬──────────────┘
              │
              ▼
┌────────────────────────────┐
│   JSON CANÓNICO            │
│────────────────────────────│
│ • Contenido normativo      │
│ • Semántica pura           │
│ • Sin gobernanza técnica   │
└─────────────┬──────────────┘
              │
              ▼
┌────────────────────────────┐
│        CHUNKING             │
│────────────────────────────│
│ • Basado en semántica      │
│ • 1 o varios NormNodes     │
│ • Preserva contexto legal  │
└─────────────┬──────────────┘
              │
              ▼
┌────────────────────────────┐
│  VECTOR + SQL GOVERNANCE   │
│────────────────────────────│
│ • law_chunks (PostgreSQL)  │
│ • metadata (JSONB)         │
│ • embeddings (pgvector)    │
│ • versionado de chunks     │
└─────────────┬──────────────┘
              │
              ▼
┌────────────────────────────┐
│      RAG / CONSULTA        │
│────────────────────────────│
│ • Similarity search        │
│ • Recuperación semántica   │
│ • Respuesta trazable       │
└────────────────────────────┘





