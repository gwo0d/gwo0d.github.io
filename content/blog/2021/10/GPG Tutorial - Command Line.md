---
title: "GPG Tutorial - Command Line"
date: 2021-10-10T15:32:59+01:00
slug: "GPG-Tutorial-Command-Line"
description: "A comprehensive tutorial on command line GPG usage..."
keywords: [GPG, PGP, GNU Privacy Guard, Security, Cryptography, Privacy, Cyber Security]
draft: false
tags: [cyber-security, long-form, privacy]
math: false
toc: true
---

## Introduction

*My GPG key can be found [here](/)*

In a world where there exists an ever-growing economy revolving around the sale and processing of individuals’ private
data, tools like [GNU Privacy Guard (GPG)](https://gnupg.org) offer a convenient way to take back control of what was
once a well-respected right – individual privacy. I have spoken before on several occasions about why it is important to
take your privacy seriously, and to be clear, GPG is not by any means an extensive solution; it is to a smaller extent a
part of a much larger mosaic of tools needed to completely take control of your privacy.

GPG offers a set of features which allow the user to secure and/or verify data in a number of ways. I often hear the
argument *“surely a big, powerful entity could decrypt my data if they really want to?”*, and sure, there are
circumstances in which this could be true, but if used correctly, GPG offers a solid way to mathematically guarantee the
integrity and security of data i.e. no one, however powerful or well-funded has any way of accessing that data ever. I
have written a guide like this before (depreciated) which goes into more detail about why this is important and how it
works on a slightly more technical level, which you can access [here](/blog/2020/11/data-security-a-comprehensive-guide)
if you’d like to. I will warn, 
however, that it’s
aimed towards only Windows users and is outdated.

## How to install GPG

Installing GPG will vary based on your platform, and there are often several methods of doing so. The following are 
the methods I recommend using to install GPG (all of which will use a package manager).

### macOS
1. Open Terminal - open Finder by holding Command `⌘` and pressing the Space Bar, then type 'Terminal' and press 
   enter `↵`
2. Install [Homebrew](https://brew.sh) by entering the following command into Terminal (please confirm this command 
   matches the one on the Homebrew website - it may be outdated):
    ```bash
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    ```
3. Once Homebrew is installed, run the following command in Terminal:
    ```bash
    brew install gnupg
    ```
   
GPG should now be installed on your Mac.

### Windows
1. Open PowerShell (admin) - in Windows Search, type PowerShell. Locate PowerShell within the results, right click, 
   and click "Run as Administrator". Approve the User Account Control prompt when it shows.
2. Install [Chocolatey](https://chocolatey.org) by entering the following command into PowerShell (please confirm this command
   matches the one on the Chocolatey website - it may be outdated):

    ```bash
    Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
    ```
3. Once Chocolatey is installed, run the following command in PowerShell:

    ```bash
    choco install gnupg
    ```

GPG should now be installed on your Windows PC.

### Linux
1. If you use Linux and don't already know how to use GPG, stop using Linux immediately - you simply aren't worthy!

## How to generate a GPG keypair

In order to use GPG, you need to generate a keypair, that is a public key and a private key. Your public key will be 
responsible for encrypting data, and is (as the name suggests) available to the public. Your private key, however, 
is the key used to decrypt and sign data; it is therefore vitally important that you keep your private key 
very safe, and equally secure to prevent others seeing your data or pretending to be you.

- To generate your keypair, run the following command in your relevant command line, either Terminal (macOS) or 
PowerShell (Windows).
   ```bash
   gpg --full-generate-key
   ```
   You will then be taken through a step-by-step setup guide, and should proceed as follows:
   - Type `1` and press enter `↵` - this will select option 1 for the key type (RSA and RSA).
   - Type `4096` and press enter `↵` - this defines the length of your keys (4096 bits). Basically the longer your 
     keys are the more secure your encryption is.
   - Type `0` and press enter `↵` - this specifies the expiry for your key, and in this case we can make it never 
     expire. If you have a good reason to have an expiring key, change this accordingly.
     - Type `y` and press enter `↵` to confirm this.
   - Enter your details correctly - it won't be possible to change these after your keys have been generated.
   - Optionally: leave a comment to attach to your key. You can just press enter `↵` to skip if you don't want a 
     comment.
   - You will now be shown a summary of the details you've entered. Check these thoroughly, as this is your last 
     opportunity to change them. If you are satisfied, type `O` and press enter `↵` to confirm and generate your 
     keypair.
   - Finally, enter a nice secure password at the prompt. This is your last line of defence if your key is stolen so 
     for \<insert preferred deity\>'s sake make your password strong.

And that's it! You're now the proud owner of a shiny new GPG keypair. Now you need to send your key 
to a keyserver, or more specifically many keyservers. This allows anyone to look up your GPG key and encrypt things 
for you, as well as to verify your signatures. You can do this as follows...

- Run the following command:
   ```bash
   gpg --list-keys
   ```
  This will provide a list of your stored keys (including yours)
- Find the key with your email address beneath it. If you're new to GPG, this will probably be the only one there.
- At the top of your key's entry, there will be a section prefixed with `pub`, the line underneath this consisting 
  of seemingly random letters and numbers is what we're looking for - that's your key's signature. Copy this and 
  keep it safe.
- Now run the following command:
   ```bash
   gpg --send-keys <your key's signature>
   ```
Your key has now been sent to a pool of keyservers around the world. Yay!

The last thing you should do is generate a revocation certificate, just in case your key goes missing. A revocation
certificate is
basically a kill-switch for your keypair. If it's published to a keyserver, it tells everyone to stop using your key,
so you can make a new one.

- To do this, run the following command:
    ```bash
    gpg --gen-revoke <your key's signature>
    ```
- You will be asked for a save location, so make sure you choose somewhere you'll remember.

Now this is very important... **KEEP THIS CERTIFICATE SAFE!** If you lose it, or it gets into the wrong hands, it 
can cause you a whole lot of problems; it's far easier to just look after the thing.

## How to use GPG

Now you've got your keypair, you're ready to start using it. GPG has a number of useful functions, but today I am only 
going to cover the two most commonly used ones - sign, and encrypt.

- Signing data is a way of mathematically proving a piece of data came from you, and hasn't been changed since you 
signed it.
- Encrypting data is a way of mathematically securing data, so that only the intended recipient can read it.

Often data will be both signed and encrypted, in order to guarantee both its integrity, origin, and security.

### How to import someone else's key
If someone has sent you a file with a signature or an encrypted file, it is important to be able to verify/decrypt it.
The first thing you'll need to do is import the key of whoever sent you the file.
- To do this, first get hold of the person's key (ideally from their website or other trusted source) and download
  it to your device.
- Then navigate to the directory you've downloaded their key to, and run the following command:
    ```bash
    gpg --import <their key's filename>
    ```
- If you are 100% confident of the key's origin i.e. are sure it's legitimate, you should finish with this command:
```bash
gpg --sign-key <their key's signature>
```

### How to sign data
To sign a file, you first need to navigate to whichever directory said file is stored in on your device. I won't 
outline here how to do that, but numerous guides online will help with this (it's very easy).

- Once in your desired file's directory, run the following command:
    ```bash
    gpg --sign <your file's name (including extension e.g. .txt)>
    ```
    - You will be asked for your key's password, and should enter it when prompted.
- When completed, you should have a signature file in the same directory as your target file, in a form like:
  - \<filename\>.sig
  - \<filename\>.gpg

When you distribute files with a signature, be sure to include both the file itself and the .gpg/.sig signature file.

### How to encrypt data
To encrypt a file, the process is remarkably similar to signing. As before, begin by navigating to the file's 
directory.

- Once in your desired file's directory, run the following command:
    ```bash
    gpg --encrypt <your file's name (including extension e.g. .txt)>
    ```
- You will be asked to enter a list of recipients. If you would like to be able to decrypt the file yourself, it is 
  important that you include yourself on this list. You may enter their key's signature, their email address, or 
  their name.
- You will be asked for your key's password, and should enter it when prompted.
- When completed, your encrypted file should be in the same directory with the filename \<filename\>.gpg
- If desired, where security is paramount, it may also be a good idea to delete the original at this point.

### How to verify a signature
With the sender's key imported [(as above)](/blog/2021/10/gpg-tutorial-command-line/#how-to-import-someone-elses-key),
run the following command in the signature file's directory. It is important to have both the signature file and the 
file itself together for this:

```bash
gpg --verify <signature's filename>
```

The level of trust in this signature should now be shown.

### How to decrypt a file
Decrypting a file is probably the easiest GPG operation. Simply navigate in the terminal to the directory where the 
encrypted file is and run the following command:

```bash
gpg --decrypt <filename>
```

That's it! I said it'd be easy.

---

A signature for this message can be found [here](/blog/files/2021/10/gpg-tutorial-command-line.md.asc)