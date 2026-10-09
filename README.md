# NETWORKWALKS-B083A-WK4-WEB-APPLICATION-PENETRATION-TEST
A full penetration test against Mediroza General Hospital

# Penetration Testing Report — Mediroza General Hospital

|**Batch:** B083 | Week 4 |
|----------------|-------|
**Target:** https://medirozahospital.com
**Engagement Type:** Black-box Penetration Test
**Duration:** 5 Days
**Conducted by:** [Your Name]
**Authorization:** Written permission granted by client for this engagement

> This assessment was conducted in a controlled, authorized educational environment as part of the NetworkWalks Cybersecurity Internship. These techniques were not and must never be applied to any system without explicit written permission from the owner.

---

## 1. Executive Summary

This report documents a black-box penetration test performed against Mediroza General Hospital's web infrastructure. The engagement identified a critical authentication vulnerability in the login mechanism, which allowed unauthorized access to a restricted portal containing confidential patient lab reports. [Add 1–2 sentences summarizing overall risk level and business impact once all milestones are complete.]

## 2. Scope and Methodology

**Scope:** Testing was limited to the target domain (medirozahospital.com) only. No social engineering, denial-of-service, or out-of-scope testing was performed, per the rules of engagement.

**Methodology:**
- Reconnaissance of the target application
- Enumeration of login behavior and error handling
- Testing for input validation weaknesses (SQL injection)
- Exploitation to demonstrate real-world impact
- Analysis of retrieved files for further data exposure
- Documentation of findings with evidence

**Tools used:** [List what you used — browser dev tools, Burp Suite, JTR/Johnny, NetworkWalks hash calculator, etc.]

## 3. Findings and Proof of Exploitation

### Finding 1: Username Enumeration via Inconsistent Error Messages
**Description:** The login form returns different error messages depending on whether a submitted username exists ("Username not found" vs. "Incorrect password"), allowing an attacker to enumerate valid accounts.

**Proof of Concept:**
| Username | Password | Response |
|---|---|---|
| `bob` | `test123` | Username not found |
| `admin` | `test123` | Incorrect password |

**Impact:** Confirms `admin` is a valid account, narrowing the attack surface for further exploitation.

---

### Finding 2: SQL Injection in Login Form (Authentication Bypass)
**Description:** The username field does not sanitize user input before passing it into a SQL query, allowing an attacker to manipulate the query logic.

**Proof of Concept:**
