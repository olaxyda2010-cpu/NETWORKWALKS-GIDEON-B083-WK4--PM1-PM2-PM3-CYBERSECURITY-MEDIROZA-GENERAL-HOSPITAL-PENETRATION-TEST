# NETWORKWALKS-GIDEON-B083-WK4--PM1-PM2-PM3-CYBERSECURITY-MEDIROZA-GENERAL-HOSPITAL-PENETRATION-TEST
###
## 👤 Lab Information

| **Field** | **Details** |
|---|---|
| **Pentester Name**<br>*(Cybersecurity Professional)* | **OYEWALE OLAOLUWA GIDEON** |
| **Program/Batch** | B083-Networkwalks |
| **Date** | 30 SEPTEMBER 2026 |
| **Modules Completed** | W4-PM1 (Attack the website and retrieve 3 confidential patient PDF lab reports.)<br>W4-PM2 (Crack the encryption on all 3 retrieved files.)<br>W4-PM3 (Write a professional penetration testing report for the client.) |
| **Client/Target** | 1. Mediroza General Hospital (secured written permission already)<br>2. https://medirozahospital.com |
| **Permission secured from client?** | **Yes** |
| **Phases Covered** | **All Phases** |
###

# Penetration Testing Report

## 1. Executive Summary

### 1.1 Engagement Overview

| Item | Details |
|---|---|
| **Client** | Mediroza General Hospital |
| **Target** | `https://medirozahospital.com` |
| **Assessment Type** | Black-box Penetration Test & Vulnerability Assessment |
| **Scope** | Target domain only |
| **Social Engineering** | Out of scope |
| **Denial of Service** | Out of scope |
| **Authorization** | Written authorization granted |
| **Duration** | 5 days |

The assessment followed the four milestones defined in the **NetworkWalks Week 4 project**:

- **M1 — Initial Access:** Identify an application weakness and retrieve three confidential patient PDF lab reports.
- **M2 — Data Extraction:** Assess and recover the contents of the three encrypted PDF reports.
- **M3 — Critical Data Exposure:** Identify the exposure leading to staff salary and shareholder information.
- **M4 — Penetration Testing Report:** Consolidate the assessment results into a professional security report.

The assessment identified multiple security weaknesses affecting:

- Authentication
- Access control
- Document protection
- Directory configuration
- Sensitive data exposure

### Key Findings

The two most significant findings identified during the assessment were:

| # | Finding | Severity |
|---|---|---|
| 1 | **SQL Injection resulting in authentication bypass** | 🔴 **Critical** |
| 2 | **Publicly accessible historical database backup** | 🔴 **Critical** |



# 2. Scope and Rules of Engagement

The engagement was defined as a **full black-box penetration test** against the target web infrastructure. Testing activities were restricted to the authorized target domain.

## 2.1 In Scope

- `https://medirozahospital.com`

## 2.2 Out of Scope

- Social engineering
- Denial-of-service (DoS/DDoS) testing
- Testing systems outside the authorized target domain
- Testing unrelated third-party infrastructure

## 2.3 Rules of Engagement

- Testing was conducted against the authorized target only.
- No intentional denial-of-service activity was performed.
- Social engineering activities were not conducted.
- Third-party systems and infrastructure were excluded from testing.
- Testing activities were performed under written authorization.

**Authorization:** Written authorization was provided for the security assessment.



# 3. Methodology

The assessment followed a standard **black-box penetration-testing workflow** broadly aligned with the **Penetration Testing Execution Standard (PTES)** and the **OWASP Web Security Testing Guide**.

## 3.1 Assessment Workflow

Reconnaissance
      ↓
Application Mapping
      ↓
Authentication & Input Analysis
      ↓
Controlled Exploitation
      ↓
Data Recovery
      ↓
Risk Assessment
      ↓
Reporting & Remediation

## 3.2 Tools Used

- `curl`
- Linux command-line utilities
- PDF hash-extraction utilities
- Dictionary-based password recovery tools


# 4. Findings Summary

| ID | Finding | Severity | Affected Area |
|---|---|---|---|
| F-01 | SQL Injection / Authentication Bypass | **Critical** | `/patient/login.php` |
| F-02 | Exposed Historical Database Backup | **Critical** | `/old/` |
| F-03 | Weak Passwords Protecting Patient PDF Reports | **High** | Patient reports |
| F-04 | Directory Listing Enabled | **High** | `/staff/`, `/old/` |
| F-05 | Username Enumeration | **Medium** | `/patient/login.php` |
