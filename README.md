# Penetration Testing Report — Mediroza General Hospital

**NetworkWalks Cybersecurity Internship — Batch B084 — Week 4 **

- **Target:** https://medirozahospital.com
- **Type:** Black-box Penetration Test


> Conducted in a controlled training environment for educational purposes, under written authorization from Mediroza General Hospital to NetworkWalks.

## 1. Security Assessment

VAPT was performed on `medirozahospital.com` as part of the Week 4 capstone project. **5 findings** were identified, **3 rated Critical**, including a SQL injection authentication bypass and an exposed legacy database backup — two independent paths into confidential patient and staff data.

## 2. Methodology & Tools

**Reconnaissance:** `whois`, `subfinder`, `whatweb`, `Nmap`/`Zenmap`

**Enumeration & Exploitation:** `gobuster` (directory brute-force) → found `/old/`; manual SQL injection testing; database backup analysis; PDF password recovery with `pdfcrack`

All testing was performed strictly within scope, under the internship's written authorization.

## 3. Evidence

> Screenshots below are redacted to remove visible PII before publishing.

1. WHOIS — `whois-redacted.png`
2. Subfinder — `subfinder.png`
3. WhatWeb — `whatweb.png`
4. Nmap / Zenmap — `nmap_1.png`
5. Gobuster — `gobuster.png`, `gobuster_1.png`
6. `/old/` directory discovered — `dir_old_found.png`
7. Database backup (redacted) — `alldata-redacted.png`
8. SQL Injection — patient portal — `sql_injection_patient_portal.png`
9. Patient portal access — `pdf_access.png`

## 4. Key Findings

| ID | Finding | Severity |
|---|---|---|
| F1 | SQL Injection — Patient Portal Auth Bypass | **Critical** |
| F2 | Exposed Legacy DB Backup (`/old/`) | **Critical** |
| F3 | Weakly-Protected Patient Pathology Reports | **Critical** |
| F4 | Information Disclosure / Enumeration Surface | Informational |
| F5 | Exposed Mail and FTP Services | Informational |

**Privacy impact:** The exposed backup disclosed confidential staff personnel records and the hospital's corporate ownership information. All retrieved patient PDFs were protected by weak, crackable passwords, exposing confidential pathology results.

## 5. Recommendations

- Patch the SQL injection with parameterized queries.
- Remove `/old/`, disable directory indexing, store backups outside the webroot (encrypted).
- Replace static PDF passwords with strong, random passphrases or authenticated download links.
- Reduce the enumeration surface (legacy cPanel aliases, exposed `wp-admin`).
- Review exposed mail/FTP services against least privilege.

## Conclusion

This marks the completion of my Week 4 capstone for the NetworkWalks cybersecurity internship (Batch B084). All testing was authorized, scoped, and conducted for educational purposes only.
