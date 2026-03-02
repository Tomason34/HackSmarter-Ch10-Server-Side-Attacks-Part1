x# HackSmarter Chapter 10 — Server-Side Attacks (Part 1)

This repo contains **raw command evidence** and **step-by-step walkthroughs** for Chapter 10 server-side vulnerabilities completed using a methodology-first approach.

No screenshots included — evidence is captured as **requests + outputs** and **repro steps**.

---

## Contents

- `00_scope/` — environment + targets
- `01_recon/` — nmap summaries per challenge
- `02_walkthroughs/` — detailed walkthroughs (report-ready)
- `03_evidence/` — raw requests + outputs (copy/paste evidence)
- `99_summary/` — lessons learned

---

## Challenges Completed

1. **Path Traversal → /proc/self/environ read**
   - Confirmed traversal via `/etc/passwd`
   - Retrieved `MEMORY_PRESSURE_WATCH` from `/proc/self/environ`

2. **SSRF → Internal port scanning**
   - Identified SSRF parameter in message refresh (`url=...`)
   - Used SSRF differential responses to identify **internal-only open port**

3. **SSTI (Jinja2) → RCE**
   - Confirmed SSTI via `{{7*7}}`
   - Escalated to RCE and executed `pwd`

---

## Methodology

1. VPN up (`tun0`) + ping target
2. Quick scan: `nmap --top-ports 1000`
3. Full scan if needed: `nmap -p-`
4. App mapping first (find the exact endpoint + parameter)
5. Test one hypothesis at a time
6. Capture raw evidence
7. Stop once objective is met
