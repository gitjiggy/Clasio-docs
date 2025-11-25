# Clasio - Document Consciousness™

[![License](https://img.shields.io/badge/license-Proprietary-red.svg)](LICENSE)
[![Version](https://img.shields.io/badge/version-4.3.1-blue.svg)](CHANGELOG.md)
[![Status](https://img.shields.io/badge/status-Public%20Beta-green.svg)](https://clasio.ai)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.x-3178C6?logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![React](https://img.shields.io/badge/React-18-61DAFB?logo=react&logoColor=black)](https://reactjs.org/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15-4169E1?logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![Google Cloud](https://img.shields.io/badge/Google%20Cloud-Platform-4285F4?logo=google-cloud&logoColor=white)](https://cloud.google.com/)

> Making documents intelligent. Not just searchable, but conscious.

**Website**: [clasio.ai](https://clasio.ai)
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
- Re-process documents on every query (slow, expensive)
- 3-5 second response times
- $0.02 per query cost
- 85-90% accuracy (hallucination risk)

**Clasio** (Document Consciousness):
- Extract intelligence once, query forever
- 80ms response times
- $0.00 per query
- 100% accuracy on extracted data

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

### 5. Domain-Aware Search
Understands document categories:
- Tax forms (1040, 1099, W-2, Schedule A)
- Medical records (prescriptions, lab results, imaging)
- Legal contracts (NDAs, settlements, agreements)
- Financial documents (invoices, receipts, statements)
- Real estate (deeds, mortgages, titles)
- Travel documents (passports, visas, I-94s)

### 6. Proactive Intelligence (Coming Soon)
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
- **Primary Model**: Google Gemini 2.5 Flash-lite (Paid Tier 1)
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

### 6-Tier Consciousness-First Waterfall

Documents are searched across 6 progressively broader tiers, each with measured confidence:

**Tier 1: Consciousness Exact Match** 
- Precise semantic search in AI-extracted metadata
- PostgreSQL word boundary regex on structured intelligence
- Example: "W-2" → matches `docType: "Tax Form W-2"`

**Tier 2: Domain-Expanded Multi-Field Search** 
- Leverages domain knowledge (1,128 terms) to expand queries
- Weighted multi-field scoring across 7 indexed columns
- Differential weighting (docType: 1.0 → filename: 0.3)
- Example: "passport" → searches travel document terminology

**Tier 3: Exact Filename Match** 
- Traditional exact filename matching
- Fast B-tree index lookups

**Tier 4: Consciousness Fuzzy Match** 
- Partial matching in consciousness data
- Handles typos and variations

**Tier 5: Vector Semantic Search** 
- Pgvector cosine similarity
- Conceptual matching ("medical coverage" finds "health insurance")

**Tier 6: Filename Fuzzy Fallback** 
- Last-resort fuzzy filename matching
- Catches edge cases

### Intent-Based Routing

Different query types route to specialized processors:
- **Timeline queries** → Date extraction optimization
- **Quantitative queries** → Monetary aggregation
- **Relationship queries** → Entity-focused search
- **Identifier queries** → Precision extraction from structured data
- **Document finder** → Multi-tier consciousness search

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

**Limits**: During Beta only. Please contact support@clasio.ai if you need additional size/storage abilities
- **File size**: 15MB per file
- **Storage**: 1GB per user (beta tier)
- **Document count**: 200 documents per user (beta tier)

---

## How It Works

### 1. Upload up to 25 files at a time (One-time, 3-5 seconds)
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

### 2. Query (80 milliseconds)
```
User asks question
    ↓
Intent detection (what type of query?)
    ↓
6-tier consciousness search (prioritizes AI-extracted metadata)
    ↓
Route to specialized resolver (Timeline, Quantitative, Relationship, etc.)
    ↓
Generate direct answer with confidence + source
    ↓
Return to user (<100ms)
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

## Competitive Differentiation

| Feature | Google Drive | Dropbox | Notion AI | ChatGPT | Clasio |
|---------|-------------|---------|-----------|---------|--------|
| **Keyword Search** | ✅ | ✅ | ✅ | ✅ | ✅ |
| **Semantic Search** | ❌ | ❌ | ⚠️ (RAG) | ⚠️ (RAG) | ✅ (Native) |
| **Natural Language Q&A** | ❌ | ❌ | ⚠️ (Slow) | ⚠️ (Slow) | ✅ (Fast) |
| **Direct Answers** | ❌ | ❌ | ❌ | ❌ | ✅ |
| **Auto-Organization** | ❌ | ❌ | ❌ | ❌ | ✅ |
| **Query Speed** | N/A | N/A | 3-5s | 3-5s | 80ms |
| **Query Cost** | N/A | N/A | $0.02 | $0.02 | $0.00 |
| **Accuracy** | N/A | N/A | 85-90% | 85-90% | 100% |
| **Product vs Infrastructure** | Product | Product | Product | Chat | Product |

---

## Roadmap

### ✅ Completed (V4.3.1 - Current)
- 6-tier consciousness-first search
- Intent-based routing with 10 specialized resolvers
- Universal field extraction (no type constraints)
- Domain knowledge system (1,128 terms)
- Search idempotency (deterministic results)
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
© 2025 Clasio. All rights reserved.

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
