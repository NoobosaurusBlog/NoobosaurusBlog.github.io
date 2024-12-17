---
date: 2024-12-14
title: "Meterpreter"
tags: ["cheat sheet"]
---


## Basic Commands

Start with the essentials to get a lay of the land:

- **`help`**: Display a list of available commands (your lifeline when you're lost).
- **`sysinfo`**: Get basic system information, including OS and hostname (think of it as a "who am I dealing with?").
- **`ps`**: List running processes.
- **`kill <PID>`**: Terminate a process by its PID (because some processes just need to "go away").
- **`migrate <PID>`**: Move Meterpreter to a different process to stay under the radar.
- **`rev2self`**: Revert privileges to the original user (a "reset button" for when things get weird).

## File System Commands

For poking around the file system:

- **`ls`**: List files in the current directory.
- **`cd <path>`**: Change to a new directory.
- **`pwd`**: Print the current working directory.
- **`cat <filename>`**: Display the contents of a file.
- **`download <filename>`**: Pull a file from the target to your local machine.
- **`upload <filename>`**: Push a file to the target system.

## Network Commands

To scope out the network situation:

- **`ipconfig`**: Display network configuration (IP addresses, gateways, etc.).
- **`route`**: Show the routing table.
- **`netstat`**: View active network connections.
- **`portfwd [add/remove]`**: Set up port forwarding (e.g., local port -> remote service).
- **`getsockname`**: Identify the socket name for a connection.

## User Management Commands

Understand who you are and who else is around:

- **`getuid`**: Display the current user ID.
- **`ps`**: See running processes and their owners.
- **`getprivs`**: List the privileges available to the current user.
- **`getsystem`**: Attempt to escalate privileges to SYSTEM (good luck!).

## Persistence Commands

Stick around longer than you’re welcome:

- **`persistence`**: Enable Meterpreter persistence on the target (requires `autorun` setup).
- **`run <script>`**: Execute scripts or commands at startup.

## Shell Commands

Take a deeper dive with shell access:

- **`shell`**: Open a command prompt on the target (sometimes, old-school is best).
- **`execute -f <command>`**: Run a command on the target.
- **`background`**: Push your current session into the background to multitask.
- **`Ctrl+Z`**: Suspend the current session (don’t forget to resume it later).

## Other Commands

For the extra "James Bond" touch:

- **`use <extension>`**: Load a Meterpreter extension (e.g., `incognito`, `sniffer`).
- **`keyscan_start`**: Begin logging keystrokes (capture your target’s every typo).
- **`keyscan_dump`**: Dump the logged keystrokes.
- **`screenshot`**: Capture a screenshot of the target’s desktop.
- **`webcam_list`**: See available webcams on the target.
- **`webcam_snap`**: Take a snapshot from a webcam.
- **`hashdump`**: Dump password hashes (everyone’s favorite).
- **`timestomp <file>`**: Modify the timestamps of a file (because subtlety matters).

## Tips and Tricks

- **Migrate Smartly**: When migrating, pick a process that’s stable (e.g., `explorer.exe`) and won’t raise suspicions.
- **Background Often**: Always background your session before launching new exploits—multitasking is key.
- **Scripting is King**: Use Meterpreter scripts (`run <script>`) to automate repetitive tasks.



