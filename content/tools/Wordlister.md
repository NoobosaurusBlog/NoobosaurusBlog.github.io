---
date: 2024-12-14
title: "Wordlister"
tags: ["tools", "script"]
---

Sometimes you just need a clean wordlist without the frills of a complicated tool. That’s where this **Wordlist Generator** comes in. It’s a simple Bash script designed to pull unique words from one or more text files, sort them, and save them neatly into a wordlist. Whether you’re prepping for a dictionary attack, building a natural language dataset, or just satisfying your curiosity, this script gets the job done quickly and efficiently.

## Why Bash?

You might be asking, why Bash? Well, there’s beauty in simplicity. This script was created to strip down the task to its essentials: no dependencies, no extra fuss, just the native power of Bash. While there are plenty of tools out there for generating wordlists, this one leans into the Unix philosophy—do one thing, and do it well.

## How It Works

The script takes one or more text files as input, extracts the words, normalizes them to lowercase, removes duplicates, sorts them, and outputs everything into a file called `wordlist.txt`. The end result? A clean, ordered list of unique words ready for your next project.

## Key Features

1. **Simple Input**: Accepts multiple text files as input.
2. **Automatic Sorting**: Ensures the wordlist is alphabetically ordered.
3. **No Dependencies**: Works out of the box with any modern Bash shell.
4. **Efficiency**: Processes files with a single command pipeline.

## Getting Started

### Installation

Just grab the script at the bottom of this page, make it executable, and you’re good to go.
Or you can get it on my github :
   ```bash
   git clone https://github.com/noobosaurus-r3x/Wordlister
   cd Wordlister
   chmod +x wordlister.sh
   ```

### Usage

The script is designed to be intuitive and easy to use. Here’s the basic syntax:

```bash
./wordlister.sh file1.txt file2.txt file3.txt
```

### What It Does

- Combines the contents of all provided text files.
- Extracts words by splitting on non-alphanumeric characters.
- Converts all words to lowercase to avoid duplicates like `Word` and `word`.
- Removes duplicates entirely.
- Outputs the results into `wordlist.txt` in the current directory.

### Example

Imagine you have two text files, `file1.txt` and `file2.txt`, and you want to generate a wordlist:

1. Run the script:
   ```bash
   ./wordlister.sh file1.txt file2.txt
   ```

2. The script processes the files and outputs:
   ```plaintext
   Created wordlist with 500 words
   ```

3. Open `wordlist.txt` to see your results.

### Notes

- If no files are provided, the script will display a usage message and exit.
- The output file is overwritten each time the script runs, so be sure to back up your previous wordlists if needed.

## The Script

For those who want a peek under the hood, here’s the full script:

```bash
#!/usr/bin/env bash
set -euo pipefail
IFS=$'\n\t'

if [ $# -eq 0 ]; then
    echo "Usage: $0 <text_file1> [<text_file2> ...]"
    exit 1
fi

wordlist="wordlist.txt"

# Process input files to extract unique words in lowercase
LC_ALL=C cat "$@" \
    | tr -c '[:alnum:]' '\n' \
    | tr '[:upper:]' '[:lower:]' \
    | sort -u > "$wordlist"

word_count=$(wc -l < "$wordlist")
echo "Created wordlist with $word_count words"
```

## Why Use This Script?

If you need a no-nonsense way to generate a wordlist, this script has you covered. It’s lightweight, fast, and doesn’t require any external tools or libraries. Whether you’re working in cybersecurity, natural language processing, or simply organizing your text data, this Bash script is a reliable companion.

## Final Thoughts

Sometimes the simplest tools are the most effective. This wordlist generator isn’t trying to be fancy; it’s just trying to do the job—and it does it well. If you’ve got improvements or ideas, feel free to tweak the script to fit your needs. After all, the best tools are the ones you make your own.


