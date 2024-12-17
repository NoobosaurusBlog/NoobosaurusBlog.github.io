---
date: 2024-12-14
title: "smbclient"
tags: ["cheat sheet", "smb"]
---

**smbclient** is a command-line tool that allows you to interact with SMB (Server Message Block) file shares. Whether you’re uploading files, listing directories, or troubleshooting network shares, this tool is your go-to for SMB.

## Basic Usage

To connect to an SMB file share, use the following syntax:

```bash
smbclient //server/share [options]
```

- Replace **`server`** with the hostname or IP address of the server hosting the file share.
- Replace **`share`** with the name of the file share.

Once connected, you will be prompted for credentials. After successful authentication, a command prompt will allow you to interact with the share.

## Common Options

- **`-U <username>`**: Specify the username to use for authentication.
- **`-W <workgroup>`**: Specify the domain or workgroup.
- **`-I <IP address>`**: Directly specify the server's IP address.
- **`-p <port>`**: Specify the port (default is 445).
- **`-d <debug level>`**: Set the debug level for verbose output.
- **`-N`**: Suppress the password prompt (useful for guest accounts).

## Available Commands

Once connected, the following commands allow you to interact with the file share:

- **`ls`**: List files and directories in the current directory.
- **`cd <directory>`**: Change to a different directory.
- **`pwd`**: Print the current working directory.
- **`put <file>`**: Upload a file to the share.
- **`get <file>`**: Download a file from the share.
- **`mput <files>`**: Upload multiple files.
- **`mget <files>`**: Download multiple files.
- **`rm <file>`**: Delete a file.
- **`mkdir <directory>`**: Create a new directory.
- **`rmdir <directory>`**: Remove a directory.
- **`exit`**: Disconnect from the share and exit smbclient.

## Examples

### List Files in a Share

```bash
smbclient //server/share -c ls
```

### Connect with a Specific Username and Password

```bash
smbclient //server/share -U username%password
```

### Connect Using an IP Address and Port

```bash
smbclient //server/share -I 192.168.1.100 -p 139
```

### Upload a File

```bash
smbclient //server/share -c "put /path/to/local/file"
```

### Download a File

```bash
smbclient //server/share -c "get /path/to/remote/file"
```

### Create a New Directory

```bash
smbclient //server/share -c "mkdir newdirectory"
```

## When to Use smbclient

- **Quick Access**: Need to interact with a file share without mounting it? smbclient gives you immediate access.
- **Testing Permissions**: Check which directories and files are accessible under different credentials.
- **File Operations**: Download, upload, or manage files on SMB shares.
- **Debugging**: Troubleshoot network shares with verbose output using `-d`.



