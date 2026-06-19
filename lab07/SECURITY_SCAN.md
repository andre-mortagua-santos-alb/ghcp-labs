# Security Vulnerability Scan Report

**Generated:** 2026-06-19  
**SBOM:** sbom.xml (CycloneDX 1.6)  
**Scanner:** Manual CVE analysis against NIST NVD + pip-audit

---

## Summary

| Metric | Count |
|--------|-------|
| Total packages scanned | 4 |
| CRITICAL | 2 |
| HIGH | 1 |
| MEDIUM | 1 |
| LOW | 2 |
| Clean | 0 |

> ⚠️ **Merge blocked** — CRITICAL findings present. Remediate before PR approval.

---

## Findings

### 1. pyyaml — CRITICAL (CVE-2017-18342)

- **Current version:** unpinned (resolves at install time)
- **CVE:** CVE-2017-18342
- **Severity:** CRITICAL (CVSS 9.8)
- **Description:** `yaml.load()` without an explicit `Loader` argument allows
  deserialisation of arbitrary Python objects, enabling remote code execution.
- **Affected versions:** < 5.1
- **Recommended action:** Pin to `pyyaml>=6.0.2` and audit all `yaml.load()` calls
  — replace with `yaml.safe_load()`.

---

### 2. pyyaml — CRITICAL (CVE-2020-14343)

- **Current version:** unpinned
- **CVE:** CVE-2020-14343
- **Severity:** CRITICAL (CVSS 9.8)
- **Description:** Incomplete fix for CVE-2017-18342. The `FullLoader` introduced
  as the safe default in 5.1 was itself exploitable in versions < 5.4.
- **Recommended action:** Pin to `pyyaml>=6.0.2` (resolves both CVEs).

---

### 3. requests==2.18.0 — HIGH (CVE-2018-18074)

- **Current version:** 2.18.0 (pinned, ~8 years old)
- **CVE:** CVE-2018-18074
- **Severity:** HIGH (CVSS 7.5)
- **Description:** When following a redirect from an HTTPS URL to an HTTP URL,
  the `Authorization` header is forwarded to the new host, leaking credentials.
- **Recommended action:** Upgrade to `requests>=2.32.0`.

---

### 4. requests==2.18.0 — MEDIUM (CVE-2023-32681)

- **Current version:** 2.18.0
- **CVE:** CVE-2023-32681
- **Severity:** MEDIUM (CVSS 6.1)
- **Description:** `Proxy-Authorization` header is forwarded to the destination
  server when a redirect crosses scheme or host boundaries.
- **Recommended action:** Upgrade to `requests>=2.31.0` (covered by >=2.32.0).

---

### 5. bcrypt — LOW (supply-chain risk)

- **Current version:** unpinned
- **CVE:** None known
- **Severity:** LOW
- **Description:** No CVEs in current releases, but unpinned versions may pull
  in future vulnerable releases automatically.
- **Recommended action:** Pin to `bcrypt>=4.1.3`.

---

### 6. pytest — LOW (supply-chain risk)

- **Current version:** unpinned
- **CVE:** None known
- **Severity:** LOW
- **Description:** Testing dependency with no known CVEs. Unpinned in production
  builds is a reproducibility and supply-chain risk.
- **Recommended action:** Pin to `pytest>=8.2.0`.

---

## Remediation Plan

### Immediate (before merge — CRITICAL/HIGH)

```txt
# requirements.txt — remediated
pytest>=8.2.0
bcrypt>=4.1.3
pyyaml>=6.0.2
requests>=2.32.0