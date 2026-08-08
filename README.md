# 🌐 Network Connectivity Testing with Telnet & Netcat

A comprehensive guide and toolkit for system administrators to test network connectivity, verify open ports, and troubleshoot firewall or service issues using **Telnet** and **Netcat (nc)**.

---

## 📋 Table of Contents

- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Telnet](#telnet)
  - [Basic Syntax](#telnet-basic-syntax)
  - [Examples](#telnet-examples)
  - [Interpreting Results](#interpreting-telnet-results)
  - [How to Exit Telnet](#how-to-exit-telnet)
  - [Installing Telnet](#installing-telnet)
  - [Common Ports to Test](#common-ports-to-test)
  - [Telnet Limitations](#telnet-limitations)
  - [Telnet Security Note](#telnet-security-note)
- [Netcat (nc)](#netcat-nc)
  - [Basic Syntax](#netcat-basic-syntax)
  - [Common Flags](#common-flags)
  - [Complete Flag Reference](#complete-flag-reference)
  - [Examples](#netcat-examples)
  - [Interpreting Results](#interpreting-netcat-results)
  - [Advanced Usage](#advanced-usage)
  - [Installing Netcat](#installing-netcat)
  - [Netcat Best Practices](#netcat-best-practices)
  - [Netcat Security Note](#netcat-security-note)
- [Telnet vs Netcat Comparison](#telnet-vs-netcat-comparison)
- [Practical Scenarios](#practical-scenarios)
- [Scripts](#scripts)
  - [Port Check Script](#port-check-script)
  - [Multi-Port Scan Script](#multi-port-scan-script)
- [Troubleshooting Guide](#troubleshooting-guide)
  - [Connection Refused](#1-connection-refused)
  - [Connection Timed Out](#2-connection-timed-out)
  - [Name or Service Not Known](#3-name-or-service-not-known)
  - [Network is Unreachable](#4-network-is-unreachable)
  - [Netcat Not Installed](#5-netcat-not-installed)
  - [Telnet Not Installed](#6-telnet-not-installed)
  - [Useful Diagnostic Commands](#useful-diagnostic-commands)
  - [Troubleshooting Flowchart](#troubleshooting-flowchart)
- [Quick Reference Cheat Sheet](#quick-reference-cheat-sheet)
- [Contributing](#contributing)
- [License](#license)

---

## Overview

When troubleshooting network issues, it's essential to determine whether a remote host is reachable and whether specific ports are open. **Telnet** and **Netcat** are two of the most widely used command-line tools for this purpose.

This guide provides:

- ✅ Step-by-step instructions for using Telnet and Netcat
- ✅ Practical real-world scenarios
- ✅ Ready-to-use shell scripts for port testing
- ✅ Comprehensive troubleshooting tips and best practices

---

## Prerequisites

- A Linux, macOS, or Windows system
- Terminal or command prompt access
- Basic understanding of TCP/UDP and port numbers
- Telnet and/or Netcat installed (see installation instructions below)

---

## Telnet

### What is Telnet?

Telnet is a network protocol and command-line tool used to establish a TCP connection to a remote host on a specific port. While originally designed for remote terminal access, it is now commonly used for **port connectivity testing**.

### Telnet Basic Syntax

```bash
telnet <hostname or IP> <port>
Test if a web server is listening on port 80:
telnet 192.168.1.10 80
Test SMTP mail server (port 25):
telnet mailserver.example.com 25
```
### Common Ports to Test

| Port | Service |
|------|---------|
| 22   | SSH     |
| 25   | SMTP    |
| 53   | DNS     |
| 80   | HTTP    |
| 110  | POP3    |
| 143  | IMAP    |
| 443  | HTTPS   |
| 993  | IMAPS   |
| 3306 | MySQL   |
| 3389 | RDP     |
| 5432 | PostgreSQL |
| 8080 | HTTP Alt |
| 8443 | HTTPS Alt |


## Netcat
What is Netcat?
Netcat (nc) is a versatile networking utility often called the "Swiss Army knife" of networking. It can read and write data across TCP and UDP connections, making it invaluable for network testing and troubleshooting. It is more versatile and powerful than Telnet for network testing.

Netcat Basic Syntax
nc -v <hostname or IP> <port>

| Flag | Description |
|------|-------------|
| `-v` | Verbose - show detailed output |
| `-z` | Zero I/O mode - scan without sending data |
| `-w <sec>` | Timeout - wait time for connection |
| `-u` | UDP mode instead of default TCP |
| `-l` | Listen mode - wait for incoming connections |
| `-p <port>` | Specify local source port |
| `-n` | Numeric only - skip DNS resolution |
| `-k` | Keep listening after client disconnects |
| `-e <cmd>` | Execute command after connection (use with caution) |
| `-q <sec>` | Quit after specified seconds of inactivity |

Test if a single port is open:
nc -zv 192.168.1.10 443

Test with a timeout (5 seconds):
nc -zv -w 5 192.168.1.10 3389
Scan a range of ports:
nc -zv 192.168.1.10 20-25
Test UDP connectivity
nc -zuv 192.168.1.10 53
Test multiple specific ports:
nc -zv 192.168.1.10 22 80 443 3306

Interpreting Netcat Results
 Successful (Port Open)
 $ nc -zv 192.168.1.10 22
Connection to 192.168.1.10 22 port [tcp/ssh] succeeded!

❌ Failed (Port Closed)
$ nc -zv 192.168.1.10 8080
nc: connect to 192.168.1.10 port 8080 (tcp) failed: Connection refused

⏳ Timed Out (Firewall Blocking)
$ nc -zv -w 5 192.168.1.10 445
nc: connect to 192.168.1.10 port 445 (tcp) failed: Connection timed out

Advanced Usage
Banner Grabbing
Identify the service running on a port:

echo "" | nc -v -w 3 192.168.1.10 22

File Transfer
Receiving side:
nc -l 9999 > received_file.txt
Sending side:
nc <receiver-IP> 9999 < file_to_send.txt

Simple Chat
Server:

nc -l 4444
Client:
nc <server-IP> 4444

Port Forwarding
nc -l 8080 | nc destination-host 80

## Netcat Best Practices
Always use -w flag to set timeouts in scripts
Use -z flag for port scanning to avoid sending data
Combine with -v for clear output
Use -n to skip DNS lookups for faster results
Be cautious with -e flag as it can be a security risk
Netcat Security Note
⚠️ Netcat is a powerful tool. Use it responsibly and only on networks and systems you are authorized to test. Unauthorized port scanning may violate laws and policies.

## Useful Diagnostic Commands

| Command | Purpose |
|---------|---------|
| `ping <host>` | Test basic connectivity (ICMP) |
| `traceroute <host>` | Trace network path |
| `nslookup <host>` | DNS lookup |
| `dig <host>` | Detailed DNS lookup |
| `ss -tlnp` | Show listening TCP ports |
| `ss -ulnp` | Show listening UDP ports |
| `netstat -tlnp` | Show listening ports (legacy) |
| `ip addr show` | Show network interfaces |
| `ip route show` | Show routing table |
| `iptables -L -n` | Show firewall rules (Linux) |
| `firewall-cmd --list-all` | Show firewall rules (firewalld) |
| `curl -v telnet://<host>:<port>` | Alternative port test using curl |

<img width="1037" height="852" alt="image" src="https://github.com/user-attachments/assets/2a0cbc2e-a507-488e-952d-373ef9688088" />
