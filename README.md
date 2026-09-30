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

## Reconnaissance

<img width="1348" height="610" alt="image" src="https://github.com/user-attachments/assets/95c06a5b-58fc-4883-a88d-89165d664144" />
<img width="1366" height="381" alt="image" src="https://github.com/user-attachments/assets/1c52297c-2908-4d3a-848e-25fad38b4938" />
<img width="1351" height="214" alt="image" src="https://github.com/user-attachments/assets/aab987c4-a0d7-4c46-8401-1ac8517c44e6" />
<img width="1366" height="182" alt="image" src="https://github.com/user-attachments/assets/fbe736d7-4f78-4558-a3aa-db7efe565a4d" />






# 4. Findings Summary

| ID | Finding | Severity | Affected Area |
|---|---|---|---|
| F-01 | SQL Injection / Authentication Bypass | **Critical** | `/patient/login.php` |
| F-02 | Exposed Historical Database Backup | **Critical** | `/old/` |
| F-03 | Weak Passwords Protecting Patient PDF Reports | **High** | Patient reports |
| F-04 | Directory Listing Enabled | **High** | `/staff/`, `/old/` |
| F-05 | Username Enumeration | **Medium** | `/patient/login.php` |

# 5. Detailed Findings

## F-01 — SQL Injection / Authentication Bypass

**Severity:** Critical

**Affected Endpoint:**

`POST /patient/login.php`

### Description

The patient authentication mechanism was found to process user-supplied input in a manner that allowed SQL injection.

Initial testing produced different responses for invalid usernames. Further controlled testing produced a SQL-related application response, indicating that user input was reaching the database layer without adequate protection.

A controlled authentication-bypass test subsequently resulted in access to the authenticated patient area without a valid password.

### Impact

Successful exploitation provided access to functionality intended for authenticated users and allowed retrieval of the three designated patient-report PDFs.

Because the affected information concerns patient laboratory reports, unauthorized access could result in significant confidentiality and privacy exposure.

### Evidence

The assessment documented:

- Discovery of the patient login endpoint
- Username enumeration
- SQL-related behavior following manipulated input
- Successful authentication bypass
- Access to the patient report area
- Retrieval of three protected PDF reports

### Remediation

1. Use parameterized SQL queries/prepared statements.
2. Never concatenate user-controlled input directly into SQL queries.
3. Validate input server-side.
4. Implement centralized authentication and authorization controls.
5. Return generic authentication error messages.
6. Implement security regression tests for authentication endpoints.
7. Review application logs for potential exploitation attempts.

<img width="1352" height="705" alt="image" src="https://github.com/user-attachments/assets/3c4b699c-c642-489c-abb0-7abd0c714beb" />
<img width="1366" height="701" alt="image" src="https://github.com/user-attachments/assets/d79b6364-1c18-476c-b846-45dc774c1138" />
<img width="1366" height="664" alt="image" src="https://github.com/user-attachments/assets/cd176be6-86a6-477d-8858-dbc75489f7a7" />

## F-02 — Publicly Accessible Historical Database Backup

**Severity:** Critical

**Affected Endpoint:**

`/old/mediroza_db_backup_2019.sql`

### Description

A historical SQL database backup was discovered inside a publicly accessible web directory.

The database backup contained sensitive staff and shareholder information.

The exposed information included categories such as:

- Staff names
- Job titles
- Departments
- Contact information
- National identification information
- Monthly salary information
- Shareholder/ownership information

### Impact

An unauthenticated user could retrieve sensitive organizational information directly from the web server without first compromising an account.

This significantly increases the potential impact of the application's other vulnerabilities.

### Evidence

The `/old/` directory exposed a downloadable historical database backup named:

`mediroza_db_backup_2019.sql`

The backup contained staff records and a separate shareholder table.

### Remediation

1. Remove database backups from the web document root.
2. Delete obsolete backups from publicly accessible directories.
3. Store backups outside the web-accessible filesystem.
4. Restrict access to backup storage.
5. Encrypt sensitive backups at rest.
6. Establish formal backup retention and destruction procedures.
7. Scan deployments for files such as:
   - `.sql`
   - `.bak`
   - `.old`
   - `.zip`
   - `.backup`
8. Disable directory indexing.
9. Review web-server access logs for unauthorized access to the exposed backup.
10. Rotate or invalidate any credentials, secrets, or keys that may have been contained in the backup.

