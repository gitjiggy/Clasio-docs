# Clasio Documentation & Capabilities

> The intelligence your documents have. The capabilities other platforms don't.

**Last Updated**: November 2025
**Version**: 4.3.1

---

## Advanced Capabilities

### What makes Clasio different

These capabilities don't exist elsewhere.

---

### 🎤 Voice Search

**Traditional**: Type on tiny mobile keyboard while juggling phone/documents

**Clasio**: Speak "show me insurance card" → Results in 2 seconds

#### How It Works

Clasio uses the Web Speech API for real-time voice transcription with automatic search triggering. Voice processing happens locally in your browser - audio is never sent to external servers or retained.

**Technical Approach**:
- Browser-native speech recognition (Chrome/Edge/Safari)
- Local audio processing (privacy-first)
- Automatic search trigger on transcription complete
- Mobile-optimized with visual feedback

**Example Queries**:
- "Show me my passport"
- "Find health insurance card"
- "What's my EIN?"
- "Tax documents from 2024"

**Availability**: Works on mobile browsers (iOS Safari, Chrome, Android Chrome) and desktop browsers with microphone access.

---

### ⚡ What Needs Attention (Proactive Intelligence)

**Traditional**: You remember deadlines (or don't)

**Clasio**: Dashboard shows "Passport expires in 45 days" automatically

#### How It Works

AI extracts deadlines from document consciousness during upload, filters by confidence threshold (≥85%), and surfaces only actionable items within configurable time windows (default: next 60 days).

**Technical Approach**:
- Deadline extraction from temporal data in consciousness
- Confidence-based filtering (high confidence only)
- Countdown calculations with urgency scoring
- Dashboard widget with expandable details

**What Gets Surfaced**:
- Document expirations (passport, license, insurance)
- Contract renewals and deadlines
- Payment due dates
- Compliance filing deadlines
- Any date marked as "action required" in extraction

**Example Alert**: "Your health insurance card expires in 23 days" (with link to document)

**Future Enhancement**: Email/SMS notifications, customizable time windows, calendar integration.

---

### 🧠 Smart Collections (Affinity Detection)

**Traditional**: Manual folder organization, drag-and-drop filing

**Clasio**: Upload 4 tax docs → Auto-grouped as "2024 Tax Documents"

#### How It Works

3-stage affinity pipeline: temporal cohorts (24-hour upload window) → multi-signal similarity scoring (naming 40%, structural 10%, semantic 50%) → domain knowledge bonus → clustering with guardrails.

**Algorithm Details**:
1. **Temporal Cohort Formation**: Documents uploaded within 24 hours form candidate pools
2. **Multi-Signal Similarity**:
   - Filename similarity: 40% weight (edit distance, common tokens)
   - Structural similarity: 10% weight (document type, format)
   - Semantic similarity: 50% weight (vector embeddings, topic overlap)
3. **Domain Knowledge Boost**: Related document types get affinity bonus (e.g., 1040 + 1099 + W-2)
4. **Clustering**: Minimum 2 signals required to create collection
5. **Guardrails**: Max 50 documents per collection, minimum 2 documents

**Example Collections**:
- "2024 Tax Documents" (4 docs: 1040, 2x 1099-MISC, W-2)
- "Acme Corp Invoices" (6 docs: invoices from same vendor)
- "Medical - Blue Cross" (3 docs: insurance card, EOB, claim)

**Collection Insights** (expandable in UI):
- Shared themes and topics
- Financial summaries (if monetary data present)
- Timeline view (if temporal data present)
- Action items (if deadlines present)

---

### 📊 Quantitative Queries

**Traditional**: "How much spent on medical?" = 11 PDFs + calculator

**Clasio**: "$2,847.65 across 11 receipts" instantly

#### How It Works

Monetary values extracted during consciousness analysis → stored in structured format → aggregated on query with entity matching and confidence scoring.

**Technical Approach**:
- Universal field extraction captures all monetary values (no type constraints)
- Normalized currency and amounts stored in consciousness
- Fuzzy entity matching ("Viasat" = "ViaSat" = "Viasat Communications")
- Aggregation with confidence-weighted averaging

**Supported Query Types**:
- "How much spent on [entity]?" → Total across all invoices
- "How much did I pay [vendor]?" → Vendor-specific totals
- "What was my total [category] expenses?" → Category aggregation
- "How much earned in [year]?" → Income aggregation

**Example Results**:
- Query: "How much spent with Viasat?"
- Answer: "$45,234.50 across 3 invoices (Jan: $4,200, Mar: $3,100, Jul: $5,100)"
- Confidence: 95%
- Sources: 3 documents linked

**Limitations**: Requires monetary values present in documents, entity names must be detectable, works best with invoices/receipts/financial documents.

---

### 📅 Timeline Intelligence

**Traditional**: Calendar searches, manual tracking

**Clasio**: "What expires in Q1 2026?" → 3 documents with countdowns

#### How It Works

Temporal data extracted from consciousness → normalized date formats → filtered by time range → ranked by urgency.

**Technical Approach**:
- AI extracts all dates during upload (deadlines, expirations, effective dates)
- Date normalization (handles MM/DD/YYYY, YYYY-MM-DD, written dates)
- Date type classification (deadline, expiration, effective, signed)
- Time range filtering with natural language support

**Supported Query Types**:
- "What expires in [time period]?" → Documents expiring in range
- "When does [thing] expire?" → Specific expiration extraction
- "Show me deadlines in [month/quarter/year]" → Filtered timeline
- "What's due next month?" → Upcoming deadlines

**Example Results**:
- Query: "What expires in Q1 2026?"
- Answer: 3 documents found
  - Passport: Expires March 1, 2026 (89 days)
  - Lease Agreement: Expires March 15, 2026 (103 days)
  - Car Insurance: Expires February 28, 2026 (86 days)

**Visual Output**: Timeline view with countdown, urgency indicators, click-through to source documents.

---

### ✅ Compliance Checker

**Traditional**: Tax season panic: "Do I have everything?"

**Clasio**: Checklist shows 8/10 required docs, 2 missing

#### How It Works

Pre-built compliance templates (tax filing, mortgage application, visa application, etc.) matched against user's document library with completion tracking.

**Technical Approach**:
- Template library with required/optional document lists
- Fuzzy matching against user's classified documents
- Completion percentage calculation
- Missing document identification

**Available Templates**:
- **Tax Filing (1040)**: W-2s, 1099s, deduction receipts, prior year return
- **Mortgage Application**: Pay stubs, tax returns, bank statements, employment verification
- **Visa Application**: Passport, photos, financial docs, employment letter
- **Insurance Claim**: Policy, incident report, receipts, medical records
- **College Application**: Transcripts, test scores, essays, recommendation letters

**Example Result**:
- Template: "Tax Filing 2024"
- Status: 80% complete (8/10 required documents)
- Found:
  - ✅ W-2 (2 found)
  - ✅ 1099-MISC (1 found)
  - ✅ 2023 Tax Return
  - ✅ Charitable donation receipts
- Missing:
  - ❌ 1099-INT (interest income)
  - ❌ Medical expense receipts

**Future Enhancement**: Custom template creation, deadline integration, submission tracking.

---

## How Clasio Compares to Alternatives

### Objective comparison based on November 2025 research and direct testing

*Platform order optimized for mobile viewing - Clasio shown first*

| **Capability** | **Clasio** | **Google Drive + Gemini** | **Dropbox Dash** | **mem.ai** | **poly.app** | **Notion AI** | **ChatGPT** |
|---|---|---|---|---|---|---|---|
| **Primary Use Case** | **Document intelligence** | Workspace integration | Universal app search | Personal notes | Local file browser | Note-taking with AI | General AI chat |
| **Query Architecture** | **Pre-extraction (query structured data)** | RAG (re-process each query) | RAG with reranking | Smart search + context | Proprietary embedding | RAG (on-demand) | RAG (re-process each query) |
| **Answer Consistency** | **Idempotent (same query = same result)** | Variable (RAG variability) | Mostly consistent | Context-dependent | Generally consistent | Variable (model dependent) | Variable (RAG variability) |
| **Direct Answer Precision** | **Exact field extraction (EIN, policy #, etc.)** | Summaries with citations | Search results + snippets | Contextual answers | Citations with timestamps | AI-generated summaries | Conversational responses |
| **Cross-Document Aggregation** | **Native (e.g., "$2,847 across 11 receipts")** | Limited (manual) | Search across, no aggregation | Related notes linking | ❌ Not primary focus | ❌ Limited to context | Limited to conversation |
| **Voice Search** | **✅ Built-in web interface** | ⚠️ Via Google Assistant | ❌ | ❌ | ❌ | ❌ | ✅ Mobile app |
| **Proactive Intelligence** | **✅ "What Needs Attention" alerts** | ❌ Reactive only | ❌ Search-based | ❌ No proactive features | ❌ Manual discovery | ❌ Query-based only | ❌ Chat-based only |
| **Auto-Organization Method** | **Affinity detection (temporal + semantic)** | Manual folders | Search-based discovery | Auto-linking (knowledge graph) | ❌ Local file system | Manual organization | ❌ No file organization |
| **Data Training** | **✅ NEVER trains on your data** | ⚠️ Yes (opt-out available) | Unclear policy | Unknown | Third-party AI concerns | ⚠️ Uses AI providers | ⚠️ Yes (opt-out for some tiers) |

**Legend**:
- ✅ = Yes, fully supported
- ⚠️ = Partial or requires opt-out
- ❌ = No or not applicable
- **Bold** = Clasio's differentiation
- Regular text = Competitor strengths

---

### Honest Strengths Assessment

#### Google Drive + Gemini Deep Research

**Strengths**:
- Deep Workspace integration (Gmail, Docs, Drive, Calendar)
- Unlimited storage on paid plans
- Strong multimodal capabilities (documents, images, videos)
- Established ecosystem with billions of users
- Native mobile apps (iOS, Android)

**Limitations**:
- Requires Gemini Advanced subscription ($20/mo) for Deep Research
- Data used for AI training by default (opt-out required)
- RAG-based processing (slower responses, per-query cost)
- No proactive intelligence or deadline tracking
- Search returns documents, not direct answers

**Best For**: Users heavily invested in Google Workspace who need deep Gmail/Drive/Docs integration.

---

#### Dropbox Dash

**Strengths**:
- Universal search across connected apps (Slack, Notion, Google, Microsoft)
- Strong video/image/audio search capabilities
- Content creation tools (AI writing assistance)
- Multimodal understanding across media types

**Limitations**:
- Requires Business or Enterprise plan (no individual tier)
- Search-focused, not answer-focused
- No direct answer extraction
- No proactive intelligence

**Best For**: Teams using multiple SaaS tools who need unified search across platforms.

---

#### Notion AI

**Strengths**:
- Fully integrated workspace (notes, databases, wikis)
- Autonomous AI agents (execute tasks, not just suggest)
- Strong team collaboration features
- PDF and image analysis built-in

**Limitations**:
- Expensive ($20/user/month, Business plan required as of May 2025)
- RAG-based (3-5 second responses)
- Workspace-focused, not document management focused
- No proactive deadline tracking

**Best For**: Teams already using Notion as their primary workspace who want AI integrated into their existing workflow.

---

#### ChatGPT

**Strengths**:
- Excellent at synthesis and conversational queries
- Widely used and familiar interface
- Strong at explanations and creative tasks
- Voice interface available on mobile app

**Limitations**:
- RAG-based processing (slower responses)
- Session-bound memory for uploaded documents
- Trains on uploads unless explicitly opted out (varies by tier)
- Limited cross-document aggregation (conversation scope only)
- No file organization or management features

**Best For**: Users who want conversational AI assistance and synthesis, not dedicated document management.

---

#### mem.ai

**Strengths**:
- Affordable ($12/mo Pro plan)
- Auto-linking notes intelligently
- Smart Write and Smart Edit features
- Built-in GPT-4 writing companion

**Limitations**:
- Note-taking focused, not full document management
- Limited file format support
- Small storage limits
- No proactive intelligence features

**Best For**: Knowledge workers focused on note-taking and personal knowledge management rather than document storage.

---

#### poly.app

**Strengths**:
- Proprietary multimodal embeddings (Polyembed-v1)
- Precise citations with timecodes and page numbers
- 100GB free storage
- Strong for media files (video, audio, images)

**Limitations**:
- Early access only (waitlist required)
- macOS only (Windows version coming soon)
- No mobile support yet
- Requires local file storage

**Best For**: macOS users with large local media collections who need advanced search with precise citations.

---

#### Clasio

**Strengths**:
- Extract once, query forever ($0.00 per query after upload)
- 80ms response time (40x faster than RAG systems)
- Direct answers, not document lists
- Proactive intelligence (deadline alerts, expiration tracking)
- Never trains AI models on user documents
- Smart Collections (automatic affinity-based grouping)
- Voice search built-in
- Quantitative and timeline queries

**Limitations**:
- Beta limits (15MB per file, 200 documents, 1GB storage)
- No teams/sharing features yet
- PWA only (no native mobile apps yet)
- Smaller user base and ecosystem

**Best For**: Individuals and small businesses who need intelligent document management with instant answers and proactive alerts.

---

**Comparison Methodology**: Based on publicly available information, direct testing where possible, vendor documentation, and user reviews as of November 2025. All platforms evolve rapidly. Pricing and features subject to change.

---

## Technical Architecture

### For the technically curious

---

### 📖 Architecture Overview

**How Document Consciousness works**

Clasio uses a fundamentally different architecture than traditional RAG systems. Instead of re-processing documents on every query, we extract intelligence once during upload and query it instantly from structured data.

**Key Concepts**:
- **Extract once, query forever**: AI analysis happens during upload (3-5 seconds), then queries hit database indexes (80ms)
- **6D consciousness framework**: Every document analyzed across WHAT/WHO/WHEN/WHERE/WHY/HOW dimensions
- **Tech stack**: TypeScript, React, Node.js 20, PostgreSQL 15 + pgvector, Google Cloud Run, Gemini 2.5 Flash
- **Performance optimizations**: Denormalized search fields, connection pooling, multi-layer caching, lightweight projections

**Cost Model**:
- Upload: ~$0.003 per document (AI extraction cost)
- Query: $0.00 (database lookup, no LLM calls)
- Storage: ~$0.023/GB/month (Google Cloud Storage)

**Why This Matters**: Traditional RAG systems re-process documents on every query (~$0.02 per query). At 100 queries per document, that's $2.00 in processing costs vs Clasio's one-time $0.003 extraction cost.

[**READ FULL TECHNICAL ARCHITECTURE →**](./README.md)

---

### 🔍 Search Architecture

**Why 80ms queries vs 3-5 seconds**

Most document AI systems use RAG (Retrieval-Augmented Generation), which means every query triggers:
1. Vector search to find relevant documents (500-1000ms)
2. Retrieve document content from storage (200-500ms)
3. Send documents + query to LLM (1000-3000ms)
4. LLM generates answer (1000-2000ms)

**Total: 3-5 seconds + $0.01-0.02 cost per query**

Clasio's approach:
1. Query pre-extracted consciousness data (30ms)
2. Multi-tier search across indexed fields (50ms)
3. Return structured results (no LLM call needed)

**Total: 80ms + $0.00 cost per query**

**Key Components**:
- **6-tier consciousness-first waterfall**: Progressive search from exact → fuzzy → semantic
- **Intent-based routing**: 10 specialized resolvers optimized for specific query types
- **Search idempotency**: Same query = same result, every time (4 pillars: deterministic ordering, consistent fetching, stable pools, long-lived caching)
- **Domain knowledge**: 1,128 curated terms across 10 categories enable smart query expansion

**Performance Targets**:
- 95% of queries complete in <100ms
- >90% accuracy on test query suite
- Zero variance on repeated queries (idempotent)

[**READ FULL SEARCH ARCHITECTURE →**](./SEARCH_ARCHITECTURE.md)

---

### 🔒 Security & Privacy

**How we protect sensitive documents**

When you upload tax returns, medical records, legal contracts, and immigration paperwork, we treat them like we're storing our own (because we are).

**Security Architecture**:
- **Never trains AI models**: Documents never used for model training (verified API contracts)
- **AES-256 encryption**: Data encrypted at rest (Google Cloud Storage managed encryption)
- **TLS 1.3 in transit**: All API communication encrypted
- **Multi-tenant isolation**: Database-level userId filtering on every query
- **Time-limited access URLs**: Signed URLs expire after 60 minutes
- **Path validation**: Every file operation validates user ownership
- **No employee access**: Service account operations only, no human credential path

**Compliance Readiness**:
- GDPR-aligned (data portability, right to deletion)
- CCPA-compliant (California privacy rights)
- HIPAA-ready technical controls
- SOC 2 Type II readiness (via GCP infrastructure)

**Verification**:
We encourage technical due diligence. You can verify our security claims by:
- Testing data deletion (upload → delete → verify complete removal)
- Inspecting network traffic (all HTTPS, no exposed credentials)
- Testing access control (create multiple accounts, verify isolation)
- Reviewing signed URLs (time-limited, expiration enforced)

[**READ FULL SECURITY ARCHITECTURE →**](./SECURITY.md)

---

## Additional Resources

### Already Have Questions?

Visit our [**Frequently Asked Questions**](/faq) page for answers about:
- Getting started and sign-in
- How to add documents
- What intelligence gets extracted
- Trust and privacy details
- Technical comparisons
- Pricing and support

### Need Help?

**Support Email**: support@clasio.ai
**Response Time**: <24 hours for all inquiries
**Beta Users**: We respond to all feedback, bug reports, and feature requests

---

## Try Clasio

**Free during beta • No credit card required**

Ready to transform your documents from passive files into intelligent knowledge?

**[GET STARTED →](https://clasio.ai)**

---

**© 2025 Clasio. All rights reserved.**

*This documentation reflects Clasio v4.3.1 as of November 2025. Features and capabilities evolve rapidly based on user feedback.*
