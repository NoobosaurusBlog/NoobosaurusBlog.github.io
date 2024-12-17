---
date: 2024-12-16
title: "InspecTor"
tags: ["tools", "tor"]
---

## InspecTor: A Streamlined Tool for Website Metadata Extraction

Pulling metadata from websites was once a straightforward task. You could hit a few URLs, scrape the required data, and move on. However, with the rise of dynamic content, Tor-hidden services (.onion domains), and increasing anonymity concerns, the process became far more complex. InspecTor is a command-line tool I developed to address these challenges. It simplifies metadata extraction from websites, including Tor services, while preserving user anonymity.

To clarify, I’m not a professional developer, just someone who needed a functional solution when existing tools fell short. Most scrapers I tried either broke on .onion domains or failed to process JavaScript-heavy pages. I created InspecTor to extract emails, links, images, and other relevant data without exposing my IP address. While it’s not perfect, it works and might save you some headaches too.

---

### What Makes InspecTor Stand Out?

InspecTor focuses on three core capabilities:

1. **Metadata Extraction**: It retrieves emails, phone numbers, links, images, and other exposed data from websites.
2. **Tor Support**: Requests are routed through the Tor network, enabling anonymous access to .onion domains and privacy-sensitive sites.
3. **Dynamic Content Handling**: By leveraging Selenium, InspecTor processes JavaScript-heavy pages that traditional scrapers typically ignore.

Combined with multithreading for concurrent URL processing, InspecTor offers an efficient way to gather metadata while avoiding flags or blocks.

---

### Key Features

- **Anonymous Scraping**: Routes all requests through the Tor network for IP anonymity and seamless .onion domain access.
- **Dynamic Content Support**: Processes JavaScript-dependent pages using Selenium.
- **Targeted Metadata Extraction**: Retrieve specific fields like emails, phone numbers, images, and links.
- **Concurrent Processing**: Multithreading allows simultaneous scraping of multiple URLs for improved speed.
- **Flexible Output Formats**: Export results to JSON, SQLite, or human-readable formats.
- **Configurable Options**: Adjust threading, output fields, SSL verification, and more.

---

### Setting Up InspecTor

#### 1. Clone the Repository
```bash
git clone https://github.com/noobosaurus-r3x/InspecTor.git
cd InspecTor
```

#### 2. Install Dependencies
```bash
pip install -r requirements.txt
```

#### 3. Install Tor
Ensure Tor is installed and running to route requests.
```bash
sudo apt update
sudo apt install tor
sudo systemctl start tor
```

#### 4. Set Up Selenium (Optional for Dynamic Content)
Install Chrome and ChromeDriver. Ensure ChromeDriver matches your browser version.

---

### Using InspecTor

#### Extract Metadata from Specific URLs
Provide single or multiple URLs:
```bash
python3 InspecTor.py -u https://example.com https://example.onion
```

#### Process a File of URLs
Input a list of targets from a file:
```bash
python3 InspecTor.py -f urls.txt
```

#### Force Tor for All Traffic
Route all requests through Tor, even for non-.onion domains:
```bash
python3 InspecTor.py -u https://example.com --force-tor
```

#### Save Results to JSON or SQLite
Export metadata to a file or database:
```bash
python3 InspecTor.py -u https://example.onion -o metadata.json
python3 InspecTor.py -u https://example.onion --database metadata.db
```

#### Extract Specific Fields
Focus on targeted data:
```bash
python3 InspecTor.py -u https://example.onion --fields emails links -o contact_info.json
```

#### Handle JavaScript Content
Enable Selenium for scraping JavaScript-dependent pages:
```bash
python3 InspecTor.py -u https://example.onion --use-selenium
```

#### Example Commands
- Extract everything:
  ```bash
  python3 InspecTor.py -u https://example.onion --extract-all -o all_metadata.json
  ```
- Grab emails and phone numbers:
  ```bash
  python3 InspecTor.py -u https://example.com --fields emails phone_numbers -o contact_info.json
  ```
- Ignore SSL certificate issues:
  ```bash
  python3 InspecTor.py -u https://example.onion --no-verify-ssl --human-readable
  ```

---

### Output Formats
- **JSON**: Structured file output for further processing.
- **SQLite**: Database storage for querying and analysis.
- **Human-Readable**: Clean, formatted text output for quick reviews.

---

### Notes on Tor and Dynamic Content
- **Tor Requirements**: Tor must be running on `127.0.0.1:9050`.
- **Selenium Setup**: Ensure Chrome and ChromeDriver versions match for dynamic content scraping.
- **SSL Verification**: Enabled by default; use `--no-verify-ssl` to bypass invalid certificates.
- **Threading**: Control parallel processing with `--max-workers` for faster scraping.

---

### Why I Built InspecTor

InspecTor was born out of necessity. Existing tools often fell short when handling .onion domains or JavaScript-heavy pages. As someone who needed a simple and effective way to extract metadata for OSINT investigations, website audits, and cybersecurity research, I created InspecTor.

It’s not perfect, but it works. If it helps you solve a problem, that’s great. If you find ways to improve it, even better.

--