<img width="1366" height="285" alt="image" src="https://github.com/user-attachments/assets/02582ae3-bd99-4a9a-8970-ead51411f45a" />
<img width="1366" height="585" alt="image" src="https://github.com/user-attachments/assets/c2905a6a-c0ef-4ac5-a13f-288fda2e046d" />

## F-03 — Weak Passwords Protecting Patient PDF Reports

**Severity:** High

### Description

The three patient-report PDFs retrieved during **M1** were password protected.

During **M2**, each document was assessed independently, and the passwords were recovered using dictionary-based password recovery.

All three reports were successfully accessed during the authorized assessment.

### Results

| File | Result | Recovery Method |
|---|---|---|
| `patient_report_1.pdf` | Recovered | Dictionary attack |
| `patient_report_2.pdf` | Recovered | Dictionary attack |
| `patient_report_3.pdf` | Recovered | Dictionary attack |


### Impact

Weak document passwords can provide insufficient protection for sensitive healthcare information once an attacker obtains the encrypted files.

An attacker may perform offline password recovery without further interaction with the web application.

This creates an additional confidentiality risk because sensitive patient information may remain accessible even when the PDF files themselves are encrypted.

### Remediation

- Use strong, randomly generated passwords.
- Avoid dictionary words and common password patterns.
- Use modern document encryption with strong cryptographic settings.
- Prefer authenticated portal access over direct downloadable medical documents.
- Apply strict access controls to sensitive document exports.
- Implement data-loss-prevention controls where appropriate.
- Avoid exposing sensitive documents through predictable or publicly accessible URLs.
- Review existing patient documents and re-encrypt them using stronger protection.
- Establish policies for secure handling and distribution of patient records.

<img width="1352" height="476" alt="image" src="https://github.com/user-attachments/assets/e392d0be-497c-4928-878b-0500459f0754" />
<img width="1109" height="572" alt="image" src="https://github.com/user-attachments/assets/37bb9014-1c4c-4e01-9ccd-4183c6637825" />
<img width="867" height="678" alt="image" src="https://github.com/user-attachments/assets/49d56d59-64b0-46da-be35-32c4b03f1547" />
<img width="1348" height="529" alt="image" src="https://github.com/user-attachments/assets/3b8ddfdb-9ae8-4d9c-9c6d-8ca67899e4fd" />
<img width="1360" height="501" alt="image" src="https://github.com/user-attachments/assets/39850cda-25b4-4966-838a-edf7dbea4bae" />
<img width="1360" height="501" alt="image" src="https://github.com/user-attachments/assets/8ad82d38-e0b1-41b8-b5b8-ee2893f6acf7" />

## F-04 — Directory Listing Enabled

**Severity:** High

**Affected Paths:**

- `/staff/`
-  `/patient/`
- `/old/`

### Description

Directory indexing was enabled on sensitive web directories.

The `/staff/` directory exposed application filenames, including the staff login endpoint.
The `/patient/` directory exposed application filenames, including the patient login endpoint.
The `/old/` directory exposed the historical database backup.

### Impact

Directory listing can:

- Reveal application paths.
- Expose backup files.
- Increase the available attack surface.
- Help attackers identify administrative functionality.
- Directly expose sensitive files.
- Provide useful information for further reconnaissance.

### Remediation

Disable directory indexing/autoindexing on web-accessible directories.

For Apache, the following configuration can be used:

<img width="1365" height="599" alt="image" src="https://github.com/user-attachments/assets/a7bf42f2-da1e-4be9-bb53-f4b78b83b110" />
<img width="1366" height="559" alt="image" src="https://github.com/user-attachments/assets/2d9b89e3-a868-49d3-b052-ae709d37a642" />
<img width="1354" height="467" alt="image" src="https://github.com/user-attachments/assets/6cdfcfcd-6471-49ac-8258-ab11c4074746" />

# F-05 — Username Enumeration

**Severity:** Medium

**Affected Endpoint:**

` /patient/login.php`

### Description

The authentication mechanism returned a response indicating whether a submitted username existed.

This behavior allows an attacker to distinguish valid usernames from invalid usernames.

### Impact

Username enumeration can assist with:

- Credential attacks
- Password spraying
- Account discovery
- Targeted authentication attacks
- Identification of valid user accounts

### Remediation

Return a generic authentication failure message regardless of whether the submitted username exists.



# 6. Milestone Results

## M1 — Initial Access

**Status: Complete**

Reconnaissance identified the patient authentication area and additional application paths.

