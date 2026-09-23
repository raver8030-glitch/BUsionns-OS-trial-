# 002 — Identity, Organization and User Management Specification

**Document ID:** BOS-SPEC-002

**Document:** Identity, Organization and User Management Specification

**Status:** Detailed Domain Specification

**Phase:** Detailed Domain Specification

**Version:** 1.0

**Date:** 2026-09-03

**Product:** BusinessOS

**Derived From:**
- `000_Software_Development_Lifecycle_Master_Plan.md`
- `000.4_Product_Requirements_Specification.md` (BOS-ID-001 through BOS-ID-008, BOS-ORG-001 through BOS-ORG-005)
- `000.6_Technical_Architecture.md` (§3, §5, §6)
- `000.9_Security_and_Compliance_Architecture.md` (§5, §6, §7, §8, §9, §10, §11, §12)
- `000.10_Implementation_Planning.md` (Phase 2 identity requirements)
- `003_Authorization_Roles_Permissions_and_Access_Control_Specification.md` (§2, identity prerequisites)
- `011_HR_and_Workforce_Management_Specification.md` (§3, §4 — User/Employee boundary)
- `012_Contractors_Vendors_and_External_Workforce.md` (§2 — Contractor identity)
- `027_Client_Portal_and_External_Client_Experience_Specification.md` (§2, §3 — Portal user context)
- `028_AI_Product_and_Intelligence_Specification.md` (§2 — AI actor context)
- `029_Automation_and_Workflow_Orchestration_Specification.md` (§2, §3 — Automation actor context)
- `044_Final_End-to-End_BusinessOS_System_Specification.md` (§8, §9, §10, §11, §12, §13)

**Note on authorship:** Spec 002 was found empty in the repository. This document was constructed by systematic cross-referencing of all 43 complete specifications and 11 SDLC documents to derive every explicit and implicit identity requirement. No architectural concepts have been introduced that are not traceable to the existing specification corpus. Where the specs use language such as "as established in 002", those references have been satisfied here.

---

# 1. Purpose

This specification defines the **Identity, Organization and User Management domain** of BusinessOS.

Identity is the foundational domain of the entire platform.

Every domain in BusinessOS depends on the identity model to answer:

- Who is making this request?
- Which organization do they belong to?
- What type of actor are they?
- What is their lifecycle state?
- Are their credentials valid?
- Are their sessions current?

Identity does not determine *what* a user can do — that is authorization (spec 003). Identity determines *who* the actor is.

---

# 2. Architectural Position

The Identity domain occupies the base layer of the BusinessOS security architecture:

```text
                         Platform

                            │

                     Identity Domain

                            │

            ┌───────────────┼───────────────┐

            ▼               ▼               ▼

     Authentication    Organizations    Sessions

            │               │               │

            └───────────────┼───────────────┘

                            ▼

                     Authorization (003)

                            │

                     All Business Domains
```

Authorization (spec 003) builds upon identity.

All 44 domain specifications build upon the combination of identity and authorization.

---

# 3. Core Principle

> **Authentication identifies the actor. Membership establishes organizational relationship. Authorization (spec 003) determines permitted scope.**

These three are explicitly different and must remain separate concepts in implementation.

---

# 4. The Identity Model

BusinessOS maintains a strict multi-actor identity model.

## 4.1 Actor Types

The system must distinguish between the following actor types:

```text
Internal User           — authenticated member of an organization (employee, admin, team member)
Portal User             — external client granted access through the Client Portal (spec 027)
Contractor User         — external contractor with controlled, limited workspace access (spec 012)
System Actor (AI)       — the AI platform acting on behalf of a user (spec 028)
System Actor (Automation) — an automation worker executing a defined workflow (spec 029)
Platform Administrator  — a platform-level operator (not a tenant user)
```

**Critical invariant:** These actor types do not collapse into one another.

A Portal User is never an Internal User with hidden menus.

An Automation actor is never an Internal User executing programmatically.

An AI actor is never an unconstrained Internal User.

## 4.2 What Identity Owns

The Identity domain owns:

