---
title: "Data Security: A Comprehensive Guide"
date: 2020-11-30T10:14:47Z
slug: ""
description: "A comprehensive guide to data security using GPG."
keywords: [Data Security, GPG, Tutorial, GNU Privacy Guard, Encryption, Signing]
draft: false
tags: [Cyber-Security, Long-Form, privacy]
math: false
toc: true
---

# Depreciated

In a world where it is increasingly difficult to keep control of one's own data, I thought I'd write a reasonably in-depth tutorial highlighting some of the core ideas behind data security.

This guide will focus on the [GNU Privacy Guard (GPG)](https://gnupg.org/), and will cover two main aspects: signing, and encryption.

## Signing & Encryption: What are they?

#### Signing
Data signing is the the process of mathematically guaranteeing that a given file came from a given individual. In the case of GPG, a combination of both symmetric and asymmetric encryption is used, making it hybrid encryption software; the main reason for this is to leverage both the speed of symmetric encryption, and the heightened security and features of asymmetric encryption.

#### Encryption
Encryption is the process of changing data in such a way that it can only be read by the intended recipient. It, if done correctly, would be mathematically impossible to break via brute force. To give you an idea of how this works, think about this:

---

If I give you these two 50-digit prime numbers:
- 36649857991871359671268059387951099780683246437639
- 60497937375492901407775142412345011113461054744869

You would probably find it easy using a calculator/computer to multiply these together, right?

---

Okay, so what if I said *"which two prime numbers did I multiply together to get this number?"*
- 6488691662963151938313315014533805534953921302149

Now that, computationally, would take a **very** long time to solve.

The numbers were:
- 5949869657461425413095793
- 1090560304094396012663893

By the way

---

Okay, so now I'd like to answer the most common question I get when I start talking about encryption...

## Why should I care? I have nothing to hide!
*The answer to this question is different to everyone, and what I say here is purely my own opinion.*

Basically, my main argument when answering this question is that if we don't take control of our own data at this stage (while it's still relatively easy to do so), companies and governments will take more and more liberties when handling personal data until we reach a point of no return where privacy is a distant memory.

You may think I'm being melodramatic here, but a real world example is [Facebook's privacy policy](https://www.facebook.com/about/privacy) and their privacy practices by extension; Facebook do allow their users to customise their privacy settings, however, they make it so intrinsically difficult that 99% of users will just accept the minor privacy blow. The accumulation of scenarios like these is what I'm talking about.

To the not-so-techy masses out there, I implore you to take your own data security seriously, because in all honesty I think we're closer to losing our privacy than we might think.

## Okay, so what can I do about it?
In a nutshell, lots! As I mentioned before, this guide is going to focus on GPG, which should offer all of the features most folks need.

#### Firstly, why can we trust GPG?
GPG is an open source piece of software, meaning the code is available for free to anyone who wants it. This means that anyone who knows what they're doing can (and do) scrutinise every single aspect of the software and guarantee its integrity. It's also written by "the community", meaning security flaws reaching the released software would be highly unlikely, and even if they did they'd be spotted very quickly.

#### How to install GPG:
Installing GPG is just the same as installing any other piece of software. I'm using Windows 10, so that's what I'll cover here - the process on other platforms is very similar, however.

1. Head over to [gnupg.org](https://gnupg.org) and find the downloads tab. Under that, scroll down to the "GnuPG Binary Releases" section and download the appropriate version for your device (in my case, Gpg4win).

![GnuPG Download Page](/blog/img/2020/11/GPG-Download.png)

2. When your installer has downloaded, locate wherever it's saved (your 'Downloads' folder by default), and double click it to run.

3. I recommend going with the default options selected, but feel free to review them if you'd like. As I said though, the defaults will be perfectly fine for most folks.

That's it! You're now the proud owner a shiny new copy of GPG. You may also have noticed Kleopatra on your system - don't worry, we'll get to her.

#### Basic Usage:
GPG is, by itself, a command line tool, meaning in order to use it, you have to do scary command line things which realistically no one sane wants to do. Luckily, Kleopatra can help with this.

Kleopatra is a Graphical User Interface (GUI) for GPG, which allows you to interact with it on the screen rather than via the command line. It makes life easier for the most part, and is a really cook piece of software.

##### How to Sign:
When you installed Kleopatra, you may have noticed there are some extra options when you right-click on a file now. If you'd like to sign a file, all you have to do is right-click on it and select `Sign`; this will open a dialogue box where you can configure the signing and confirm it. *Note: you'll be asked for your key's password if you set one.*

##### How to Encrypt:
Similarly to encrypt data, you right-click on the file and select either `Encrypt` or `Sign and Encrypt`, and these do what they say on the tin. There's really no reason not to use the `Sign and Encrypt` option but it's up to you. You can choose to encrypt files for yourself (with your public key), and/or to encrypt them for others - be sure to add everyone you'd like to be able to read it before you encrypt.

##### Further Reading:
There are of course far more functions GPG is capable of, but I've covered enough for the majority of people. If you need more advanced usage, [this article](https://www.howtogeek.com/427982/how-to-encrypt-and-decrypt-files-with-gpg-on-linux/) by [HowToGeek](https://www.howtogeek.com/) is very detailed.

## Summary:
In this article I've given a brief overview of how to use GPG, and why you should. I hope you've found it helpful!

*-George*