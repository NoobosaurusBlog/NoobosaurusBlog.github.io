---
date: 2024-12-14
title : "SMBMap"
tags: ["cheat sheet", "smb"]
---


## Basic Syntax

```bash
smbmap -u <username> -p <password> -H <host> [options]
```

## Common Usage Examples

### Connect with Null Password

```bash
smbmap -u guest -p "" -d . -H 192.168.1.1
```

### Connect as Admin with Password

```bash
smbmap -u admin -p password123 -d . -H 192.168.1.1
```

### Execute a Command

```bash
smbmap -u admin -p password123 -d . -H 192.168.1.1 -x 'ipconfig'
```

### Connect to a Specific Drive

```bash
smbmap -u admin -p password123 -d . -H 192.168.1.1 -r 'C$'
```

### Upload a File

```bash
smbmap -u admin -p password123 -d . -H 192.168.1.1 --upload '/path/to/file.txt' 'C$\file.txt'
```

### Download a File

```bash
smbmap -u admin -p password123 -d . -H 192.168.1.1 --download 'C$\file.txt'
```

### Enumerate a Specific Share

```bash
smbmap -H 192.168.1.1 -s 'share_name'
```

### Enumerate Users

```bash
smbmap -H 192.168.1.1 --users
```

## Key Options

- **`-u <username>`**: Specify the username.
- **`-p <password>`**: Specify the password.
- **`-H <host>`**: Specify the target host.
- **`-r <share>`**: Connect to a specific share or drive.
- **`-x <command>`**: Execute a command on the target.
- **`--upload <local_file> <remote_path>`**: Upload a file to the target.
- **`--download <remote_file>`**: Download a file from the target.
- **`-s <share>`**: Enumerate a specific share.
- **`--users`**: Enumerate users on the target.
- **`-R`**: Check for shares with full permissions.
- **`-p <port>`**: Specify a port.

## When to Use SMBMap

- **Permission Audits**: Quickly identify shares with read, write, or full access permissions.
- **Command Execution**: Execute remote commands on accessible shares.
- **File Transfers**: Upload or download files directly from SMB shares.
- **User Enumeration**: Discover user accounts configured on the target system.


