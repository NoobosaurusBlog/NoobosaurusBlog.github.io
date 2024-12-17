---
date: 2024-12-16
title: "Osintagram"
tags: ["tools"]
---

Gathering OSINT (Open-Source Intelligence) from Instagram used to be straightforward—grab a GitHub tool, run it, and get results. Then Instagram’s API updates broke nearly everything, leaving most tools useless. That’s where **Osintagram** comes in: a simple script I put together to finally get Instagram OSINT working again.

I’m no developer, just someone frustrated by older tools failing in CTFs and OSINT exercises. Osintagram isn’t perfect, but it’s built to handle the updated systems Instagram uses today. Let me show you how it works and why it might save you some headaches.

## Why Osintagram?

If you’ve ever tried to scrape data from Instagram, you’ve probably hit limitations like expired session cookies or blocked API calls. Osintagram addresses these issues by:

- **Using Session Cookies**: It requires an Instagram session cookie (sockpuppet accounts recommended). This lets you sidestep some of the traditional hurdles of accessing data.
- **Focusing on Practical OSINT**: Instead of bloated features, Osintagram keeps it simple and effective—fetching user data like followers, bio, posts, and more.
- **Actually Working**: Unlike older tools that throw errors with Instagram’s new API, this one is tested against modern challenges.

## Features

- **Profile Information Retrieval**:
  - Extract usernames, full names, follower and following counts, posts, biographies, and even external website links.
  - Identify whether the account is private or verified.
- **Secure Session Management**:
  - Stores session cookies securely using encryption.
- **Straightforward Command-Line Interface**:
  - Easy-to-use commands for data extraction.
- **Randomized User Agents**:
  - Mimics browser requests to avoid detection.

## Setting It Up

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/noobosaurus-r3x/osintagram.git
   cd osintagram
   ```
2. Install dependencies:
   ```bash
   pip3 install -r requirements.txt
   ```

### Initial Configuration

Osintagram relies on an Instagram session ID. During the setup, you’ll provide this ID (from a browser cookie), and the tool will encrypt and store it securely. Use a sockpuppet account to avoid risks.

Run the setup command:

```bash
python3 osintagram.py --setup
```

This generates two files:
- `config.ini`: Stores encrypted credentials.
- `secret.key`: The encryption key for decrypting session IDs.

Now you’re ready to dive into OSINT.

## Using Osintagram

To fetch information about a specific Instagram user, run:

```bash
python3 osintagram.py -u <target_username>
```

Replace `<target_username>` with the Instagram handle you’re interested in. The tool will return:
- Profile stats (followers, following, posts).
- Account details (bio, verification status, links).

## The Tech Behind the Tool

Osintagram’s architecture is straightforward but effective:

- **Session Management**:
  - Handles login sessions securely using encrypted cookies.
- **Randomized User Agents**:
  - Rotates user agents to simulate real browser activity.
- **Output Handling**:
  - Formats fetched data for clarity using `rich` for visually appealing results.

### Key Scripts

- **`osintagram.py`**: The main script that orchestrates everything.
- **`setup.py`**: Encrypts and stores session cookies during the initial setup.
- **`instagram_api_handler.py`**: Handles API interactions to fetch profile data.
- **`output_manager.py`**: Manages formatting and presenting results.
- **`encryption_utils.py`**: Encrypts and decrypts session credentials.
- **`user_agent_manager.py`**: Generates randomized user agents.

## Limitations and Ethical Considerations

- **Limitations**:
  - Requires manual extraction of session cookies.
  - Cannot bypass Instagram’s rate limits or restrictions.
- **Ethical Use**:
  - Only use this tool on accounts you have permission to analyze. Misuse of OSINT tools can lead to legal consequences.

## Credits

Osintagram is inspired by [Toutatis](https://github.com/megadose/toutatis) by Palenath. Huge thanks to Palenath for blazing the trail in Instagram OSINT tooling.

## Final Thoughts

Osintagram isn’t trying to reinvent the wheel—it’s here to fill the gaps left by older tools that couldn’t keep up with Instagram’s changes. Whether you’re an OSINT enthusiast or a researcher, it’s a reliable companion for extracting and analyzing Instagram profile data.

Give it a shot, adapt it to your needs, and let me know if you run into issues.