- User accounts (credentials, profile, contact identity)
- Organization records (tenant definitions, settings, plans)
- Organization membership (which users belong to which org, in what role category, with what status)
- Authentication mechanisms (password, email verification, MFA, OAuth extension points)
- Sessions (access tokens, refresh tokens, device records)
- Account lifecycle states
- Security events (login, logout, MFA, password change, session revocation)
- Portal user membership (which client contacts have portal access)
- Contractor user access grants (which contractors have controlled workspace access)
- Invitation management
- Account recovery mechanisms

## 4.3 What Identity Does Not Own

- Authorization rules, roles, permissions → spec 003
- Employee records (employment relationship, history, HR data) → spec 011
- Client records (CRM relationship, client organization details) → spec 004
- Contractor relationship details (skills, rates, agreements) → spec 012
- Portal content or experience → spec 027
- AI permissions or tool scope → spec 028
- Automation execution scope → spec 029

The existence of a user account does not automatically confer business access. Membership and authorization (spec 003) determine access.

---

# 5. User Account

## 5.1 User Identity

A **User** represents a system identity — the authenticated principal making requests to the platform.

A User is not:
- An employee (which is an HR concept — spec 011)
- A role (which is an authorization concept — spec 003)
- A client contact (which is a CRM concept — spec 004)

The relationship is:

```text
User
└── may have Organization Membership(s)
      └── may be linked to Employee Record (HR domain)
      └── may be linked to Contractor Profile (spec 012)
      └── may be linked to Client Contact (spec 004)
```

A single human may have:
- A User account
- An Employee record in org A
- A Contractor profile in org B
- A Portal User account in org C (as a client of org C)

These are separate relationships; the User account is the single authentication identity.

## 5.2 User Account Fields

The following fields define a User account:

| Field | Description |
|-------|-------------|
| `id` | Stable UUID, never reused or changed |
| `email` | Primary email address (unique across platform) |
| `email_verified` | Whether email address has been verified |
| `display_name` | Human-readable name |
| `avatar_url` | Optional profile picture URL (object storage reference) |
| `status` | Account lifecycle status (see §6) |
| `auth_methods` | Enabled authentication methods |
| `mfa_enabled` | Whether MFA is enabled |
| `mfa_type` | MFA type if enabled (totp, hardware_key) |
| `timezone` | User's preferred timezone |
| `locale` | User's preferred locale |
| `created_at` | When the account was created |
| `updated_at` | When the account was last modified |
| `last_login_at` | Last successful authentication timestamp |
| `password_changed_at` | When password was last changed |
| `deleted_at` | Soft-deletion timestamp (nullable) |
| `deletion_reason` | Reason for deletion if applicable |

Passwords are never stored. Only password hashes are stored (Argon2id or equivalent — see §10).

## 5.3 User Account Invariants

- A user's `id` must never change.
- A user's `email` may change but the change must be verified before taking effect.
- A deactivated user must not be able to authenticate.
- A deleted user's account must be anonymized appropriately per compliance requirements (spec 043).
- User accounts exist at the platform level, not at the organization level.

---

# 6. Account Lifecycle

User accounts move through the following lifecycle:

```text
Registered / Invited
        │
        ▼
Pending Verification
        │
        ▼
      Active
        │
   ┌────┴────┐
   ▼         ▼
Suspended  Deactivated
              │
              ▼
           Archived
```

## 6.1 Lifecycle State Definitions

| State | Description |
|-------|-------------|
| `pending_verification` | Account created; email not yet verified |
| `active` | Account is active and may authenticate |
| `suspended` | Temporarily blocked from authentication (admin or security action) |
| `deactivated` | Account deactivated; cannot authenticate; data retained for audit |
| `archived` | Historical state; account anonymized per compliance policy |

## 6.2 Lifecycle Distinctions

The system must distinguish between:

- **Disabling login** → changes `status` to `suspended` or `deactivated`
- **Removing organization membership** → removes the `organization_membership` record, not the user account
- **Revoking all sessions** → invalidates all session tokens, does not change account status
- **Revoking permissions** → modifies authorization data (spec 003), not identity data
- **Deleting/anonymizing** → data retention and compliance operation (spec 043)

These must be independent operations. A user can have their sessions revoked without being deactivated. A user can be removed from an organization without their account being deleted.

---

# 7. Organization (Tenant)

## 7.1 Definition

An **Organization** is the primary business isolation boundary (tenant) in BusinessOS.

Every piece of business data is associated with an organization.

An organization represents a business entity: a production house, agency, freelancer's workspace, or professional services company.

