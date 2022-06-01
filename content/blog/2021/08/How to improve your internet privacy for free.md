---
title: "How to improve your internet privacy (for free!)"
date: 2021-08-01T21:01:56+01:00
slug: ""
description: "How to make your internet usage more secure, more private, and faster for free..."
keywords: [Internet Security, Privacy, Security, 1.1.1.1, Cloudflare, Warp, Warp+]
draft: false
tags: [Long-Form, General, Cyber-Security, Privacy]
math: false
toc: false
---

*Note: I am not in any way affiliated with Cloudflare, I just think they're cool!*

## Introduction
As I've made clear in previous publications, I believe passionately that everyone should take their own digital 
hygiene and privacy seriously. In a world where users' personal data is the backbone of a $1.7 trillion industry<sup>
[[1]](#references)</sup>, it is vitally important that the average person takes a stand.

[Cloudflare](https://www.cloudflare.com) is a company which (unless you're a computer scientist) I'd forgive you for 
not recognising in the slightest; however, what they do is paramount to the smooth running of the internet. 
A staggering 10% of all internet requests run through Cloudflare's network<sup>[[2]](#references)</sup> (including 
the request you made to visit this website) making it one of the main players in the internet's day-to-day working. 
Cloudflare, in my opinion, is one of a dwindling number of honourable big tech companies who not only genuinely 
respect their users' privacy, but actively work to protect it.

<br>

---

<br>
<a href="https://www.cloudflare.com" target="_blank"><img src="https://www.cloudflare.com/img/logo-web-badges/cf-logo-on-white-bg.svg" alt="Cloudflare Logo"></a>

<br>

---

## What can Cloudflare do for me?
Cloudflare makes most of its money offering cyber security solutions and protections to large internet companies; 
because of this, they have a lot of headroom to offer easy to use, comprehensive, and secure privacy protecting 
tools to individuals and small businesses for free.

To a computer scientist (like me), this is good because we have access to a myriad of really cool tools we can 
use for our internet-based antics - for example, I send all the traffic for both this website and my [personal website](https://gwood.dev)
through the Cloudflare network. I choose to do this because for me, it offers some really fancy security tools to 
make sure my website uses top-notch security standards, and for you, the loading speeds when you visit this site are 
17% faster<sup>[[3]](#references)</sup>.

To the average user, however, Cloudflare still has something to offer you. Their DNS service [1.1.1.1 with Warp](https://1.1.1.1)
offers vastly improved speed alongside vastly improved privacy, and it's as simple as downloading an app and 
flipping a switch. It routes all the web requests from your device through Cloudflare's high speed network, and it 
does so through a proprietary protocol called Warp (based on [WireGuard](https://www.wireguard.com)) which improves 
your security by encrypting your traffic all whilst preserving most of your speed. They also offer a paid service 
called Warp+ (£4.99/month) which seamlessly adds something called [Argo Smart Routing](https://blog.cloudflare.com/argo/) to your connection, essentially putting you into the 
internet fast lane for up to 30% increased speeds<sup>[[4]](#references)</sup>. Although this is an entirely optional 
addition, I would recommend giving it a try if your internet speed is important to you.

Seriously... Cloudflare are awesome, I use them, and you should too!

## What can't Cloudflare do for me?
As much as using [1.1.1.1 with Warp](https://1.1.1.1) is a huge step in the right direction, and will effectively 
hide which websites you visit from your ISP, it isn't a comprehensive solution. To the average person, it really is 
most of what you need, but in any scenario where your internet privacy, security, and anonymity are essential, 
you'll need to use a paid VPN service. Personally I use [NordVPN](https://nordvpn.com/) *(not affiliated)*, as from my 
research and experience, they offer the best service at a fair price, but any VPN with OpenVPN/WireGuard support, a 
strict 'no logs' policy, and reputable third-party auditing should do the trick - always do your research!

## Summary
To summarise, every company with a stake in advertising are after your personal data in some way or another; if 
you're fine with that, I think you're wrong but that's fair enough. If, however, you're like me and you're very 
concerned about your privacy being compromised, I highly recommend following the instructions on the [1.1.1.1](https://1.1.1.1)
website and using it on your device(s); it won't hide everything from everyone, but it's a bloomin' good start! If 
your privacy/security is essential, or if you're just paranoid, get yourself a decent paid VPN.

## References
1. Forbes. 2019. How Much Money Is In The Global Marketing Industry - More Than We Believed. [ONLINE] Available at: https://www.forbes.com/sites/zarkodimitrioski/2019/02/13/how-much-money-is-in-the-global-marketing-industry-more-than-we-believed. [Accessed 1 August 2021].
2. The Cloudflare Blog. 2016. Control your traffic at the edge with Cloudflare. [ONLINE] Available at: https://blog.cloudflare.com/cloudflare-traffic. [Accessed 1 August 2021].
3. As per a site speed test conducted on 1 August 2021 from the Cloudflare dashboard - [results](/blog/2021/08/img/sitespeedtest.png).
4. The Cloudflare Blog. 2019. WARP is here (sorry it took so long). [ONLINE] Available at: https://blog.cloudflare.com/announcing-warp-plus/. [Accessed 7 August 2021].
