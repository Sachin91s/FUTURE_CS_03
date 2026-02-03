<div align="center">

# API Security Risk Analysis (Read-Only)

A professional, GitHub-standard security assessment of public REST API endpoints (passive analysis).

**Submitted By:** Sachin Kumar

[![Status](https://img.shields.io/badge/Status-Complete-success)](https://shields.io/)
[![Assessment](https://img.shields.io/badge/Assessment-Read--Only%20Passive-blue)](https://shields.io/)
[![Risk Level](https://img.shields.io/badge/Risk_Level-Medium-orange)](https://shields.io/)

</div>

---

## Project Overview

This repository contains a structured **API Security Risk Analysis** performed on publicly accessible REST endpoints provided by the GoREST platform. The objective is to identify common API security weaknesses related to:

- Authentication (AuthN)
- Authorization (AuthZ)
- Data exposure
- Rate limiting and abuse protection
- SaaS security fundamentals (privacy, access control, monitoring)

> **Important:** This assessment follows a **read-only and non-intrusive** approach. No exploitation, bypass attempts, stress testing, or denial-of-service activities were performed.

---

## Table of Contents

- [Scope of Assessment](#scope-of-assessment)
- [Endpoints Analyzed](#endpoints-analyzed)
- [Tools Used](#tools-used)
- [Methodology](#methodology)
- [Key Findings](#key-findings)
  - [Authentication](#authentication)
  - [Authorization](#authorization)
  - [Data Exposure](#data-exposure)
  - [Rate Limiting and Abuse Protection](#rate-limiting-and-abuse-protection)
- [Risk Summary](#risk-summary)
- [Recommendations](#recommendations)
- [Evidence (Screenshots)](#evidence-screenshots)
- [Skills Demonstrated](#skills-demonstrated)
- [Ethical Disclaimer](#ethical-disclaimer)
- 
---

## Scope of Assessment

| Included in Scope | Excluded from Scope |
|---|---|
| Public API endpoints | Exploitation or bypass attempts |
| Read-only HTTP methods (GET) | DoS / rate-limit flooding |
| Response body inspection (JSON) | Attacking private/production systems |
| Response header inspection | Modifying or deleting data |

---

## Endpoints Analyzed

| Endpoint | Method | Primary Security Focus |
|---|---|---|
| `/public/v2/users` | GET | PII exposure, open access validation |
| `/public/v2/posts` | GET | Content access patterns, enumeration risk |
| `/public/v2/comments` | GET | Response over-exposure assessment |
| `/public/v2/todos` | GET | User-to-resource mapping risk (in production) |

---

## Tools Used

- **Postman** (requests, responses, headers, evidence capture)
- **Browser DevTools** (optional; header verification)
- Manual analysis and documentation

---

## Methodology

1. **Endpoint Selection**  
   Identified public REST endpoints for review.

2. **Read-Only Execution**  
   Sent controlled **GET** requests to ensure no state changes occurred.

3. **Response Body Review**  
   Inspected JSON responses for sensitive fields and unnecessary exposure.

4. **Authentication Verification (AuthN)**  
   Confirmed whether endpoints require API keys/tokens/OAuth. Documented access using **No Auth**.

5. **Authorization Review (AuthZ)**  
   Observed access patterns to infer the presence/absence of role or ownership checks (passive review).

6. **Header and Metadata Inspection**  
   Reviewed HTTP response headers for pagination (`x-pagination-*`), content type, server indicators, and rate limit signals.

7. **Risk Identification and Severity Mapping**  
   Categorized issues by likelihood and impact, aligned with common API security patterns.

8. **Documentation and Evidence Collection**  
   Captured screenshots and documented findings in a structured report format.

---

## Key Findings

### Authentication
- **Observation:** Endpoints are accessible without login/token (No Auth).
- **Risk:** Anonymous access increases exposure and scraping risk in production-like SaaS systems.
- **Severity:** Medium

### Authorization
- **Observation:** No visible role/ownership enforcement for returned records (passive observation).
- **Risk:** In production systems, missing AuthZ controls can lead to horizontal data access.
- **Severity:** Medium

### Data Exposure
- **Observation:** Responses expose user-related fields (e.g., `name`, `email`, `status`).
- **Risk:** PII exposure increases phishing/spam risk and privacy concerns.
- **Severity:** Medium

### Rate Limiting and Abuse Protection
- **Observation:** No visible `X-RateLimit-*` headers; pagination headers (`x-pagination-*`) are present.
- **Risk:** Pagination can be leveraged for large-scale data harvesting if abuse controls are absent.
- **Severity:** Medium

---

## Risk Summary

| Risk Area | Description | Severity |
|---|---|---|
| Authentication | No login or token required | Medium |
| Authorization | No role or ownership checks | Medium |
| Data Exposure | Excessive response data (PII fields) | Medium |
| Rate Limiting | Abuse protection not visible; pagination present | Medium |

---

## Recommendations

To strengthen API security in SaaS environments:

- Enforce authentication using **secure tokens (JWT)** or **OAuth 2.0** where applicable
- Implement **role-based authorization** and **ownership validation** per resource
- Minimize exposed response fields; avoid exposing PII on public endpoints
- Apply rate limiting and abuse monitoring (throttling, bot protection)
- Enable logging and monitoring to detect scraping and abnormal pagination usage

---

## Evidence (Screenshots)

Store evidence files in the `evidence/` folder.

### Screenshot Checklist (Recommended)
1. **GET request + 200 OK** (URL visible)
2. **Authorization tab** showing `No Auth`
3. **Response body** showing exposed fields (sample JSON)
4. **Response headers** showing:
   - `content-type`
   - pagination headers (`x-pagination-*`)
   - any server/security indicators (e.g., CDN/cloud)
5. **Optional:** headers showing the absence of `X-RateLimit-*` (if visible)

> **Note:** Some Postman request headers (e.g., auto-generated headers) may appear disabled and cannot be unchecked. This is normal. You may crop screenshots to focus on response and response headers.

---

## Skills Demonstrated

- API Security Analysis
- Authentication and Authorization Assessment (read-only validation)
- Risk Identification and Severity Mapping
- Security Documentation and Reporting
- SaaS Security Fundamentals (access control, privacy, abuse prevention)

---

## Ethical Disclaimer

All testing activities were performed on publicly accessible endpoints using **read-only** and **passive observation** methods only. No exploitation, scanning, or intrusive attacks were conducted.

---