## 7.2 Organization Fields

| Field | Description |
|-------|-------------|
| `id` | Stable UUID, never reused or changed |
| `name` | Organization's business name |
| `slug` | URL-safe identifier (unique across platform) |
| `status` | Organization lifecycle status |
| `type` | Organization type (e.g., agency, production_house, freelancer, contractor) |
| `plan_id` | Reference to SaaS billing plan (spec 025) |
| `timezone` | Organization's primary timezone |
| `locale` | Organization's primary locale |
| `logo_url` | Optional logo URL (object storage reference) |
| `settings` | Organization-level configuration (structured JSONB) |
| `created_at` | When the organization was registered |
| `updated_at` | When the organization was last modified |
| `deleted_at` | Soft-deletion timestamp (nullable) |

## 7.3 Organization Invariants

- An organization's `id` must never change.
- Every tenant-owned business record must carry an explicit `org_id` column.
- Data belonging to Organization A must never be readable by Organization B through any query path.
- An organization may have zero users (newly created, waiting for owner), but eventually requires at least one owner.
- Organization deletion is a compliance-level operation with defined data handling (spec 043).

## 7.4 Organization Status

| Status | Description |
|--------|-------------|
| `active` | Organization is operational |
| `suspended` | Organization access temporarily blocked (billing or admin action) |
| `cancelled` | Subscription cancelled; read-only grace period |
| `decommissioned` | Organization fully decommissioned |

## 7.5 Platform Hierarchy

```text
Platform
└── Organization A (Tenant)
      ├── Users (via memberships)
      ├── Clients
      ├── Projects
      ├── Finance
      ├── Employees (HR)
      ├── Contractors
      ├── Resources
      ├── Files
      └── Configuration

└── Organization B (Tenant)
      └── ... (completely isolated)
```

Cross-tenant access is prohibited. There is no mechanism in the application for Organization A to access Organization B's data unless explicitly mediated through a defined integration channel (spec 021).

---

# 8. Organization Membership

## 8.1 Definition

**Organization Membership** is the explicit relationship linking a User to an Organization.

A user gains access to an organization's data only through an explicit, active membership record.

A user may have memberships in multiple organizations simultaneously.

## 8.2 Membership Fields

| Field | Description |
|-------|-------------|
| `id` | Stable UUID |
| `org_id` | Organization this membership belongs to |
| `user_id` | User this membership belongs to |
| `role_category` | Broad actor category (see §8.3) |
| `status` | Membership status |
| `invited_by` | User who issued the invitation |
| `invited_at` | When the invitation was issued |
| `accepted_at` | When the invitation was accepted |
| `joined_at` | When the member became active |
| `suspended_at` | When suspension was applied |
| `removed_at` | When access was removed |
| `removal_reason` | Why access was removed |
| `created_at` | Record creation timestamp |
| `updated_at` | Record last modified timestamp |

## 8.3 Membership Role Categories

At the identity layer, memberships are categorized broadly. Fine-grained authorization is managed by spec 003.

| Role Category | Description |
|---------------|-------------|
| `owner` | Organization owner; highest administrative access |
| `administrator` | Full administrative access within organization |
| `member` | Standard internal team member |
| `contractor` | External contractor with controlled access (spec 012) |
| `portal_user` | External client using the Client Portal (spec 027) |
| `billing_admin` | Access to subscription/billing management only |

These categories inform the authorization layer (spec 003). They are not permissions themselves.

## 8.4 Membership Status

| Status | Description |
|--------|-------------|
| `invited` | Invitation sent, not yet accepted |
| `active` | Full membership, can authenticate and access org |
| `suspended` | Temporarily removed from org access |
| `removed` | Access permanently removed from org; record retained for audit |

## 8.5 Membership Invariants

- A user with no active membership in an organization must not access that organization's data.
- A removed membership must be retained for audit purposes.
- Membership removal does not delete the user account.
- A suspended membership blocks org access but does not block platform authentication.

---

# 9. Portal User Access

## 9.1 Architectural Context

A **Portal User** is an external client contact who has been granted access to the Client Portal (spec 027).

The Portal represents an explicit, restricted external access context. It is not the internal application with hidden menus.

## 9.2 Portal Identity Model

