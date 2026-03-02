# Lessons Learned — Chapter 10 (Server-Side Attacks Part 1)

## General
- Start with an attack-surface map (ports, routes, parameters) before testing payloads.
- Change one variable at a time and record raw outputs immediately.
- Stop once you confirm impact and capture evidence.

## Path Traversal
- “Preview / download / image / logo” endpoints are high risk when they accept a file parameter.
- Confirm with a safe read (e.g., `/etc/passwd`) before targeting sensitive files.
- `/proc/self/environ` is high value because it exposes runtime environment variables and potential secrets.

## SSRF
- Refresh/fetch functions often hide server-side HTTP calls (internal resources).
- SSRF can be used as an internal port scanner via differential behavior:
  - banner / protocol mismatch
  - connection refused
  - 200 OK / bytes fetched
- Compare SSRF-discovered ports to external nmap results to prove “internal-only” exposure.

## SSTI (Jinja2)
- Confirm SSTI with arithmetic (`{{7*7}}`).
- Then validate access to Python internals (`self.__init__.__globals__`, `__builtins__`, `__import__`).
- Achieve RCE only as far as needed for the objective; avoid unnecessary commands.

## Tooling Notes
- WSL2 + Canary + WSLg can be unstable for heavy GUI tools.
- A CLI-first workflow (nmap/curl + browser DevTools) still succeeds when GUIs fail.
