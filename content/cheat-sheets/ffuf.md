---
date: 2024-12-15
title: "ffuf"
tags: ["cheat sheet", "fuzzing"]
---

**FFUF** (Fuzz Faster U Fool) is a fast and flexible web fuzzer that helps penetration testers and security researchers discover directories, files, parameters, and more.

## Basic Syntax

```bash
ffuf -c -w path/to/wordlist -u https://target_url/FUZZ
```

### Examples

```bash
# Filter responses with a content size of 4242 bytes
ffuf -w /path/to/vhost/wordlist -u https://target_url/ -H "Host: FUZZ" -fs 4242

# Filter responses with a 401 status code
ffuf -w /path/to/values.txt -u https://target_url/script.php?valid_name=FUZZ -fc 401

# Filter 401 responses and fuzz passwords in a POST request
ffuf -w /path/to/postdata.txt -X POST -d "username=admin\&password=FUZZ" -u https://target_url/login.php -fc 401
```

## Common Flags

- **`-c`**: Enable colorized output.
- **`-maxtime`**: Set the maximum runtime for the process in seconds.
- **`-p`**: Set a delay between requests (e.g., `0.1` seconds).
- **`-v`**: Verbose output.
- **`-t`**: Number of threads (default is 40).
- **`-mc`**: Match specific HTTP status codes (e.g., `200`, `301`, `403`, or `all`).
- **`-fc`**: Filter out responses by HTTP status codes.
- **`-w`**: Specify the wordlist path.
- **`-u`**: Define the target URL.
- **`-s`**: Enable silent mode.
- **`-recursion`**: Enable recursive fuzzing.
- **`-r`**: Follow redirects.
- **`-o`**: Output results to a file.
- **`-of`**: Specify output format (e.g., `json`, `html`, `csv`, `all`).
- **`-b`**: Include cookies in the request.

## Examples

```bash
# Match all responses, filter 42-byte answers, output colored and verbose
ffuf -w wordlist.txt -u https://example.org/FUZZ -mc all -fs 42 -c -v

# Fuzz host headers and show only status 200 responses
ffuf -w hosts.txt -u https://example.org/ -H "Host: FUZZ" -mc 200

# Fuzz the `name` field in a POST request with JSON data, filter responses containing "error"
ffuf -w entries.txt -u https://example.org/ -X POST -H "Content-Type: application/json" \
-d '{"name": "FUZZ", "anotherkey": "anothervalue"}' -fr "error"

# Use two wordlists for parameter and value fuzzing, match responses containing "VAL"
ffuf -w params.txt:PARAM -w values.txt:VAL -u https://example.org/?PARAM=VAL -mr "VAL" -c
```

## Tips and Tricks

- **Interactive Mode**: Press `Enter` while FFUF is running to access interactive features, such as reconfiguring filters or saving the state.
- **Multiple Payloads**: Use the `FUZZ` keyword multiple times in a URL (e.g., `https://example.org/path/FUZZ/another_path/FUZZ`).
- **Variables in URLs**: Specify payload locations using variables (e.g., `https://example.org/path/{var1}/another_path/{var2}`).