Portal users:
- Are real User accounts at the platform level
- Have a Membership with `role_category = portal_user` in the organization whose portal they access
- Have an associated Client Contact record (spec 004) linking them to the CRM
- Can only see explicitly authorized client-visible projections
- Can never see internal business data: costs, margins, employee notes, internal comments

## 9.3 Portal User Lifecycle

```text
Client Contact created (spec 004)
        │
        ▼
Portal invitation issued
        │
        ▼
User account created (or existing account linked)
        │
        ▼
Portal membership activated
        │
        ▼
Portal access active
        │
        ▼
Access revoked or contact archived
```

## 9.4 Portal Security Invariant

Portal authentication must operate through a session context that identifies the actor as a portal user. The authorization layer (spec 003) must enforce the portal security boundary on every request.

---

# 10. Contractor User Access

## 10.1 Architectural Context

A **Contractor User** is an external contractor who has been granted limited, controlled access to specific internal workspace elements.

This is distinct from:
- A Contractor Profile in the Contractors domain (spec 012), which is the business relationship record
- An Employee record in HR (spec 011), which is an employment relationship

## 10.2 Contractor Identity Model

Contractor users:
- Are real User accounts at the platform level
- Have a Membership with `role_category = contractor` in the organization they are contracted with
- Have an associated Contractor Profile (spec 012) linking them to the contractor management domain
- Are granted access only to specific entities explicitly assigned to them (projects, deliverables, tasks)
- Can never access financial internals, HR records, or other contractors' information

---

# 11. System Actors

## 11.1 Architectural Context

BusinessOS includes two categories of non-human actors that must have identity representation for audit trail integrity.

## 11.2 AI Actor

When the AI platform (spec 028) performs an action on behalf of a user:
- The AI executes with the permission context of the delegating user
- AI actions are recorded with both the originating user ID and an AI actor indicator
- The AI may not elevate permissions beyond those of the delegating user
- The AI may not acquire permissions the user does not have

## 11.3 Automation Actor

When the Automation engine (spec 029) executes a workflow:
- The automation executes with the permissions explicitly granted to the automation definition
- Automation actions are recorded with an Automation actor indicator and the automation definition ID
- Automation actors must go through the standard authorization layer (spec 003)
- Automation must not have platform-level unrestricted access

## 11.4 System Actor Audit Requirements

All system actor actions must be fully auditable:
- What triggered the action
- What user context was delegated (if any)
- What the actor attempted to do
- Whether it was authorized
- What the outcome was
- Timestamp and correlation ID

---

# 12. Authentication

## 12.1 Authentication Principle

Authentication answers: **"Is this actor who they claim to be?"**

Authentication is a security-critical subsystem. It must not be implemented casually.

## 12.2 Supported Authentication Mechanisms

BusinessOS must support the following authentication mechanisms:

### 12.2.1 Email + Password

- Password strength requirements enforced at registration and change
- Passwords stored only as Argon2id hashes (never plaintext, never MD5/SHA1/bcrypt unless it provides equivalent security)
- Brute-force protection via rate limiting (IP-based, account-based)
- Account lockout after repeated failed attempts (configurable threshold)
- Password recovery via email-verified token (time-limited, single-use)
- Credential breach detection extension point (Have I Been Pwned or equivalent)

### 12.2.2 Email Verification

- All new accounts must verify email before gaining active access
- Verification token is time-limited (e.g., 24 hours)
- Re-send mechanism with rate limiting
- Change-of-email requires re-verification

### 12.2.3 Multi-Factor Authentication (MFA)

- TOTP-based MFA (RFC 6238 — e.g., Google Authenticator, Authy compatible)
- Recovery codes generated at MFA enrollment (stored as hashed values)
- MFA strongly encouraged for Owners and Administrators
- MFA required for high-risk actions regardless of account-level MFA setting (configurable per action)
- Extension point for hardware security keys (FIDO2/WebAuthn) — future capability

### 12.2.4 OAuth 2.0 / OIDC (Extension Point)

- Architecture must accommodate future SSO/OAuth integration
- Provider-agnostic OAuth flow abstraction
- Existing user accounts must be linkable to OAuth providers without account duplication
- OAuth providers may include: Google Workspace, Microsoft Entra ID, and others

## 12.3 Authentication Architecture

The authentication flow is:

