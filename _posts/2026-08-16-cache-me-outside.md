---
layout: post
title: "TryHackMe: [Cache Me Outside] Writeup"
date: 2026-08-16 
categories: [tryhackme, writeup,]
tags: [OSINT]  
---

> **Room:** [Cache Me Outside] — [Medium]
> **Link:** [tryhackme.com/room/roomname](https://tryhackme.com/room/cachemeoutside


## Overview

Years after walking away from the scene, a retired hacker has left pieces of his identity scattered across the open internet.

At first glance, it looks like nothing more than a leaked conversation screenshot. But buried in that image is the first thread of a much larger trail. Public profiles, forgotten details, and small mistakes begin to connect into something more deliberate.

Someone wanted this person found.

Your Assignment
You are an OSINT investigator tasked with identifying the retired hacker and tracing the clues he left behind.

Start with the conversation screenshot, follow his online presence, connect the exposed details, and use the final evidence to determine where the trail ends.
![Task Image](/intial/git_1.png)
I first read the task at hand and tried to gather as many clues as possible.

Within the picture, I notice a link which I follow.

Within the link is a Komoot profile. The first things that catch my eye are the GitHub link, 370 followers which can potentially be traced, and a description that matches the Discord conversation I read earlier (outdoors, ex-hacker, running, etc.).

Within the follower list, there seem to be a lot of filler/fake profiles, possibly to obfuscate his trail. However, some real-looking names are present. I go through a handful of these but nothing pans out, so I move on rather than chase every one down.

## Pivot 1: GitHub

I follow the GitHub link, which presents me with a single pinned repo, 84 followers, and "Jim Lee Security Consulting" pinned to his workplace on his GitHub profile (could be another trail to follow down).

I first choose to examine the repo info. It seems he joined GitHub on April 16, 2026, and created his first repo on April 16.

Looking within the GitHub repo forks, I find this:

![GitHub repo forks](/assets/git_1.png)

This makes me think his clients possibly communicate via GitHub, which makes this a good source of info about him, noted and pinned for later.

Looking at Jim Lee's commit history, I find a deleted fun fact that used to exist within his README:

![Deleted fun fact in README](/assets/git_2.png)

These are the two accounts associated with the commits:

![Commit account 1](/assets/git_3.png)

![Commit account 2](/assets/git_4.png)

Looking further, I check the "issues" section of his readme, which reveals more communication with Jim Lee:

![Issues section communication](/assets/git_5.png)

Going through all of these, though, I wasn't able to find much personal info. So I go back to his initial commit and add `.patch` to the URL to pull the full header, a neat trick that exposes the raw commit metadata GitHub normally hides. This gives us our first piece of submittable info:

https://github.com/jiml33t/jiml33t/commit/7b2c8e0a540c36f2e09da5945066020621d6a059.patch

![Commit patch header showing email](/assets/git_6.png)

**Flag 1: Email** `jimleepro1@gmail.com`

## Pivot 2: chasing the name and email

With his email and name in hand, I try Googling "Jim Lee Security Consulting," but don't find much.

I think I've found a matching LinkedIn profile, but it has a different GitHub linked to it, so I doubt it's our guy and drop it.

I search "jimlee1337" once more and this time turn up an Instagram and a Threads account:

![Instagram account found](/assets/instagram_1.png)

![Threads account found](/assets/threads_1.png)

This looks like where I'll find his location, so I pin it for later and go back to the GitHub forks in the meantime. One fork in particular catches my eye, it's following our guy, which makes me wonder if it's an alt account of his:

![Suspicious fork account](/assets/git_7.png)

I go through the profile pretty thoroughly, but it leads nowhere.

Back on Komoot, I try searching usernames from the original Discord profile, specifically Jim Lee's username "WKM1337." I find an account following 6 people:

![WKM1337 Komoot search](/assets/komoot_1.png)

Another dead end.

At this point I try using the email itself as a probe, sending a message to it just to see if anything bounces back or triggers an autoreply:

![Email autoreply](/assets/gmail_1.png)

It works. This gets us our second piece of information.

**Flag 2: Phone number** [fill in the number from the autoreply]

## Pivot 3: geolocation

With the first two flags answered, I circle back to Jim Lee's Threads account.

![Threads post 1](/assets/threads_2.png)

![Threads post 2](/assets/threads_image_1.png)

What immediately catches my eye is the ".ro" ending on the sign in the left-hand side of the photo. Romania.

I first try irigati.ro, which brings up this:

![irigati.ro incorrect site](/assets/website_1.png)

Something's off, the site isn't even HTTPS. Going back to the photo, I look more closely and realize there are actually two "i"s, not one.

Searching irigatii.ro instead gives me this:

![irigatii.ro correct site](/assets/website_2.png)

This confirms Jim Lee is in Romania and gives us a lead on the city.

A quick Google search for the shop name turns up their Facebook page:

![Facebook page with location](/assets/website_3.png)

This has a location attached, the Romanian city of Timișoara.

**Flag 3: City** Timișoara

Checking back on the Threads post, Jim Lee wrote:

> "Just finished my last run before the big day, hopping on the tram for my well-deserved coffee at my favourite French supermarket."

The most obvious "French supermarket" is Carrefour, so I look for tram stops that sit close to both a Carrefour and the irigatii.ro shop location. Overlaying the two narrows it down to one station that satisfies both: Gara Timișoara Est.

**Flag 4: Final location** Gara Timișoara Est train station

![Final location - Gara Timișoara Est](/assets/maps_1.png)

Thank you for reading!
