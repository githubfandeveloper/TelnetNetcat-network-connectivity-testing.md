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

## Common Ports to Test
