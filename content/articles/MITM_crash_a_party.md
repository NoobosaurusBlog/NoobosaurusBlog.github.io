---
date: 2024-12-17
title: "MITM Attacks"
tags: ["articles", "mitm"]
---


# MITM Attacks: How to Crash the Party Between Alice and Bob

Man-in-the-Middle attacks (MITM) are like showing up uninvited to someone else’s private conversation, grabbing a chair, and whispering, *“Don’t mind me.”* Except, instead of tea and gossip, the stakes are passwords, credit card numbers, and the little details your digital life holds. Carol (the uninvited hacker) isn’t just listening, she’s reading, stealing, and sometimes *tweaking* what’s being said.

Today, we’ll crash this party and take a look at how Carol pulls off her tricks, why they work, and what you can do to stop her from making herself at home in your traffic.

---

## What Even Is a Man-in-the-Middle Attack?

Picture this: Alice and Bob are exchanging secrets, love letters, memes, bank details, or maybe just complaining about Carol. They think they’re communicating directly, but little do they know, Carol is sitting in the middle, reading every word, tweaking the conversation, and cackling like a villain in a bad spy movie.

In the digital world, Alice could be your laptop, Bob a website or server, and Carol a hacker lurking on your café’s Wi-Fi or corporate network. She intercepts traffic, decrypts it (sometimes), and messes with it however she pleases.

The terrifying part? This can happen to you without you realizing it, until it’s too late.

---

## How Carol Crashes the Party: Common MITM Tricks

Carol’s bag of tricks is stuffed with clever (and sometimes shockingly simple) ways to hijack your traffic. Here’s how she pulls it off:

---

### 1. Rogue Wi-Fi Access Points: Carol’s Favorite Honeytrap

Setting up a rogue Wi-Fi access point doesn’t require much more than a laptop, a coffee shop corner, and a catchy SSID like *Free\_Cafe\_WiFi* or *Starbux\_Free*. You think you’re connecting to free Wi-Fi for your overpriced latte, but you’re actually walking straight into Carol’s trap.

#### How It Works (The Tech Bit):

1. **Broadcast the Trap:** Carol uses tools like Airbase-ng to create a fake access point.

```bash
airbase-ng -e "Starbux_Guest" -c 6 wlan0mon
```

2. **Monitor the Victims:** Your device connects, trusting the familiar name. Carol now acts as the gateway to the internet.
3. **Proxy the Traffic:** With tools like **ettercap** or **mitmproxy**, Carol routes all your traffic through her machine.

```bash
bettercap -T -q -M arp:remote // // -i wlan0
```

4. **Optional Evil Fun:** Carol can inject JavaScript keyloggers, replace downloads with malware, or redirect DNS queries to phishing pages.

#### Why It’s Effective

Devices love auto-connecting to networks they recognize, and humans… well, we love free Wi-Fi.

**Defense Tip:** Always use a VPN.

---

### 2. ARP Spoofing: “Hi, I’m the Router Now”

ARP (Address Resolution Protocol) is like the phonebook for local networks, mapping IP addresses to MAC addresses. But ARP has a fatal flaw: it trusts *everyone*. Carol exploits this blind trust to impersonate the router and redirect all traffic through herself.

#### How It Works:

```bash
arpspoof -i eth0 -t 192.168.1.10 -r 192.168.1.1
```

#### Why It’s Effective

On a LAN, ARP spoofing is lightning-fast and stealthy.

**Defense Tip:** Use ARP detection tools like **Arpwatch**.

---

### 3. DNS Spoofing: Carol’s Redirection Magic

You type `bank.com` into your browser. Carol decides that’s cute and redirects you to *fak3bank.com*, a malicious clone where she harvests your login details.

#### How It Works:

```bash
tcpdump -i eth0 udp port 53
dnsspoof -i eth0 -f dns_hosts
```

Example `dns_hosts` file:
```text
133.7.133.7 google.com
```

**Defense Tip:** Use DNSSEC.

---

### 4. SSL Stripping: Downgrading You Back to 2005

You know HTTPS, the comforting padlock in your browser bar? Carol strips it away like a magician revealing a trapdoor.

#### How It Works:

```bash
bettercap -iface eth0 -caplet https-ui
```

**Defense Tip:** Use HSTS.

---

### 5. The Terrapin Attack: SSH Handshake Manipulation

The Terrapin attack, disclosed in 2023, targets vulnerabilities in the SSH protocol. Carol, with her devilish grin, manipulates the sequence numbers during the SSH handshake, playing a twisted game of digital Jenga.

#### How It Works:

1. Carol intercepts and tampers with the SSH handshake sequence numbers.
2. She forces a downgrade or disables security features like keystroke timing obfuscation.
3. This allows her to potentially exfiltrate sensitive SSH session data.

#### Why It’s Dangerous

SSH is supposed to be secure by design, but Terrapin cracks open a weakness at a fundamental level, undermining trust in encrypted sessions.

**Defense Tip:** Ensure SSH clients and servers are updated to versions patched against Terrapin vulnerabilities (e.g., OpenSSH 9.6+).

---

## Final Thoughts: How to Keep Carol Out

- Always use a VPN.
- Enable HSTS, DNSSEC, and encrypted DNS.
- Inspect SSL certificates.
- Watch for anomalies: duplicate MAC addresses, suspicious DNS redirects, or missing HTTPS.

In short: trust no one! Especially not the Wi-Fi named *Free_Cafe_WiFi*. Carol's out there, latte in hand, waiting for you to slip up. Don’t give her the satisfaction.

