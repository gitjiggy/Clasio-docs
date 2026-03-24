# Clasio - Document Consciousness™

[![License](https://img.shields.io/badge/license-Proprietary-red.svg)](LICENSE)
[![Version](https://img.shields.io/badge/version-5.1.0-blue.svg)](CHANGELOG.md)
[![Status](https://img.shields.io/badge/status-Public%20Beta-green.svg)](https://clasio.ai)
![Repo Views](https://komarev.com/ghpvc/?username=gitjiggy&repo=Clasio-docs&label=Repo%20Views&color=0e75b6&style=flat)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.x-3178C6?logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![React](https://img.shields.io/badge/React-18-61DAFB?logo=react&logoColor=black)](https://reactjs.org/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15-4169E1?logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![Google Cloud](https://img.shields.io/badge/Google%20Cloud-Platform-4285F4?logo=google-cloud&logoColor=white)](https://cloud.google.com/)

> Making documents intelligent. Not just searchable, but conscious.

**Website**: [clasio.ai](https://clasio.ai)
**Public Docs**: [clasio.ai/docs](https://clasio.ai/docs) - Live technical documentation
**Status**: Public Beta (Free during beta)
**Stack**: TypeScript, React, PostgreSQL, Google Cloud

---

## The Vision

Clasio transforms passive documents into **Document Consciousness™** - intelligent knowledge that understands and answers questions.

Upload a tax return, ask "What's my AGI?" and get `$67,890` instantly. No hunting through pages. No manual searching. No frustration.

---

## The Problem We're Solving

You spend 12 hours per week on document chaos:
- Searching for files you know you have
- Opening PDFs to find one number
- Manually organizing documents into folders
- Missing deadlines because files can't remind you

**Traditional systems** (Google Drive, Dropbox, Notion):
- Keyword search (no understanding)
- Manual organization (you do the work)
- Static files (passive artifacts)

**RAG systems** (ChatGPT, Notion AI):
- Re-process documents on every query (slow)
- 3-5 second response times
- Cost per query adds up at scale
- 85-90% accuracy (hallucination risk)

**Clasio** (Document Consciousness):
- Extract intelligence once, query forever
- Answers from inside your documents, insights across them
- Parallel search with deep answers in seconds
- 100% accuracy on extracted data, verified Gemini answers when consciousness falls short
- Upload entire folders with structure preserved
- Link multiple email accounts to one document library

---

## Core Features

### 1. Instant Natural Language Q&A
Ask questions, get direct answers:
- "What's my EIN?" → "12-3456789" (source: 2024_Tax_Return.pdf)
- "When does my lease expire?" → "March 15, 2026"
- "How much did I spend on medical?" → "$2,847.65 across 11 receipts"
- "Who is my landlord?" → "Oak Street Properties LLC"

### 2. Smart Auto-Organization
Documents file themselves based on content:
- Tax forms automatically cluster together
- Medical records group by type
- Contracts organize by vendor
- No manual folder management required

### 3. 6-Dimensional Intelligence
Every document understands itself across 6 dimensions:
- **WHAT**: Document type, key facts, entities
- **WHO**: People, organizations, relationships
- **WHEN**: Dates, deadlines, timelines
- **WHERE**: Locations, jurisdictions
- **WHY**: Purpose, obligations, context
- **HOW**: Processes, procedures, methods

### 4. Universal Field Extraction
No rigid schemas. Extract ANY labeled field from ANY document type:
- Driver license numbers
- GST IDs
- Policy numbers
- Passport numbers
- EINs, SSNs, account numbers
- Future-proof for documents we've never seen

### 5. Ask Clasio (Deep Document Q&A)
When consciousness extraction alone can't produce a confident answer, Ask Clasio sends document content directly to Gemini for a verified answer. It fires automatically as progressive enhancement in search results, and is also available as "Ask This Document" inside any document's detail view. Supports cross-document queries (e.g. "compare 2024 vs 2023 taxes") by including content from multiple related documents in a single Gemini call.

### 6. Folder Upload with Structure Preservation
Upload entire folders from your computer. Your folder hierarchy is preserved exactly as you have it, no matter how many levels deep. Every document is analyzed while respecting your existing organization. No competitor combines folder structure preservation with AI document intelligence.

### 7. Multi-Email Account Linking
Link multiple Google accounts to one Clasio identity. Sign in with any linked email and see your complete document library. Documents from all linked accounts appear in a single, unified view. No account switching, no separate libraries.

### 8. Domain-Aware Search
Understands document categories:
- Tax forms (1040, 1099, W-2, Schedule A)
- Medical records (prescriptions, lab results, imaging)
- Legal contracts (NDAs, settlements, agreements)
- Financial documents (invoices, receipts, statements)
- Real estate (deeds, mortgages, titles)
- Travel documents (passports, visas, I-94s)

### 7. Proactive Intelligence (Coming Soon)
Documents that tell you what matters:
- "Your lease auto-renews in 30 days"
- "You've almost met your insurance deductible"
- "Your passport expires before your trip"

---

## Technical Architecture

### Frontend
- **Framework**: React 18 + TypeScript
- **Build**: Vite (fast bundling + HMR)
- **State Management**: React hooks + context
- **UI Components**: Custom design system
- **Mobile**: Responsive + touch-optimized

### Backend
- **Runtime**: Node.js 20 (ESM modules)
- **Framework**: Express.js + TypeScript
- **API Design**: RESTful with structured JSON responses
- **Authentication**: Firebase Auth (token-based)
- **Queue System**: Async job processing for AI extraction

### Database
- **Engine**: PostgreSQL 15
- **ORM**: Drizzle ORM (type-safe queries)
- **Vector Search**: pgvector for semantic similarity
- **Indexing**: Strategic B-tree + GIN indexes for performance
- **Connection Pool**: Optimized for Cloud Run (2-40 connections)

### AI & Intelligence
- **Primary Model**: Google Gemini 2.5 Flash (Paid Tier 3, 30K RPM, 30M TPM)
- **Extraction**: Multi-dimensional consciousness analysis (6D framework)
- **Embeddings**: 768-dimensional vectors for semantic search
- **Domain Knowledge**: 1,128 curated terms across 10 categories
- **Intent Routing**: 10 specialized resolvers for different query types

### Infrastructure
- **Hosting**: Google Cloud Run (auto-scaling serverless)
- **Database**: Google Cloud SQL (managed PostgreSQL)
- **Storage**: Google Cloud Storage (encrypted object storage)
- **CDN**: Integrated content delivery
- **Monitoring**: Structured logging + health checks

### Security
- **Authentication**: Firebase Admin SDK with token verification
- **Data Isolation**: Multi-tenant with strict userId filtering
- **Document Access**: Time-limited signed URLs (60-minute expiration)
- **Encryption**: AES-256 at rest, TLS 1.3 in transit
- **Privacy**: Documents never train AI models 
- **Validation**: File type, size, and content validation
- **Headers**: Helmet.js security headers + CSP middleware

---

## Search Architecture

### Parallel Search + Ask Clasio

Search runs in two phases. Phase one (parallel search) finds documents and extracts answers from pre-computed consciousness data with zero API calls. Phase two (Ask Clasio) fires only when the consciousness answer is weak, sending document content to Gemini for a verified answer.

**Parallel keyword + semantic search:**
- Keyword search tests the query against 11 fields (consciousness identity, denormalized search columns, filenames) with max-based scoring.
- Semantic search runs pgvector cosine similarity on 768-dim embeddings concurrently. Skipped when keyword matches are strong.
- Results merge with dynamic weighting based on match strength.
- Trigram fallback catches typos when keyword search returns nothing.

**Consciousness extraction cascade:**
Direct answers come from pre-computed 6D metadata (structured attributes, key Q&A pairs, instant answers, content snippets) without any API calls.

**Ask Clasio (progressive enhancement):**
When consciousness confidence falls below 50% on a question query, the frontend fires Ask Clasio in the background. It sends document content to Gemini at temperature 0 and replaces the weak answer with a verified one on success.

### Intent-Based Routing

Different query types route to specialized resolvers via hint fast-path, dimension pre-filter, or pattern matching:
- **Timeline queries** → Date extraction optimization
- **Quantitative queries** → Monetary aggregation (exhaustive 100-doc search)
- **Relationship queries** → Entity and stakeholder search
- **Identifier queries** → Precision extraction from structured data
- **Document finder** → Catch-all fallback with direct Q&A lookup

### Search Idempotency

Same query = same result. Every time. Four pillars:
1. **Deterministic ordering** with stable tiebreakers
2. **Consistent data fetching** (explicit `ORDER BY` on all queries)
3. **Stable candidate pools** (50+ documents for reliable scoring)
4. **Long-lived caching** (1-year TTL eliminates variance)

---

## Performance Optimizations

### Database
- **Denormalized search fields**: 7 indexed columns for fast multi-field queries
- **Lightweight projections**: Exclude heavy embeddings (50x payload reduction)
- **Connection pooling**: 2-40 connections with automatic scaling
- **Statement timeout**: 30s timeout prevents long-running query blocking
- **Strategic indexes**: B-tree for exact match, GIN for full-text/array/JSONB

### Caching
- **L1 Cache**: In-memory LRU for hot queries (24-hour TTL)
- **L2 Cache**: Query embeddings (1-year TTL for stability)
- **Result caching**: User-scoped with automatic invalidation
- **Query fingerprinting**: SHA-256 cache keys for consistent lookups

### Content Delivery
- **Two-phase enrichment**: Lightweight fetch → Content enrichment for top N only
- **Bounded term expansion**: Max 50 terms prevents SQL overload
- **Meaningful term filtering**: Removes terms <2 chars
- **Batch operations**: Minimize roundtrips

---

## Supported File Types

**Documents**:
- PDF
- Microsoft Word (.docx, .doc)
- Microsoft Excel (.xlsx, .xls)
- Microsoft PowerPoint (.pptx, .ppt)
- Plain text (.txt)
- CSV

**Images**:
- JPEG
- PNG
- GIF
- WebP
- HEIC/HEIF (Apple)

**Limits**: During Beta only. Please contact support@clasio.ai if you need additional capacity.
- **File size**: 100MB per file
- **Storage**: 25GB per user
- **Document count**: 5,000 documents per user
- **Batch upload**: 5,000 files per batch, or entire folders with structure preserved

---

## How It Works

### 1. Upload files or folders (One-time, 3-5 seconds per document)
```
User uploads document
    ↓
Extract content (PDF/DOCX/XLSX → text)
    ↓
AI Consciousness Extraction (3 Gemini API calls)
    - Identity Analysis (type, category)
    - Intelligence Extraction (6 dimensions: WHAT/WHO/WHEN/WHERE/WHY/HOW)
    - Summary Generation
    ↓
Generate embeddings (768-dim vectors, 4 fields)
    ↓
Populate denormalized search fields (7 indexed columns)
    ↓
Store in database (structured, searchable JSON)
```

### 2. Query (Two Phases)
```
User asks question
    ↓
Phase 1: Parallel Search
    Keyword (11 SQL fields) + Semantic (pgvector) run simultaneously
    ↓
    Dynamic merge scoring → top 10 enriched documents
    ↓
    Resolver routing → consciousness extraction cascade
    ↓
    Return answer + documents to frontend

Phase 2: Ask Clasio (conditional)
    IF consciousness confidence < 50% AND query is a question:
    ↓
    Send top document content to Gemini (temperature 0)
    ↓
    Replace weak answer with verified "Ask Clasio" answer
```

---

## API Example (Conceptual)

```typescript
// Upload document
POST /api/documents/upload
{
  file: File,
  userId: string
}
→ { documentId, status: "processing" }

// Query documents
POST /api/search
{
  query: "What's my EIN?",
  userId: string
}
→ {
  answer: "Your EIN is 12-3456789",
  confidence: 0.98,
  rationale: "Found in 2024_Tax_Return.pdf",
  sources: [{ documentId, documentName }],
  documents: [...matched documents...]
}
```

---

## Roadmap

### Completed (V5.0, Current)
- Parallel keyword + semantic search with dynamic merge scoring
- Ask Clasio for deep document Q&A (progressive enhancement + "Ask This Document")
- Consciousness extraction cascade (structured attributes, key Q&A, instant answers, snippets)
- Gemini query preprocessor for typo correction and intent classification
- Intent-based routing with 10 specialized resolvers (hint fast-path, dimension pre-filter)
- Universal field extraction (no type constraints)
- 50 golden query test suite with quality grading
- Denormalized search optimization (7 indexed fields)
- Multi-tenant security architecture
- Auto-organization via affinity detection

### 🚧 In Progress (V4.4)
- Proactive intelligence surfacing
- Cross-document synthesis
- Enhanced mobile experience
- Collection management UI

### 📋 Planned (V5.0+)
- Compliance checklists (HIPAA, SOX, etc.)
- Multi-user workspaces (teams, sharing)
- API access for developers
- Advanced analytics dashboard

---

## Contributing

Clasio is currently **not open source**. The repository is private during active development.

However, we welcome:
- **Bug reports**: Help us improve quality
- **Feature requests**: Tell us what you need
- **Documentation improvements**: Clarify anything confusing
- **User feedback**: Your experience matters

Contact: support@clasio.ai

---

## License

**Proprietary Software**
© 2025-2026 Clasio. All rights reserved.

---

## Learn More

- **Website**: [clasio.ai](https://clasio.ai)
- **Documentation**: [clasio.ai/docs](https://clasio.ai/docs) 
- **Blog**: Substack newsletter (launching soon)
- **Support**: support@clasio.ai
- **LinkedIn**: [Niraj Desai](https://linkedin.com/in/desainiraj)

---

## About the Founder

**Niraj Desai**
Former product leader at Fortune 200 companies (tech, media, telecom)
Electrical Engineer, Wharton MBA
25 years of immigration paperwork across 7 visas/citizenships
Built Clasio to solve his own document chaos

"I spent 2 hours at 2am searching for an I-94 from 2007. That's when I decided documents need to be conscious, not just searchable."

---

**Try Clasio**: [clasio.ai](https://clasio.ai) (Free during beta)