```text
Client (Desktop / Web / Android / Portal)
        │
        ▼
API Gateway / Auth Endpoint
        │
        ▼
Credential Verification
        │
        ▼
MFA Check (if enabled)
        │
        ▼
Account Status Check
        │
        ▼
Membership Validation (org context if provided)
        │
        ▼
Token Issuance
        │
        ▼
Session Record Created
        │
        ▼
Security Event Logged
```

## 12.4 Threat Model

Authentication must defend against:

| Threat | Mitigation |
|--------|-----------|
| Credential stuffing | Rate limiting, lockout, breach detection |
| Brute force | Progressive delay, lockout, CAPTCHA extension point |
| Session hijacking | HTTPS only, secure cookie flags, token rotation |
| Token theft | Short-lived access tokens, refresh token rotation |
| Replay attacks | Token `jti` (JWT ID) tracking for sensitive flows |
| Account enumeration | Consistent response times and messages for invalid credentials |
| MFA bypass | Server-side MFA validation, recovery code rate limiting |
| Password recovery abuse | Time-limited single-use tokens, email confirmation |

---

# 13. Session Management

## 13.1 Token Architecture

BusinessOS uses a two-token session model:

```text
Access Token (short-lived)
  - Purpose: Authenticate individual API requests
  - Lifetime: 15 minutes (configurable)
  - Storage: Memory / secure storage on client; never localStorage
  - Content: user_id, org_id, session_id, actor_type, exp

Refresh Token (long-lived)
  - Purpose: Obtain new access tokens without re-authentication
  - Lifetime: 30 days (configurable)
  - Storage: HttpOnly, Secure, SameSite cookie (web); secure storage (desktop/mobile)
  - Rotation: Refresh token is rotated on every use (old token invalidated)
  - Reuse Detection: Reuse of a consumed refresh token invalidates the entire session
```

## 13.2 Session Record

Every active session is recorded:

| Field | Description |
|-------|-------------|
| `id` | Session UUID |
| `user_id` | Owning user |
| `org_id` | Organization context at login |
| `actor_type` | Type of actor (internal_user, portal_user, contractor_user) |
| `device_type` | Desktop / Web / Android / API |
| `device_fingerprint` | Optional hashed device identifier |
| `user_agent` | Client user agent string |
| `ip_address` | Client IP at creation (hashed or truncated for privacy) |
| `created_at` | Session creation timestamp |
| `last_active_at` | Last token use timestamp |
| `expires_at` | Session expiry timestamp |
| `revoked_at` | If session was explicitly revoked |
| `revocation_reason` | Why the session was revoked |

## 13.3 Session Revocation

Sessions must be revocable:

- By the user (explicit logout, "sign out from all devices")
- By an administrator (security incident, user suspension)
- By the system (account status change, detected anomaly)
- By expiry (access token TTL, refresh token TTL)

## 13.4 Session Invariants

- Access tokens must expire in minutes, not days.
- Refresh tokens must rotate on use — a consumed token is invalid immediately.
- Refresh token reuse must trigger session termination and a security alert.
- A session tied to a suspended/deactivated account must be rejected even if the token is technically valid.
- Sessions must be validated on every access token use — account status checked against server state.

## 13.5 Multi-Device Support

A user may have multiple concurrent sessions across:
- Desktop application
- Web browser
- Mobile (Android)
- API clients

Each session is independent. Revoking one session does not revoke others unless explicitly requested.

Users must be able to view and revoke their active sessions.

---

# 14. Invitation System

## 14.1 Invitation Flow

```text
Existing Member (with invite permission)
        │
        ▼
Issues Invitation (email + role_category)
        │
        ▼
Invitation Record Created (org_id, email, role_category, invited_by, expires_at, token_hash)
        │
        ▼
Email Sent to Invitee
        │
        ▼
Invitee Clicks Link (time-limited token)
        │
     ┌──┴──────────────────────────┐
     ▼                             ▼
New User Account              Existing Account
Created + Linked              Linked to Org
     │                             │
     └────────────────┬────────────┘
                      ▼
            Membership Activated
                      │
                      ▼
            Security Event Logged
```

## 14.2 Invitation Invariants

- Invitations must expire (configurable, default 7 days)
- Invitation tokens must be single-use
- An existing platform user may accept an invitation without re-registering
- Invitations cannot be used to escalate privileges beyond the issuer's granted scope
- Invitation links must be HTTPS and time-limited
- Invitation re-send must invalidate previous token

