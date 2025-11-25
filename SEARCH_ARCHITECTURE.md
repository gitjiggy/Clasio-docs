# Clasio Search Architecture - "Answers First"™

**Version**: 4.3.1 (November 2025)

> This document describes Clasio's consciousness-first search architecture at a conceptual level.

---

## Table of Contents
1. [Vision & Philosophy](#vision--philosophy)
2. [Architecture Overview](#architecture-overview)
3. [6-Tier Consciousness-First Waterfall](#6-tier-consciousness-first-waterfall)
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

### Multi-Layer Intelligence Stack

```
┌──────────────────────────────────────┐
│   QUESTION ANALYZER                  │
│   - Intent detection                 │
│   - Entity extraction                │
│   - Dimension classification         │
│   - Confidence scoring               │
└──────────────────────────────────────┘
              ↓
┌──────────────────────────────────────┐
│   UNIVERSAL CONSCIOUSNESS SEARCH     │
│   - Single 6-tier waterfall          │
│   - AI-extracted metadata priority   │
│   - Pre-searches once per query      │
│   - Passes results to resolvers      │
└──────────────────────────────────────┘
              ↓
┌──────────────────────────────────────┐
│   INTENT-BASED ROUTING               │
│   - 10 specialized resolvers         │
│   - Pattern matching                 │
│   - Priority-based selection         │
│   - Intelligent extraction           │
└──────────────────────────────────────┘
              ↓
┌──────────────────────────────────────┐
│   BUSINESS LOGIC SERVICES            │
│   - Aggregation                      │
│   - Quantitative calculations        │
│   - Relationship mapping             │
│   - Temporal analysis                │
└──────────────────────────────────────┘
              ↓
┌──────────────────────────────────────┐
│   DATA PERSISTENCE LAYER             │
│   - PostgreSQL + pgvector            │
│   - Optimized indexing               │
│   - Caching strategy                 │
│   - Query optimization               │
└──────────────────────────────────────┘
```

### Key Components

**Question Analyzer**
- Detects query intent (WHAT/WHO/WHEN/WHERE/WHY/HOW/HOW_MUCH)
- Extracts entities using pattern matching
- Classifies dimension with confidence scoring
- Meta-query extraction for complex questions

**Universal Consciousness Search**
- Single source of truth for document search
- Executes 6-tier waterfall once per query
- Returns documents with confidence scores
- Eliminates redundant database queries

**Resolver Registry**
- Central routing system for query types
- Priority-based resolver selection
- Domain-aware pattern matching
- Specialized processing pipelines

**Data Gateway**
- Abstraction over persistence layer
- Lightweight field projection (50x payload reduction)
- Content enrichment for top results only
- Result caching with TTL management

---

## 6-Tier Consciousness-First Waterfall

Our search strategy prioritizes AI-extracted metadata (document consciousness) over raw keyword matching.

### What is Document Consciousness?

A 6-dimensional AI-extracted metadata structure capturing document intelligence:

```typescript
Document Consciousness {
  identity: {
    docType: "Invoice" | "Resume" | "Tax Form 1040"
    docTitle: AI-extracted title
  }

  extraction: {
    structuredFields: [
      { label: "EIN", value: "12-3456789", fieldType: "identifier" }
      { label: "Due Date", value: "2024-04-15", fieldType: "date" }
    ]

    temporalData: [
      {
        rawDate: "04/15/2024"
        normalizedDate: "2024-04-15"
        dateType: "deadline"
        actionRequired: true
      }
    ]

    monetaryValues: [
      {
        rawValue: "$1,234.56"
        normalizedAmount: 1234.56
        currency: "USD"
      }
    ]

    actionableInsights: [
      {
        insight: "Payment due in 7 days"
        category: "action"
        relevance: "Time-sensitive financial obligation"
      }
    ]
  }
}
```

### The 6 Tiers (Progressively Broader)

**Tier 1: Consciousness Exact Match** 
- Precise semantic search in AI-extracted structured data
- Word boundary matching on consciousness fields
- Highest confidence due to structured data accuracy

**Tier 2: Domain-Expanded Multi-Field Search** 
- Leverages domain knowledge (1,128 curated terms)
- Weighted scoring across multiple consciousness fields
- Differential field weighting (critical fields weighted higher)
- Primary query terms: full weight | Expansion terms: reduced weight

**Tier 3: Exact Filename Match** 
- Traditional exact filename matching
- Fast index-based lookups
- Useful when users remember file names

**Tier 4: Consciousness Fuzzy Match** 
- Partial/fuzzy matching in consciousness data
- Handles typos and variations
- Lower confidence due to broader matching

**Tier 5: Vector Semantic Search** 
- Pgvector cosine similarity on document embeddings
- Conceptual matching ("medical coverage" finds "health insurance")
- Semantic understanding without exact keywords

**Tier 6: Filename Fuzzy Fallback** 
- Last-resort fuzzy filename matching
- Lowest confidence tier
- Catches edge cases when all else fails

### Why This Ordering Matters

Higher tiers = more precise understanding = higher confidence

The system tries precise understanding first (structured AI data) before falling back to fuzzy matching. This ensures users get the most accurate answers first.

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

### Current State (V4.3.1)
- 6-tier consciousness-first search
- 10 specialized resolvers with intent routing
- Universal field extraction (no type constraints)
- Search idempotency (deterministic results)
- Domain knowledge system (1,128 terms)
- Denormalized search optimization

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

**© 2025 Clasio. All rights reserved.**