Controlled testing demonstrated an authentication weakness and resulted in access to the designated patient-report area.

### Deliverables Achieved

- Proof of access
- Three patient-report PDF files

---

## M2 — Data Extraction

**Status: Complete**

The three retrieved PDF files were independently assessed.

All three document passwords were successfully recovered using dictionary-based password recovery.

### Deliverables Achieved

- Successful access to all three designated files
- Evidence of password recovery

---

## M3 — Critical Data Exposure

**Status: Complete**

Further analysis of the exposed web directories identified a historical SQL database backup.

The backup contained the information required by the milestone, including:

- Staff salary information
- Staff personal information
- Shareholder information

  <img width="1122" height="586" alt="image" src="https://github.com/user-attachments/assets/e7e6ff09-b17c-4ceb-a979-af0a5daef359" />
  <img width="1081" height="440" alt="image" src="https://github.com/user-attachments/assets/3c1e6e14-5220-46ed-9522-2187671cf0ff" />



### Deliverables Achieved

- Evidence of the exposed database backup
- Identification of staff salary information
- Identification of shareholder information

---

# 7. M4 — Penetration Testing Report

**Status: Complete**

This report consolidates the results of **M1–M3** and provides:

- Executive Summary
- Scope
- Methodology
- Findings
- Evidence
- Risk Ratings
- Impact Analysis
- Remediation Recommendations

---

# 8. Risk Rating Summary

| Finding | Exploitability | Authentication Required | Data Sensitivity | Severity |
|---|---|---|---|---|
| SQL Injection / Authentication Bypass | Trivial | None | Very High | **Critical** |
| Exposed Database Backup | Trivial | None | Very High | **Critical** |
| Weak PDF Passwords | Low effort after file acquisition | None | Very High | **High** |
| Directory Listing | Trivial | None | High | **High** |
| Username Enumeration | Trivial | None | Moderate / Indirect | **Medium** |

---

# 9. Overall Security Observations

The assessment demonstrated how multiple weaknesses could be chained together:

```text
Public Reconnaissance
        ↓
Sensitive Path Discovery
        ↓
Authentication Weakness
        ↓
Unauthorized Portal Access
        ↓
Patient Report Acquisition
        ↓
Weak Document Protection
        ↓
Sensitive Data Recovery
        ↓
Public Backup Exposure
        ↓
Staff & Ownership Data Exposure
```
# 10. Remediation Priorities

## 10.1 Immediate Actions

1. Remove all database backups from the web root.
2. Restrict or remove `/old/`.
3. Disable directory indexing.
4. Remediate the SQL injection vulnerability.
5. Review and rotate credentials potentially exposed through the database backup.
6. Treat exposed sensitive information as compromised within the training scenario.

## 10.2 Short-Term Actions

7. Replace weak PDF passwords.
8. Standardize authentication error messages.
9. Implement centralized authorization checks.
10. Add automated security testing for authentication and file-access functionality.
11. Scan production deployments for backup and temporary files.

## 10.3 Long-Term Actions

12. Establish secure software-development lifecycle practices.
13. Conduct recurring web application penetration tests.
14. Implement secure backup-management procedures.
15. Apply least privilege to application and database accounts.
16. Implement centralized security logging and monitoring.
17. Provide developer security training covering:

- SQL Injection
- Authentication security
- Authorization
- Sensitive-data protection
- Secure file management

# 13. Conclusion

The authorized black-box assessment identified multiple weaknesses across authentication, application input handling, document protection, directory configuration, and sensitive-data exposure.

The assessment demonstrated that the SQL injection vulnerability could result in authentication bypass and unauthorized access to patient-report functionality. Further testing demonstrated that the retrieved documents were protected by weak passwords.

The assessment also identified publicly accessible directories and a historical database backup containing sensitive staff and shareholder information.

The M1, M2, and M3 objectives were completed, and this document fulfills the M4 requirement for a professional penetration-testing report.

---

# Disclaimer

This repository documents a controlled cybersecurity training exercise.

The target and techniques described in this report must **not** be tested against systems without explicit written authorization.

Sensitive patient, employee, and shareholder information has intentionally been omitted or redacted from this public version.

---

# Project Information

| Field | Details |
|---|---|
| **Program** | NetworkWalks — Week 4 |
| **Client** | Mediroza General Hospital |
| **Target** | `https://medirozahospital.com` |
| **Milestones** | M1, M2, M3, M4 |
| **Authorization** | Written authorization granted |

---