---

# 15. Security Events and Audit

Every significant identity event must be recorded as an immutable security event.

## 15.1 Auditable Events

| Event | Description |
|-------|-------------|
| `user.registered` | New account created |
| `user.email_verified` | Email address verified |
| `user.login.success` | Successful authentication |
| `user.login.failed` | Failed authentication attempt |
| `user.login.mfa_success` | MFA verification passed |
| `user.login.mfa_failed` | MFA verification failed |
| `user.logout` | Explicit logout |
| `user.password.changed` | Password changed |
| `user.password.reset_requested` | Password reset requested |
| `user.password.reset_completed` | Password reset completed |
| `user.mfa.enrolled` | MFA enabled on account |
| `user.mfa.removed` | MFA disabled on account |
| `user.account.suspended` | Account suspended |
| `user.account.deactivated` | Account deactivated |
| `user.session.revoked` | Session explicitly revoked |
| `user.sessions.all_revoked` | All sessions revoked |
| `org.membership.invited` | User invited to organization |
| `org.membership.accepted` | Invitation accepted |
| `org.membership.suspended` | Membership suspended |
| `org.membership.removed` | Membership removed |
| `user.refresh_token.reuse_detected` | Refresh token reuse detected (security alert) |

## 15.2 Audit Record Invariants

- Audit records must be immutable after creation
- Audit records must not contain passwords, tokens, or secrets
- Audit records must include a correlation ID for tracing
- Security events related to the same request must share a correlation ID

---

# 16. Privacy and Data Classification

## 16.1 Sensitive Fields

The following user identity fields are classified as personally identifiable information (PII):

- `email`
- `display_name`
- `avatar_url`
- `ip_address` (in session records)
- `device_fingerprint`
- `user_agent`
- `last_login_at`

These fields must be handled according to the compliance and privacy policies defined in spec 043.

## 16.2 Account Deletion and Anonymization

When a user account is deleted:
- PII must be anonymized or removed according to the retention policy
- Audit records must be retained but with PII references neutralized
- Business records that reference the user (created_by, assigned_to, etc.) must retain a non-identifying reference or a tombstone record
- Authentication credentials must be irrecoverably destroyed

---

# 17. Identity API Contract

The Identity domain exposes the following command and query surface to the platform API layer.

**Note:** Exact endpoint paths and schemas are defined in the API specification (spec 037). This section defines the required operations.

## 17.1 Authentication Operations

| Operation | Type | Description |
|-----------|------|-------------|
| Register account | Command | Create new user account |
| Verify email | Command | Verify email with token |
| Login with password | Command | Authenticate with credentials, receive tokens |
| Refresh access token | Command | Exchange refresh token for new access token |
| Logout | Command | Revoke current session |
| Logout all sessions | Command | Revoke all sessions for the user |
| Request password reset | Command | Initiate password recovery |
| Complete password reset | Command | Complete password reset with token |
| Change password | Command | Change password (requires current password) |
| Enroll MFA | Command | Set up TOTP MFA |
| Confirm MFA enrollment | Command | Confirm MFA TOTP code |
| Disable MFA | Command | Remove MFA (requires auth + current TOTP code) |
| Verify MFA | Command | Verify MFA code during login |

## 17.2 Account Management Operations

| Operation | Type | Description |
|-----------|------|-------------|
| Get current user | Query | Return authenticated user profile |
| Update profile | Command | Update display_name, timezone, locale |
| Change email | Command | Initiate email change (requires verification) |
| List active sessions | Query | Return list of active sessions |
| Revoke session | Command | Revoke a specific session |
| Delete account | Command | Initiate account deletion |

## 17.3 Organization Operations

| Operation | Type | Description |
|-----------|------|-------------|
| Create organization | Command | Register a new organization |
| Get organization | Query | Return organization details |
| Update organization | Command | Update organization settings |
| Suspend organization | Command | Suspend organization (admin) |
| List organization members | Query | Return members of an organization |
| Invite member | Command | Issue membership invitation |
| Accept invitation | Command | Accept an invitation |
| Update membership | Command | Change membership status or role category |
| Remove membership | Command | Remove user from organization |

---

# 18. Domain Boundaries

