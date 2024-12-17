---
date: 2024-12-15
title: "redflagger"
tags: ["tools", "script", "bash"]
---

Daily domain reports are a treasure trove for cybersecurity analysts, but collecting and organizing them can quickly become tedious. That’s where **RedFlagger** comes in. This lightweight Bash script automates the process of downloading and aggregating reports from [Red Flag Domains](https://dl.red.flag.domains/daily/). It’s simple, efficient, and built to save time—whether you’re sifting through a few recent reports or analyzing a year’s worth of data.

## The Backstory

This project started as a bit of a joke. My friend **lil-doudou** had written an excellent Python tool called [NewRedflag](https://github.com/lil-doudou/NewRedflag) to handle domain report aggregation, but he’s also a massive Bash enthusiast. So, as a playful nod to his love for scripting, I decided to rewrite the functionality in Bash—simpler, lighter, and arguably more fun (depending on your feelings about shell scripts).

## What Does RedFlagger Do?

RedFlagger streamlines the process of collecting domain reports. Instead of manually navigating the Red Flag Domains website and downloading reports one by one, you can use RedFlagger to:

- Fetch the latest report.
- Download reports from a specific range of dates.
- Aggregate all available reports into one file for easier analysis.

It’s a no-frills script that prioritizes functionality and flexibility.

## How Does It Work?

RedFlagger fetches reports directly from the Red Flag Domains website by parsing the daily directory. It uses simple Bash commands like `curl` to download files and aggregates them into a single output file for easy handling. If you’re running a quick analysis or building a dataset for long-term research, this script has you covered.

### Key Features:

1. **Custom Date Ranges**: Specify a range of days to download only the reports you need.
2. **All-Inclusive Downloads**: Grab every report available with a single command.
3. **Custom Output Files**: Aggregate data into a file of your choice instead of dealing with multiple separate files.

## Why Use RedFlagger?

RedFlagger is built for simplicity and speed. It doesn’t aim to replace more advanced tools but instead provides a lightweight option for users who need quick, automated access to domain reports. If you find yourself regularly pulling data from Red Flag Domains, RedFlagger can:

- Save time by automating the download process.
- Ensure reports are organized and aggregated for easier analysis.
- Provide flexible options for handling specific dates or all available data.

Whether you’re an analyst tracking malicious domains or a researcher building a threat intelligence dataset, RedFlagger can fit seamlessly into your workflow.

## Getting Started

### Installation

RedFlagger is a standalone Bash script, so there’s no complicated setup. Here’s how to get started:

1. Download the script:
   ```bash
   git clone https://github.com/noobosaurus-r3x/redflagger
   cd redflagger
   chmod +x redflagger.sh
   ```

2. Make sure `curl` is installed on your system:
   ```bash
   sudo apt install curl
   ```

### Usage

The script provides several options to customize your downloads. Here’s the basic syntax:

```bash
./redflagger.sh [--latest|--days num] [--all] [--output filename]
```

### Options

- `--latest` or `-l`: Downloads the report from 1 day ago.
- `--days num` or `-d num`: Downloads the report from `num` days ago.
- `--all` or `-a`: Downloads all available reports.
- `--output filename` or `-o filename`: Specifies the output file to store the downloaded reports. Defaults to `output.txt` if no filename is provided.

### Examples

Here are a few practical ways to use RedFlagger:

1. **Download the latest report**:
   ```bash
   ./redflagger.sh -l
   ```

2. **Download all reports available since 3 days ago**:
   ```bash
   ./redflagger.sh -d 3 -a -o my_file.txt
   ```

3. **Download a specific day’s report**:
   ```bash
   ./redflagger.sh -d 5 -o report_5days_ago.txt
   ```

4. **Download all reports into a custom file**:
   ```bash
   ./redflagger.sh -a -o all_reports.txt
   ```

## Limitations and Room for Improvement

RedFlagger is intentionally simple, but it’s not without its limitations. Here are a few areas where it could be expanded or improved:

- **Error Handling**: While the script includes basic error checks, it could provide more detailed feedback when something goes wrong (e.g., network issues or missing reports).
- **Parallel Downloads**: Adding support for downloading multiple reports simultaneously could speed up large fetches.
- **Advanced Filtering**: Options for filtering by domain type or metadata could make the tool even more powerful.

If you’re interested in extending RedFlagger, feel free to fork it and make it your own.

## Final Thoughts

RedFlagger is a small, straightforward tool designed to make life easier for anyone working with Red Flag Domains. It doesn’t try to do everything but focuses on doing one thing well: fetching and aggregating domain reports quickly and efficiently.

Whether you’re doing threat research, building datasets, or just exploring the domain data available, RedFlagger is a lightweight addition to your toolbox. And let’s not forget—it’s also a fun jab at my friend’s Python-first approach. If you’ve got ideas for improvements or run into any issues, don’t hesitate to reach out or fork the project. Happy aggregating!


