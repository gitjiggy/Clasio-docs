# Changelog

All notable changes to Clasio's architecture and capabilities will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [4.3.1] - 2025-11-24

### Added
- Universal field extraction (no type constraints) - extracts ANY labeled field from ANY document
- Database-backed Drive OAuth for persistent Google Drive connections
- Collections subfolder pagination improvements
- Dev/Prod database isolation for safer development

### Fixed
- Collections subfolder pagination edge cases
- Google Drive OAuth token persistence issues

### Documentation
- Created dedicated documentation repository (Clasio-docs)
- Added comprehensive SEARCH_ARCHITECTURE.md deep-dive
- Added detailed SECURITY.md with privacy guarantees
- Created DOCUMENTATION.md for user-facing capabilities

---

## [4.3.0] - 2025-11-18

### Added
- Intent-based routing system with 10 specialized resolvers
- Direct answer precision extraction for identifier queries
- Enhanced query intent classification (WHAT/WHO/WHEN/WHERE/WHY/HOW/HOW_MUCH)
- Improved grounding verification for answer accuracy

### Changed
- Refactored search architecture to use universal consciousness search
- Consolidated resolver pattern matching logic
- Enhanced confidence scoring for all resolver types

### Improved
- Answer precision for EIN, policy numbers, license numbers
- Quantitative query aggregation across documents
- Timeline query handling with better date normalization

---

## [4.2.0] - 2025-11-10

### Added
- Smart Collections with affinity detection
- Temporal cohort formation (24-hour upload windows)
- Multi-signal similarity scoring (naming 40%, structural 10%, semantic 50%)
- Domain knowledge bonus for related document types
- Collection insights (shared themes, financial summaries, timelines)

### Changed
- Auto-organization algorithm to use 3-stage affinity pipeline
- Clustering with guardrails (min 2 docs, max 50 per collection)

---

## [4.1.0] - 2025-11-01

### Added
- Proactive intelligence dashboard ("What Needs Attention")
- Deadline extraction with confidence thresholds (≥85%)
- Countdown calculations with urgency scoring
- Configurable time windows (default: 60 days)

### Improved
- Temporal data extraction from consciousness
- Dashboard widget with expandable deadline details

---

## [4.0.0] - 2025-10-15

### Added
- 6-tier consciousness-first waterfall search architecture
- Domain knowledge system with 1,128 curated terms across 10 categories
- Search idempotency (deterministic results with 4 pillars)
- Denormalized search fields (7 indexed columns)
- Multi-layer caching (L1 in-memory, L2 embeddings, L3 results)

### Changed
- **BREAKING**: Migrated from RAG to pre-extraction architecture
- Redesigned database schema with pgvector integration
- Refactored consciousness extraction pipeline

### Performance
- Sub-second document discovery via parallel keyword and semantic search
- Ask Clasio deep answers verified against document content (~$0.008 per deep query)
- Near-zero cost for consciousness-based queries (pre-extracted data)
- 50x payload reduction with lightweight projections

---

## [3.x] - 2025-09 and earlier

### Legacy Architecture
- RAG-based document processing
- On-demand LLM queries for each search
- Basic keyword and semantic search
- Manual document organization

### Migration to v4.0
- Complete architecture redesign
- Migration from RAG to consciousness-first approach
- One-time data migration for existing users

---

## Versioning Strategy

- **Major versions (X.0.0)**: Fundamental architecture changes, breaking changes
- **Minor versions (4.X.0)**: New features, capabilities, or significant enhancements
- **Patch versions (4.3.X)**: Bug fixes, minor improvements, documentation updates

---

## Roadmap

### Planned for V4.4
- Enhanced proactive intelligence surfacing
- Cross-document synthesis
- Improved mobile experience
- Collection management UI enhancements

### Planned for V5.0+
- Compliance checklists (HIPAA, SOX, etc.)
- Multi-user workspaces (teams, sharing)
- Public API access for developers
- Advanced analytics dashboard
- Voice-first query interface

---

**For detailed technical changes, see**:
- [README.md](./README.md) - Architecture overview
- [SEARCH_ARCHITECTURE.md](./SEARCH_ARCHITECTURE.md) - Search system deep-dive
- [SECURITY.md](./SECURITY.md) - Security & privacy architecture

**Questions?** Contact support@clasio.ai
