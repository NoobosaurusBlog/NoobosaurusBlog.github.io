---
date: 2024-12-15
title: "nmap"
tags: ["cheat sheet"]
---

## Basic Syntax

```bash
nmap <target IP>
nmap -sT -sS -Pn -v 10.10.10.10
sudo nmap -A -sS -Pn 10.10.10.10
sudo nmap -sV -sT -O -p- -vv --script vulners 10.10.10.10
```

## Common Flags

### Scan Types

- **`-sT`**: Perform a TCP connect scan.
- **`-sU`**: Perform a UDP scan.
- **`-sS`**: Perform a SYN scan ("Stealth Scan").
- **`-Pn`**: Skip pinging the target.
- **`-sn`**: Host discovery without scanning ports.
- **`-A`**: Enable aggressive scan options.

### Advanced Features

- **`-p <PORT>`**: Scan specific ports.
- **`-p-`**: Scan all 65,535 ports.
- **`-sV`**: Detect services and versions running on the target.
- **`-O`**: Detect the operating system.
- **`-v`, `-vv`, `-vvv`**: Set verbosity levels.
- **`--script vuln`**: Run vulnerability scripts.
- **`--script vulners`**: Use vulners scripts for CVE-based scanning.
- **`--script=http-enum`**: Act like Nikto to enumerate HTTP resources.

## Output Formats

- **`-oN`**: Normal text output, best for human-readable logs during manual reviews.
- **`-oX`**: XML output, ideal for automated tools or integrations that require structured data.
- \`\`: Greppable output, useful for scripting and quickly filtering resulst with tools like `grep`.
- **`-oA`**: Generate all three formats at once, providing maximum flexibility for further analysis or reporting.

## SMB Scripts

### Enumerate Security Mode

```bash
nmap -p445 --script smb-security-mode 192.168.1.1
```

### Enumerate Sessions

```bash
nmap -p445 --script smb-enum-sessions 192.168.1.1
nmap -p445 --script smb-enum-sessions --script-args smbusername=administrator,smbpassword=password 192.168.1.1
```

### Enumerate Shares

```bash
nmap -p445 --script smb-enum-shares 192.168.1.1
nmap -p445 --script smb-enum-shares --script-args smbusername=administrator,smbpassword=password 192.168.1.1
```

### Enumerate Shares with Listing

Listing shares and their contents can reveal valuable information about a system, such as misconfigured permissions or sensitive files stored in shared directories. This is especially important during audits or penetration tests to identify potential security gaps.

```bash
nmap -p445 --script smb-enum-shares,smb-ls --script-args smbusername=administrator,smbpassword=password 192.168.1.1
```

### Enumerate Users

```bash
nmap -p445 --script smb-enum-users --script-args smbusername=administrator,smbpassword=password 192.168.1.1
```

### Enumerate Stats

```bash
nmap -p445 --script smb-enum-stats --script-args smbusername=administrator,smbpassword=password 192.168.1.1
```

### Enumerate Domains

```bash
nmap -p445 --script smb-enum-domains --script-args smbusername=administrator,smbpassword=password 192.168.1.1
```

### Enumerate Groups

```bash
nmap -p445 --script smb-enum-groups --script-args smbusername=administrator,smbpassword=password 192.168.1.1
```

## SSH Scripts

### Enumerate Algorithms

```bash
nmap 192.168.1.1 -p 22 --script ssh2-enum-algos
```

### Enumerate Host Keys

```bash
nmap 192.168.1.1 -p 22 --script ssh-hostkey --script-args ssh_hostkey=full
```

### Enumerate Authentication Methods

```bash
nmap 192.168.1.1 -p 22 --script ssh-auth-methods --script-args="ssh.user=admin"
```



