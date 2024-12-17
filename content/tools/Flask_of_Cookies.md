---
date: 2024-12-15
title: "FlaskOfCookies"
tags: ["tools", "CTF", "Flask"]
---

Flask web applications are clever beasts, storing session data client-side in cookies. It’s convenient for developers, but it can also be a security rabbit hole if you’re not careful. That’s why I put together **FlaskOfCookies**, a tool to help you decode, encode, and (if necessary) brute-force Flask session cookies.

To be clear, this isn’t entirely my invention. It started because I hit a wall on a **Root-Me challenge**, I couldn’t get it done with **noraj’s tool** (props to Alexandre Zanni for his great work). So, I decided to rework it, adding my own spin to tackle the issue. This tool is for anyone who’s curious about Flask’s session cookies, whether you’re debugging, testing, or just poking around.

## Why Session Cookies Matter

Session cookies in Flask encode data into a compact, URL-safe string. They’re handy for keeping track of users or passing small pieces of data between the client and server. But they also mean your data sits in plain sight. If you’re not careful with what you store—or if your secret key isn’t strong—those cookies can tell stories you’d rather keep quiet.

## What Does FlaskOfCookies Do?

### Decoding Cookies

FlaskOfCookies can crack open a Flask session cookie and show you the contents. If you have the secret key, it’ll reconstruct the original session data. Without the key, it’ll still give you a peek at the encoded structure. This is helpful for:

- Checking if sensitive information is leaking.
- Testing whether session data is being properly secured.

### Encoding Cookies

Need to create a Flask-compatible session cookie? FlaskOfCookies takes a Python dictionary and a secret key as input and spits out a session cookie. This is handy if you’re:

- Debugging session handling in your app.
- Seeing how different data structures get encoded.

### Brute-Forcing Secret Keys

If you don’t know the secret key, FlaskOfCookies can try to guess it for you. Just supply a wordlist, and the tool will hammer away until it finds a match (or gives up). This isn’t a feature for cracking into random apps; it’s a wake-up call to use strong, random keys. If you’re using “password123” for your Flask secret, consider yourself warned.

## How It Works

FlaskOfCookies is built on Flask’s session-handling mechanisms and the **itsdangerous** library, which Flask uses under the hood. It aligns with Flask’s default behavior, including the `cookie-session` salt, to make sure the results match what Flask itself would produce.

Here’s the general flow:

1. **Decoding**: The tool parses the encoded cookie value, optionally verifying it against a provided secret key.
2. **Encoding**: It serializes a Python dictionary into a session cookie using Flask-compatible methods.
3. **Brute-Forcing**: Tries every key in your wordlist to find the one that correctly decodes the cookie.

It’s straightforward, with clear error messages and input validation to keep things manageable.

## Why Use FlaskOfCookies?

Honestly, this is more of a “because I had to” kind of tool. After struggling with the Root-Me challenge and realizing noraj’s tool wasn’t working for me, I figured I’d make something myself. FlaskOfCookies won’t win awards, but it’s lightweight, easy to use, and gives you insight into how Flask manages session cookies. Whether you’re a Flask developer or a security researcher, it can help you:

- Learn how session cookies work.
- Test your app for key management flaws.
- Debug session-related bugs.

## Getting Started with FlaskOfCookies

First, make sure you have Python 3.x installed. You’ll also need Flask and itsdangerous:

```bash
pip install Flask itsdangerous
```

Then, grab FlaskOfCookies from the repository:

```bash
git clone https://github.com/noobosaurus-r3x/FlaskOfCookies
cd FlaskOfCookies
```

Alternatively, you can download the `FOC.py` script directly.

## What You Can Do With It

Here’s a quick guide to the tool’s commands:

### Decode a Session Cookie

If you know the secret key:
```bash
python3 FOC.py decode -s '<secret_key>' -c '<cookie_value>'
```

Without the key, you can still see the structure:
```bash
python3 FOC.py decode -c '<cookie_value>'
```

### Encode a Session Cookie

To create a new session cookie:
```bash
python3 FOC.py encode -s '<secret_key>' -t "{'username':'admin','role':'superuser'}"
```

### Brute-Force the Secret Key

To test key strength with a wordlist:
```bash
python3 FOC.py bruteforce -c '<cookie_value>' -w '<path_to_wordlist>'
```

## Final Thoughts

FlaskOfCookies isn’t groundbreaking, but it’s a practical little tool for anyone exploring Flask session cookies. Whether you’re trying to figure out how they work, testing your app’s security, or debugging a frustrating challenge, it’ll save you some time.

Remember, this started as a personal project to solve a specific problem, so don’t expect perfection. That said, I hope it’s useful—and if you think of ways to improve it, feel free to fork the repo and go wild. You can find it [here](https://github.com/noobosaurus-r3x/FlaskOfCookies).
