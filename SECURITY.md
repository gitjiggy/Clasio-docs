# Clasio Security & Privacy Architecture

**Last Updated**: November 2025
**Version**: 4.3.1

> Built like we're storing our own tax returns. Because we are.

---

## Table of Contents
1. [Security Philosophy](#security-philosophy)
2. [Authentication & Authorization](#authentication--authorization)
3. [Multi-Tenant Data Isolation](#multi-tenant-data-isolation)
4. [Document Access Control](#document-access-control)
5. [Encryption](#encryption)
6. [Input Validation & Quotas](#input-validation--quotas)
7. [Infrastructure Security](#infrastructure-security)
8. [Privacy Guarantees](#privacy-guarantees)
9. [Error Handling & Monitoring](#error-handling--monitoring)
10. [Compliance Readiness](#compliance-readiness)

---

## Security Philosophy

When you upload your tax returns, medical records, insurance cards, contracts, and immigration paperwork to Clasio, you're trusting us with your most sensitive documents.

We take that trust seriously.

**Our approach**:
- Security paranoia by design
- Pro-grade architecture without enterprise pricing
- Multiple layers of defense (defense in depth)
- Transparency about our security model
- Privacy-first data handling

We don't just follow security best practices. We assume every component could fail and build redundant protections.

---

## Authentication & Authorization

### Token-Based Authentication

**Firebase Admin SDK Integration**
- Industry-standard authentication using Google's Firebase platform
- Cryptographically signed JWT tokens
- Token verification on every API request
- No plaintext passwords stored in Clasio systems

**Token Extraction**
- Multi-source token detection (Authorization header, cookies, session)
- Secure token transmission only
- Automatic token refresh handling
- Session management with expiration

**User Identity Verification**
- Every request validates user identity before processing
- User ID extraction and validation
- No anonymous access to document operations
- Failed authentication = immediate request rejection

### Authorization Model

**Role-Based Access**
- Users can only access their own documents
- No cross-user data access (enforced at database level)
- Admin operations require elevated privileges
- API endpoints enforce user-scoped data access

---

## Multi-Tenant Data Isolation

### Database-Level Isolation

**Tenant Separation Strategy**
- Every database row tagged with userId
- All queries filtered by authenticated user ID
- No shared data between users
- Isolation verified at query execution time

**How It Works**
- Think of it like apartments: shared building (database), private spaces (your data)
- Your documents never appear in another user's searches
- Your search history stays private
- Your extracted intelligence is yours alone

**Query-Level Enforcement**
- Every database query includes userId filter
- Automatic injection of tenant isolation clauses
- No manual filtering (reduces human error)
- Validated at ORM level

### Storage Isolation

**Document Storage Architecture**
- User-specific paths in object storage
- Path structure: `users/{userId}/docs/{docId}/{filename}`
- No path traversal vulnerabilities
- Strict path validation on all operations

---

## Document Access Control

### Time-Limited Access URLs

**Signed URL Strategy**
- Documents served via time-limited signed URLs
- Default expiration: 60 minutes
- URL regeneration required after expiration
- No permanent public links

**Why This Matters**
- Even if a URL leaks, it expires quickly
- You control document access lifetime
- Shared links become invalid automatically
- Reduces risk of unauthorized access

### Path Validation

**File System Security**
- Strict validation of all file paths
- No directory traversal attacks possible
- Whitelisted path patterns only
- Sanitization of user-provided filenames

**Access Control Checks**
- Every document request verifies ownership
- UserId matching before URL generation
- No access to documents you don't own
- Audit trail for all access attempts

---

## Encryption

### Data at Rest

**Storage Encryption**
- AES-256 encryption for all stored documents
- Google Cloud Storage encryption by default
- Database encryption at rest (Cloud SQL managed encryption)
- Encrypted backups

**Metadata Protection**
- Document consciousness data encrypted
- Search indexes protected
- User information encrypted
- Credentials never stored in plaintext

### Data in Transit

**Transport Layer Security**
- TLS 1.3 for all API communication
- HTTPS-only connections (HTTP automatically upgraded)
- Certificate validation enforced
- Secure WebSocket connections (future feature)

**API Security Headers**
- Helmet.js security headers applied
- Content Security Policy (CSP) enforcement
- X-Content-Type-Options: nosniff
- X-Frame-Options: DENY
- HSTS (HTTP Strict Transport Security)

---

## Input Validation & Quotas

### File Upload Validation

**Size Limits**
- Maximum file size: 100MB per document
- Hard limit enforced at upload time
- Prevents resource exhaustion attacks
- Quota-aware upload processing

**File Type Validation**
- Whitelist of supported file types
- MIME type verification
- Magic byte inspection (not just extension checking)
- Malicious file rejection

**Content Validation**
- File integrity checks
- Corrupted file detection
- Extraction preview before full processing
- Graceful error handling for invalid files

### Quota Management

**Resource Limits (Beta Tier)**
- Storage: 25GB per user
- Documents: 5,000 per user
- File size: 100MB per document
- Upload rate limiting
- API request throttling

**Quota Enforcement**
- Pre-upload quota checks
- Transaction rollback on quota exceeded
- Clear error messages with current usage
- No partial uploads consuming quota

**Abuse Prevention**
- Rate limiting on API endpoints
- Upload frequency monitoring
- Suspicious activity detection
- Automatic temporary lockouts

---

## Infrastructure Security

### Cloud Architecture

**Google Cloud Platform**
- Enterprise-grade infrastructure
- SOC 2 Type II certified providers
- ISO 27001 compliance
- Regular security audits by Google

**Serverless Deployment**
- Google Cloud Run (auto-scaling containers)
- No persistent server state
- Automatic security patches
- Ephemeral compute instances

### Database Security

**Cloud SQL (Managed PostgreSQL)**
- Automatic security updates
- Encrypted connections (Unix socket in production)
- Private VPC networking
- No public IP exposure

**Connection Management**
- Connection pooling (2-40 connections)
- Statement timeouts (30 seconds)
- Idle connection cleanup
- Connection leak detection

**Query Safety**
- Parameterized queries only (no SQL injection)
- Type-safe ORM (Drizzle)
- Query timeout enforcement
- Input sanitization

### Network Security

**CORS Configuration**
- Strict origin whitelisting
- Production: Only clasio.ai domains allowed
- Credentials flag properly configured
- Preflight request handling

**CSP (Content Security Policy)**
- Script source restrictions
- Style source restrictions
- Image source whitelisting
- No inline script execution

**Firewall & DDoS Protection**
- Google Cloud Armor integration
- Automatic DDoS mitigation
- Rate limiting at edge
- Geographic filtering (optional)

---

## Privacy Guarantees

### Never Trains AI Models

**Strict Policy**
- Your documents NEVER train any AI model
- No data retention by AI providers
- No model fine-tuning on your data

**Processing Model**
- AI processes your documents during upload
- Extraction happens in real-time
- AI forgets your document immediately after processing
- Only extracted metadata stored

### Data Retention

**User Control**
- You own your data
- Delete documents anytime (permanent deletion)
- Account deletion removes all user data
- 30-day retention for recovery (optional)

**What We Store**
- Original documents (encrypted)
- Extracted metadata (document consciousness)
- Search embeddings (vector representations)
- User profile (minimal: email, userId)

**What We DON'T Store**
- Credit card information (no payment setup in beta)
- Plaintext passwords (Firebase handles auth)
- Document access logs beyond security monitoring
- Marketing analytics beyond essential metrics

### Third-Party Services

**Limited Dependencies**
- Firebase Auth (authentication only)
- Google Cloud Platform (infrastructure)
- Google Gemini API (document processing)

**Data Sharing**
- We don't sell your data. Ever.
- No third-party marketing integrations
- No advertising networks
- No data brokers

---

## Error Handling & Monitoring

### Secure Error Messages

**User-Facing Errors**
- No sensitive information in error messages
- No stack traces exposed to frontend
- Generic messages for security failures
- Quirky, friendly error text (without revealing system internals)

**Example Approach**
- "Houston, we have a problem!" (file too large)
- "Document collector's achievement unlocked!" (quota exceeded)
- Friendly UX without compromising security

### Logging & Monitoring

**Structured Logging**
- All API requests logged with timestamp
- Authentication events tracked
- Failed login attempts monitored
- Suspicious activity flagged

**What We Log**
- Request metadata (userId, endpoint, timestamp)
- Performance metrics (query latency, error rates)
- Security events (failed auth, quota violations)
- System health (database connections, API errors)

**What We DON'T Log**
- Document content
- Search query details (PII-scrubbed)
- User passwords or tokens
- Sensitive extracted data

### Incident Response

**Security Event Handling**
- Real-time alerting for critical issues
- Automated response to common attacks
- Manual review of suspicious patterns
- User notification for account-related events

**Transparency Commitment**
- Security incidents disclosed to affected users
- Timeline provided for remediation
- Post-mortem analysis shared
- Continuous improvement process

---

## Compliance Readiness

### Standards Alignment


**Technical Controls**
- Data encryption (at rest and in transit)
- Access controls (authentication & authorization)
- Audit logging (security events tracked)
- Data isolation (multi-tenant architecture)
- Backup and recovery (Cloud SQL automated backups)

### Future Compliance Roadmap

**Planned Certifications**
- SOC 2 Type II audit (when revenue supports cost)
- HIPAA Business Associate Agreement (for healthcare users)
- ISO 27001 certification
- FedRAMP authorization (for government users)

**We're Building For It Now**
- Architecture designed with compliance in mind
- Security controls exceed current requirements
- Documentation of data flows and processing
- Regular third-party security assessments planned

---

## Security Best Practices for Users

### Recommendations

**Account Security**
- Use strong, unique passwords
- Enable two-factor authentication (via Firebase)
- Don't share account credentials
- Log out on shared devices

**Document Security**
- Review uploaded documents periodically
- Delete documents you no longer need
- Report suspicious activity immediately

**Privacy Tips**
- Use Clasio for personal/professional documents only
- Don't upload documents you don't own
- Review our privacy policy regularly
- Contact us with security concerns: support@clasio.ai

---

## Contact & Disclosure

**Security Team**
- Email: support@clasio.ai
- Response time: <24 hours for critical issues

**Responsible Disclosure**
- We welcome security research
- Coordinated disclosure preferred
- No legal action for good-faith research
- Recognition for valid findings

---

**Questions about our security?**
Email: support@clasio.ai

**Want to audit our architecture?**
Enterprise customers (future): We'll provide detailed security documentation and architecture reviews.

---

**© 2025 Clasio. All rights reserved.**

*This document describes our security architecture at a conceptual level. Implementation details are confidential. Last updated: November 2025.*