## 18.1 What Identity Explicitly Does Not Own

| Concept | Actual Owner | Spec |
|---------|-------------|------|
| Authorization roles | Authorization | 003 |
| Permissions | Authorization | 003 |
| Employee records | HR | 011 |
| Contractor relationship details | Contractors/Vendors | 012 |
| Client relationship details | CRM | 004 |
| Client contact records | CRM | 004 |
| Portal content and experience | Client Portal | 027 |
| AI behavior and tool access | AI | 028 |
| Automation execution rules | Automation | 029 |
| Invoice ownership | Finance | 015 |
| Project ownership | Projects | 005 |
| Documents | Documents | 008 |

## 18.2 Reference Pattern

When a business domain needs to associate a record with a user, it stores:

```text
created_by   = user_id (UUID reference to identity)
updated_by   = user_id (UUID reference to identity)
assigned_to  = user_id (UUID reference to identity)
```

The Identity domain is the system of record for what a user_id resolves to.

Other domains must not duplicate user profile data. They reference user_ids.

---

# 19. Implementation Notes

These notes are for the implementation team. They record requirements and constraints that must be honored during development.

## 19.1 Database Schema Requirements

Every user account table must have:
- `id UUID PRIMARY KEY` (stable, never reused)
- `email TEXT UNIQUE NOT NULL` (platform-wide uniqueness)
- `status TEXT NOT NULL` (lifecycle state enum)
- Appropriate indexes on `email`, `status`

Every organization_membership record must have:
- `id UUID PRIMARY KEY`
- `org_id UUID NOT NULL REFERENCES organizations(id)`
- `user_id UUID NOT NULL REFERENCES users(id)`
- `status TEXT NOT NULL`
- Unique constraint on `(org_id, user_id)` — one membership per user per org

Every session record must have:
- `id UUID PRIMARY KEY`
- `user_id UUID NOT NULL REFERENCES users(id)`
- `revoked_at TIMESTAMPTZ` (nullable — null means active)
- Index on `(user_id, revoked_at)` for efficient session lookup

## 19.2 Credential Security Requirements

- Password hashing: Argon2id with appropriate parameters (memory, iterations, parallelism)
- Never store passwords, tokens, or secrets in logs
- Never expose user passwords in any API response
- Never expose password hashes in any API response
- Refresh tokens must be stored as hashes (not plaintext) — validate by hashing the presented token

## 19.3 Authentication Security Requirements

- Rate limit login attempts per IP and per account
- Rate limit password reset requests per email
- Rate limit invitation acceptance attempts per token
- Validate account status on every access-token use (not just at login)
- Validate session revocation status on every access-token use
- Implement refresh token rotation and reuse detection from day one

## 19.4 No Floating Point for Timestamps

Timestamps must use timezone-aware timestamp types (TIMESTAMPTZ in PostgreSQL). Never use UNIX timestamps as floating-point values in database columns.

---

# 20. Cross-Specification Dependencies

The following specifications depend directly on the identity model established here:

| Spec | Dependency |
|------|-----------|
| 003 | Authorization roles and permissions require user_id and org_id from identity |
| 004 | Client contacts may be linked to Portal User accounts |
| 005 | Projects reference `created_by`, `owner`, team members as user_ids |
| 006 | Workflow approvals reference user_ids as actors |
| 008 | Documents reference user_ids as authors and approvers |
| 009 | Communication references user_ids as participants |
| 011 | HR Employee records are linked to user_ids but remain separate entities |
| 012 | Contractor profiles linked to user_ids with contractor membership |
| 015 | Finance operations reference user_ids for approval and audit |
| 027 | Client Portal users are a restricted membership category in this domain |
| 028 | AI acts within the user identity and permission context |
| 029 | Automation acts with an explicit automation actor identity |
| 035 | Offline sync uses session/user context for conflict attribution |
| 037 | All API requests require authenticated identity context |
| 038 | Observability correlates events via user_id and correlation IDs |
| 043 | Compliance and privacy policies apply to user PII in this domain |
| 044 | Identity is listed as the foundational domain of the entire platform |

---

*End of Specification 002.*

*This document was authored by cross-referencing the complete BusinessOS specification corpus (000–001, 003–044) and SDLC documentation set. No architectural decisions have been introduced that are not traceable to the existing corpus.*
