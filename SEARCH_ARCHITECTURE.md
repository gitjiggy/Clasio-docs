# Clasio Search Architecture - "Answers First"™

**Version**: 5.0 (March 2026)

> **Note (March 2026):** This document was updated to reflect the March 2026 search overhaul. The 6-tier sequential waterfall was replaced by parallel keyword + semantic search, and Ask Clasio was added for deep document Q&A. For the full technical reference, see `docs/search/ARCHITECTURE_CURRENT.md` in the main repository.

> This document describes Clasio's consciousness-first search architecture at a conceptual level.

---

## Table of Contents
1. [Vision & Philosophy](#vision--philosophy)
2. [Architecture Overview](#architecture-overview)
3. [Parallel Search + Ask Clasio](#parallel-search--ask-clasio)
4. [Intent-Based Routing](#intent-based-routing)
5. [Document Consciousness Framework](#document-consciousness-framework)
6. [Performance & Optimization](#performance--optimization)
7. [Search Idempotency](#search-idempotency)
8. [Quality Assurance](#quality-assurance)

---

## Vision & Philosophy

### The "Answers First" Approach

Users should get **direct answers** to questions, not lists of documents to search through.

**Traditional search**:
- User: "Where's my tax form?"
- System: *Shows 12 files*
- User: *Opens each one looking for EIN*

**Clasio**:
- User: "What's my EIN?"
- System: "12-3456789" *(Source: 2024_Tax_Return.pdf, 98% confidence)*

### Core Principles

1. **Answer First, Always**: Direct answer in the first line
2. **Source Attribution**: Every answer links to source document
3. **Confidence Transparency**: Users see how certain we are
4. **Idempotent Results**: Same query = same answer, every time
5. **Sub-2s Response**: 95% of queries complete in <2 seconds

---

## Architecture Overview

### Two-Phase Search Stack

```
┌──────────────────────────────────────┐
│   QUERY PREPROCESSING                │
│   - Conversational pattern stripping │
│   - Possessive detection             │
│   - Gemini preprocessor (on retry)   │
│   - Dimension classification         │
└──────────────────────────────────────┘
              ↓
┌──────────────────────────────────────┐
│   PHASE 1: PARALLEL SEARCH           │
│                                      │
│   ┌──────────┐  ┌──────────────┐    │
│   │ Keyword  │  │ Semantic     │    │
│   │ (11 SQL  │  │ (pgvector    │    │
│   │  fields) │  │  cosine)     │    │
│   └────┬─────┘  └──────┬──────┘    │
│        └──────┬─────────┘           │
│        Dynamic Merge + Score         │
└──────────────────────────────────────┘
              ↓
┌──────────────────────────────────────┐
│   INTENT-BASED ROUTING               │
│   - 10 specialized resolvers         │
│   - Resolver hint fast-path          │
│   - Dimension pre-filter             │
│   - Pattern matching fallback        │
└──────────────────────────────────────┘
              ↓
┌──────────────────────────────────────┐
│   CONSCIOUSNESS EXTRACTION CASCADE   │
│   - Structured attribute extraction  │
│   - Key Q&A matching (lexical+sem.)  │
│   - Instant answer matching          │
│   - Content snippet extraction       │
│   (All from pre-computed data, 0 API │
│    calls)                            │
└──────────────────────────────────────┘
              ↓
┌──────────────────────────────────────┐
│   PHASE 2: ASK CLASIO (conditional) │
│   - Fires when confidence < 50%     │
│   - Sends doc content to Gemini     │
│   - Verified answer replaces weak   │
│     consciousness answer             │
└──────────────────────────────────────┘
              ↓
┌──────────────────────────────────────┐
│   DATA PERSISTENCE LAYER             │
│   - PostgreSQL + pgvector            │
│   - 7 denormalized search fields     │
│   - HNSW indexes for vectors         │
│   - B-tree + GIN for keywords        │
└──────────────────────────────────────┘
```

### Key Components

**Parallel Search Service**
- Runs keyword and semantic search simultaneously
- Dynamic weighting based on match strength (strong keyword matches suppress semantic path)
- Trigram fallback for typos when keyword search returns nothing
- Max-based scoring per field (prevents weak matches from outscoring strong ones)

**Consciousness Extraction Cascade**
- Extracts direct answers from pre-computed 6D metadata without any API calls
- Tries structured attributes first, then key Q&A, then instant answers, then content snippets
- Confidence thresholds gate each extraction method

**Ask Clasio**
- Progressive enhancement on the frontend; fires only when consciousness answers are weak
- Sends document content directly to Gemini (temperature 0 for deterministic output)
- Also available as "Ask This Document" inside the document detail modal
- Supports cross-document queries via document hints

**Resolver Registry**
- Central routing system for query types
- Priority-based resolver selection with hint fast-path
- Dimension pre-filter skips mismatched resolvers
- 10 specialized resolvers from aggregation to compliance

**Data Gateway**
- Abstraction over persistence layer
- Lightweight field projection (50x payload reduction)
- Content enrichment for top results only
- Result caching with TTL management

---

## Parallel Search + Ask Clasio

Search runs in two phases. Phase one (parallel search) finds documents and extracts answers from pre-computed consciousness data. Phase two (Ask Clasio) fires conditionally when phase one's answer is weak, sending document content directly to Gemini for a verified answer.

### Phase 1: Parallel Search

Keyword and semantic search run simultaneously against consciousness metadata and embeddings.

**Keyword search** tests the query against 11 fields (consciousness identity fields, 7 denormalized search columns, filenames) using ILIKE and PostgreSQL word boundary regex. Scoring is max-based: each document gets the score of its single best matching field, which prevents documents with many weak matches from outranking one strong match.

**Semantic search** generates a query embedding and runs pgvector cosine similarity against `summaryEmbeddingV` (768-dim). It is skipped entirely when the top keyword hit scores above 0.8, since a strong keyword match means the right document is already found. A 3-second timeout prevents slow embedding calls from blocking results.

**Dynamic merge scoring** combines the two result sets. When keyword matches are strong (normalized score >= 0.50), keyword gets 55% weight and semantic gets 25%. When keyword matches are weak, the weights flip. An exact-match boost of 0.10 is added when the match comes from consciousness identity fields (docType, docTitle).

**Trigram fallback**: When keyword search returns zero results, `pg_trgm similarity()` provides fuzzy matching for typos and near-misses.

### Phase 2: Ask Clasio

When the consciousness extraction cascade produces a low-confidence answer (below 50%) on a question query, the frontend automatically fires Ask Clasio. This sends the top document's content (plus up to 4 related documents identified by hints) directly to Gemini at temperature 0.

If the Gemini answer has confidence above 50%, it replaces the weak consciousness answer in the UI with a "Verified Answer" badge. If it fails, the original consciousness answer remains.

Ask Clasio is also available as "Ask This Document" inside the document detail modal for user-initiated questions.

### Consciousness Extraction Cascade

Before Ask Clasio fires (or instead of it, when consciousness confidence is sufficient), direct answers are extracted from pre-computed 6D metadata with zero API calls:

1. **Structured attribute extraction**: For identifier, date, or monetary queries, searches consciousness structured fields.
2. **Key Q&A matching**: Searches pre-computed question/answer pairs. Tries lexical matching first (50% term overlap), falls back to semantic similarity (0.75 threshold).
3. **Instant answer matching**: Same approach against instant answer fields.
4. **Content snippet extraction**: Regex search against document content, extracting a 120-character window around the match.

---


## Document Consciousness Framework

### 6-Dimensional Intelligence

Every document is analyzed across 6 fundamental dimensions:

**1. WHAT (Content & Facts)**
- Document type classification
- Key entities and facts
- Structured field extraction
- Topic identification

**2. WHO (People & Relationships)**
- Individuals mentioned
- Organizations involved
- Relationship mapping
- Contact information

**3. WHEN (Dates & Deadlines)**
- Critical dates extraction
- Deadline detection
- Timeline analysis
- Expiration tracking

**4. WHERE (Location & Jurisdiction)**
- Geographic locations
- Jurisdiction identification
- Coverage areas
- Address extraction

**5. WHY (Purpose & Obligations)**
- Document purpose
- Obligations identification
- Intent analysis
- Action items

**6. HOW (Processes & Procedures)**
- Process documentation
- Procedure extraction
- Step-by-step instructions
- Method descriptions

### Universal Field Extraction

No rigid schemas. The AI extracts ANY labeled field from ANY document type:
- Driver license numbers
- GST IDs, EINs, SSNs
- Policy numbers
- Account numbers
- Custom fields unique to document types we've never seen

**Future-proof**: Works on documents the system has never encountered before.

### Domain Knowledge Integration

1,128 curated terms across 10 categories enable smart query expansion:

**Categories**:
- Tax & Compliance (1040, 1099, W-2, Schedule A, etc.)
- Medical & Health (CPT codes, prescriptions, lab tests)
- Legal & Contracts (NDA, settlement, jurisdiction)
- Financial & Accounting (invoice, ledger, P&L)
- Real Estate (deed, mortgage, escrow)
- Travel & Immigration (passport, visa, I-94)
- Education (transcript, diploma, GPA)
- Employment (offer letter, benefits, W-2)
- Insurance (policy, claim, deductible)
- Corporate & Business (stock options, SEC filings)

**How it works**:
- Query: "tax documents"
- Expands to include: "1040", "1099", "W-2", "irs", "schedule", "deduction"
- Finds all tax-related documents even without exact phrase match

---

## Performance & Optimization

### Database Optimizations

**Denormalized Search Fields**
- 7 indexed columns extracted from consciousness data
- Eliminates runtime JSON parsing overhead
- Enables fast multi-field weighted queries
- B-tree indexes for exact match, GIN for full-text search

**Lightweight Projections**
- Exclude heavy embedding fields by default (50x payload reduction)
- Fetch content only for top N results (two-phase enrichment)
- Reduces query latency and network overhead

**Connection Pooling**
- Optimized pool sizing for serverless environment
- Automatic scaling (2-40 connections)
- Statement timeouts prevent blocking
- Connection leak detection

### Caching Strategy

**Multi-Layer Caching**:
- **L1 (In-Memory)**: Hot queries with LRU eviction
- **L2 (Query Embeddings)**: Long-lived (1-year TTL)
- **L3 (Result Cache)**: User-scoped with automatic invalidation

**Cache Invalidation**:
- Document updates invalidate user-specific result caches
- Smart TTL management (embeddings: 1 year, results: 5 minutes)
- Query fingerprinting for consistent cache keys

### Query Optimization

**Bounded Operations**:
- Limit term expansion to prevent SQL overload
- Filter meaningless terms (too short)
- Stable candidate pools for consistent scoring

**Batch Processing**:
- Minimize database roundtrips
- Parallel processing where possible
- Async queue for heavy AI operations

---

## Search Idempotency

Same query = same result. Every time. No variance.

### Four Pillars

**1. Deterministic Ordering**
- Stable tiebreakers when scores are equal
- Consistent sort order across all rankings
- Document ID as secondary sort key

**2. Consistent Data Fetching**
- Explicit ordering on all database queries
- No undefined row ordering
- Alphabetical or timestamp-based sorts

**3. Stable Candidate Pools**
- Consistent number of candidates for scoring
- Large enough pools to prevent boundary variance
- Reproducible search spaces

**4. Long-Lived Caching**
- Extended TTL prevents re-computation variance
- 1-year cache for embeddings
- Eliminates temporal inconsistency

---

## Quality Assurance

### Multi-Factor Scoring

Search results combine multiple signals:
- **Semantic similarity** (vector embeddings)
- **Lexical match** (keyword presence)
- **Quality signals** (metadata completeness)
- **Freshness** (recency boost)
- **User feedback** (historical accuracy)

### Confidence Calibration

Confidence scores map to user-facing tiers:
- **90%+**: Very High (green)
- **75-89%**: High (blue)
- **60-74%**: Medium (yellow)
- **30-59%**: Low (orange)
- **<30%**: Very Low (red)

### Hallucination Prevention

**Grounding Verification**:
- Answer text must appear in source document
- Key phrases cross-referenced with source content
- Low grounding score = confidence penalty

**Source Attribution**:
- Every answer includes source document reference
- Users can click through to verify
- Transparency builds trust

### Testing & Validation

**Golden Query Suite**:
- 50-100 queries with known correct answers
- Automated regression testing before deployments
- Latency and accuracy monitoring
- Drift detection for result stability

**User Feedback Loop**:
- Track click-through rates per resolver
- Measure user satisfaction (thumbs up/down)
- Analyze which answers users trust
- Continuous improvement based on real usage

---

## Evolution & Roadmap

### Current State (V5.0)
- Parallel keyword + semantic search with dynamic merge scoring
- Ask Clasio for deep document Q&A (progressive enhancement)
- Consciousness extraction cascade (structured attributes, key Q&A, instant answers, snippets)
- 10 specialized resolvers with hint fast-path, dimension pre-filter, and pattern matching
- Gemini query preprocessor for typo correction and intent classification (on retry)
- Universal field extraction (no type constraints)
- Search idempotency (deterministic results)
- 50 golden query test suite with quality grading

### Future Enhancements
- Enhanced proactive intelligence
- Cross-document synthesis
- Advanced relationship mapping
- Multi-user collaborative features
- Voice-first query interface
- Compliance automation (HIPAA, SOX, etc.)

---

## Learn More

For a deeper technical dive, see our **[README](./README.md)** or visit **[clasio.ai/docs](https://clasio.ai/docs)** 

---

**© 2025-2026 Clasio. All rights reserved.**
