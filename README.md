# Network Reconnaissance Lab

## Project Overview
A beginner cybersecurity project exploring TCP port scanning,
listening services, and basic service detection using Kali Linux
and Nmap.

## Objective
Learn how to scan localhost, identify listening TCP ports, interpret
scan results, and document network reconnaissance findings.

## Lab Environment
- Operating System: Kali Linux
- Scanning Tool: Nmap 7.99
- Local Inspection Tool: ss
- Target: 127.0.0.1 (localhost)
- Date: 12 October 2026

## Methodology

### 1. Inspect Listening TCP Sockets
Command:
`ss -lnt`

Observation:
A listening socket was observed on TCP port 1716.

### 2. Identify the Listening Process
Command:
`sudo ss -lntp | grep ':1716'`

Observation:
The socket was associated with `kdeconnectd`, PID 1308,
at the time of inspection.

### 3. Scan the Default TCP Port Set
Command:
`nmap -sT -sV --version-light -oN scan.txt 127.0.0.1`

Observation:
The host was reachable. All 1,000 TCP ports scanned were
reported closed.

### 4. Scan Port 1716 Specifically
Command:
`nmap -sT -sV --version-light -p 1716 -oN port-1716.txt 127.0.0.1`

Observation:
TCP port 1716 was open. Nmap reported the service as
`tcpwrapped`, without identifying a specific application protocol.

## Key Findings
- The initial scan checked the default 1,000 TCP ports.
- Port 1716 was outside that initial scan's reported port set.
- A separate socket inspection associated port 1716 with KDE Connect.
- The targeted scan confirmed that port 1716 accepted a TCP connection
  through localhost.
- An open port alone does not establish that a vulnerability exists.

## Limitations
- Only localhost was scanned.
- The initial scan covered 1,000 common TCP ports, not every port.
- Service detection did not identify the application protocol.
- This experiment did not test for vulnerabilities or assess exposure
  from other devices on the network.

## Lessons Learned
- Scan scope affects which ports are examined.
- Listening sockets and scan results provide complementary information.
- Service identification results require careful interpretation.
- Reconnaissance findings should be documented without overstating them.

## Ethical Scope
All scans in this project targeted my own machine at 127.0.0.1.
No third-party systems were scanned.

## Evidence
See `scan.txt` and `port-1716.txt` for the saved Nmap results.
