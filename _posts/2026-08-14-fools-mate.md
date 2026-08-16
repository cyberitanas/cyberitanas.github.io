---
layout: post
title: "TryHackMe: [Fools Mate] Writeup"
date: 2026-08-14 10:00:00 +0000
categories: [tryhackme, writeup]
tags: [linux, privesc, web, enumeration]  # edit tags to match the room
---

> **Room:** [Room Name] — [difficulty, e.g. Easy]
> **Link:** [tryhackme.com/room/roomname](https://tryhackme.com/room/foolsmate
> **Note:** Flags are redacted below in line with TryHackMe's writeup guidelines.
> Follow along and find them yourself!

## Overview

A short intro: what the room covers, what skills it tests, and a one-line
summary of how you got from nothing to root/user.

## Enumeration

Start with your initial recon.

```bash
nmap -sC -sV -oN nmap_initial.txt 10.10.10.10
```

Explain what the scan turned up — open ports, services, versions — and what
that told you about likely attack paths.

## Initial Access

Walk through how you got a foothold. Include the commands you ran and *why*
you ran them, not just the output.

```bash
# example
curl http://10.10.10.10/some-endpoint
```

## Privilege Escalation

Same approach — show the enumeration that revealed the privesc path, then the
exploit itself.

```bash
sudo -l
```

## Flags

- User flag: `THM{redacted}`
- Root flag: `THM{redacted}`

## Lessons Learned

A few sentences on what this room taught you, or techniques you want to
remember for next time (e.g. a new linpeas trick, a CVE, a tool you hadn't
used before).
