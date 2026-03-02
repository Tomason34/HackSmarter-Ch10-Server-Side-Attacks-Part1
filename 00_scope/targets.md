# Targets Used — Chapter 10

## Challenge 1 — Path Traversal
Target: 10.0.30.19
Service: Flask (Werkzeug 3.1.5)
Objective: Retrieve /proc/self/environ and extract MEMORY_PRESSURE_WATCH.

Credentials provided:
- admin : password1
- tony : basketball
- johnny : dolphin
- student : liverpool

---

## Challenge 2 — SSRF Internal Port Scan
Target: 10.0.30.19
Service: Flask message dashboard
Objective: Identify port only open internally via SSRF.

Confirmed internal-only port:
8000

---

## Challenge 3 — SSTI → RCE
Target: 10.1.82.253
Service: Flask badge generator
Objective: Achieve RCE and run `pwd`.

Command output:
 /home/ubuntu
