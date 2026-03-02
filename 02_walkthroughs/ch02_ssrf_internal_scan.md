# SSRF — Internal Port Scan (Differential Responses)

## Target
10.0.30.19

## Objective
Intercept the message refresh request which fetches an internal resource. Use it to scan internal ports from the provided ports list and identify which port is ONLY open internally.

## External Recon (baseline)
Top-ports scan showed only:
- 22/tcp open ssh
- 80/tcp open http

This establishes that any additional responding service discovered via SSRF is **internal-only**.

## SSRF Entry Point
On the Messages dashboard, clicking **Refresh Messages** triggers:

/messages?url=http://127.0.0.1/api/users/all

Status: 200 OK

This confirms the server fetches a user-controlled URL parameter (`url=`).

## Internal Port Testing (controlled)
We used the SSRF parameter to request different localhost ports and observed response differences:

### Port 22 (control)
url=http://127.0.0.1:22

Observed:
BadStatusLine containing SSH banner:
SSH-2.0-OpenSSH_9.6p1 Ubuntu-3ubuntu13.14

Interpretation: Port open internally (and also externally).

### Port 3306
url=http://127.0.0.1:3306

Observed:
Connection refused

Interpretation: closed internally.

### Port 8080
url=http://127.0.0.1:8080

Observed:
Connection refused

Interpretation: closed internally.

### Port 8000
url=http://127.0.0.1:8000

Observed:
200 OK
Fetched 424 bytes

Interpretation: HTTP service open internally.

## Conclusion / Answer
Because port **8000** responds internally but is not exposed externally (nmap only showed 22/80), the port that is ONLY open internally is:

**8000**
