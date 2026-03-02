# Lab Environment

## Host System
Windows 11 Canary (26200.x)

## Linux Environment
WSL2 Kali Linux

## VPN
OpenVPN (tun0 interface verified before each lab)

## Tooling Strategy
- CLI-first approach (nmap, curl)
- Firefox (WSLg)
- Burp optional (avoided due to WSLg instability in previous labs)

## Methodology Rules
1. Verify VPN + reachability
2. Establish baseline with minimal scan
3. Identify attack surface before exploitation
4. Change one variable at a time
5. Capture raw outputs
6. Stop after confirming impact
