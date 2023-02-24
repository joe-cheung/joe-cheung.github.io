---
title:  "Why You Should Use A Password Manager"
subtitle:
date:   2021-08-15 00:00:00
update: 
author: Joe Cheung
description:
tags: software cryptography finished
wordcount: 1843
---
_I declare no conflict of interest. I’m just a happy user of Bitwarden and Authy (they’re free anyway)._

1. TOC
{:toc}

## Problem 1: You Need Good Passwords

The bare minimum a website like Gmail does to keep your password secure in its database is to encrypt your password using a [one-way pseudorandom function](https://en.wikipedia.org/wiki/Pseudorandom_generator_theorem#One-way_functions) (input: plaintext password; output: pseudorandom hash i.e. long string of gibberish), so Google only have to see that the hash of the password you typed in matches the hash of your password stored on its database.

In the event of a data breach, the hacker can’t reverse the hash to get your password because of its pseudorandomness, but they can try all the combinations, though brute-force attacks start getting infeasible when your password is longer than 8 characters.

Instead, the hacker can pass a dictionary of the [most common passwords](https://en.wikipedia.org/wiki/List_of_the_most_common_passwords) like “password”, “qwerty”, and “12345678” through the same one-way pseudorandom function, and if any of the hashes match the leaked hash, they know they’ve cracked your password. 

And such a [dictionary attack](https://en.wikipedia.org/wiki/Dictionary_attack) is scarily easy to do. 

Let’s say the hacker has a [Nvidia Titan X](https://en.wikipedia.org/wiki/GeForce_900_series) graphics card (GPUs are only getting [better](https://www.gpucheck.com/gpu-benchmark-graphics-card-comparison-chart)), they can perform a dictionary attack with [hashcat](https://hashcat.net/wiki/) at the rate of _10 billion_ passwords per second using the cryptographically broken but still widely used 128-bit hash function [MD5](https://en.wikipedia.org/wiki/MD5). If a better hash function is used, it will simply lower the rate to millions or thousands of passwords per second. [Data breaches](https://en.wikipedia.org/wiki/List_of_data_breaches) happen _all the time_, so the hacker can crack your password even faster by trying billions of real passwords.

Worse, [Google](https://cloud.google.com/blog/products/g-suite/notifying-administrators-about-unhashed-password-storage), [Facebook](https://about.fb.com/news/2019/03/keeping-passwords-secure/), [Instagram](https://about.fb.com/news/2019/03/keeping-passwords-secure/), [Twitter](https://blog.twitter.com/official/en_us/topics/company/2018/keeping-your-account-secure.html), [GitHub](https://www.zdnet.com/article/github-says-bug-exposed-account-passwords/) all stored millions of passwords in plaintext! If even tech giants fail to do the bare minimum of encrypting all of their users’ passwords, what makes you think you can rely on smaller companies to secure your passwords?

## Problem 2: Good Passwords Are Hard To Remember

The key idea in [password strength](https://en.wikipedia.org/wiki/Password_strength) is entropy i.e. the information held in a password. For example, a password made of 42 random bits has an entropy of 42 bits, which requires 2<sup>42</sup> (4,398,046,511,104) attempts to exhaust all possibilities during a [brute-force search](https://en.wikipedia.org/wiki/Brute-force_search). Thus, increasing the entropy of the password by one bit doubles the number of guesses required.

To simplify, the general rules in choosing a password with high entropy are:

1. Minimum password length of 8
2. Generate passwords randomly
3. Avoid character repetition, keyboard patterns, dictionary words, letter or number sequences
4. Avoid using information that is or might become publicly associated with you, e.g. username, ID number, dates, or names of ancestors, romantic partners, relatives or pets

This means the better your passwords, the harder they are to remember.

![](/images/2021-08-15-Password-Manager/image1.png)

_[Obligatory XKCD](https://xkcd.com/936)_

You have two options: write them down on a piece of paper, or use the same password. 

The former is not a good solution because you may lose the piece of paper, it takes effort to come up with a unique, long, random password, and it's inconvenient because you’ll have to look up your password every time you log in.

The latter is a terrible idea because no matter how strong that one password is, the hacker only needs to crack it once to gain access to all of your accounts.

## The Solution

Enter [password manager](https://en.wikipedia.org/wiki/Password_manager) – encrypted list of all your passwords. You only need to memorise one [strong](https://1password.com/password-generator/) master password to access your vault of strong passwords.

Putting all your eggs in one basket seems like a bad idea, so here is how password managers in general work, using [Bitwarden](https://bitwarden.com/)’s simplified security protocol as an example:

1. Passwords in the vault are encrypted using 256-bit [AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard)-[CBC](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher_block_chaining_(CBC)) (used by the US NSA for top secret information).
2. [Encryption key](https://bitwarden.com/help/article/what-encryption-is-used/) derived from master password using [PBKDF2](https://en.wikipedia.org/wiki/PBKDF2) [SHA-256](https://en.wikipedia.org/wiki/SHA-2).
    1. You enter a strong master password
    2. On client side:
        1. Appends your master password with your email address
        2. Salts (adding a series of characters to) your master password using your email address
        3. hash (“password” + “ email”)
        4. After 100,001 iterations, the 256-bit hashed password is sent to the server
    3. On server side:
        5. Salts hash with a pseudorandom series of characters
        6. hash (“hashed password from client side” + “salt”)
        7. After another 100,000 iterations, the 256-bit hash is stored on the server as the encryption key
3. When authenticating with the server ([Microsoft Azure Cloud US](https://en.wikipedia.org/wiki/Microsoft_Azure) or self-hosted), a copy of the encrypted vault is downloaded on your device.
4. When you access the vault, it is decrypted using your encryption key and stored in RAM only
5. When the vault is locked, the data is purged from RAM

As the hash functions are one-way only, meaning no one could reverse-engineer them into your master password, they’re also virtually useless to hackers.

## Can’t I Just Use My Browser?

Using your browser’s built-in password storage is better than nothing, but other than zero-knowledge security protocol, password managers have better features. Bitwarden again for example:

1. Supports multiple operating systems (Windows, macOS, Linux, iOS, Android)
2. Supports extension on multiple browsers to auto-fill usernames and passwords (Chrome, Firefox, Safari, Edge, Opera, Vivaldi, Brave, Tor)
3. Supports web vault on any browser
4. Generates customisable pseudorandom passwords or [passphrases](https://en.wikipedia.org/wiki/Passphrase)
5. Vault timeout and biometric authentication
6. Stores other data e.g. software product keys, addresses, bank accounts, and credit card numbers
7. Identifies passwords and other data that have been compromised in data breaches, reused passwords, and weak passwords
8. Logs or clears password history
9. Identifies URIs that use unsecured schemes
10. Supports sharing usernames and passwords
11. Emergency access (grants one person access to your vault in case of emergency)
12. Self-host option

Self-hosted password managers, encrypted Excel spreadsheets (any document before Office 2007 is [insecure](https://en.wikipedia.org/wiki/Microsoft_Office_password_protection)) or markdown files all are better than nothing, but you won’t be able to enjoy any of the features listed above, with the biggest cons being

1. Possibly lower security
2. No access from other devices (e.g. can’t login on your phone when you’re out)
3. Having to manually lookup and type in password for every login
4. Regular manual backups
5. Cumbersome password sharing

The more friction it is to use, the less you’ll use it, so save yourself the hassle and enjoy the cloud-based password managers. There are [plenty](https://en.wikipedia.org/wiki/List_of_password_managers) of good options; I use Bitwarden because it is free (with the most complete features and no limits), secure, cloud-based, open-source, audited by third-parties, and is [consistently](https://www.nytimes.com/wirecutter/reviews/best-password-managers/) [the](https://www.cnet.com/tech/services-and-software/best-password-manager/) [top](https://www.wired.com/story/best-password-managers/) [free](https://www.tomsguide.com/us/best-password-managers,review-3785.html) [recommendation](https://www.investopedia.com/best-password-managers-5080381).

## Overview of Bitwarden’s Security Protocol

Feel free to skip to the next section if you’re not interested to know how it works in detail.

Some password managers have more sophisticated security protocols; below is from Bitwarden’s security [whitepaper](https://bitwarden.com/images/resources/security-white-paper-download.pdf).

Upon account creation:

![](/images/2021-08-15-Password-Manager/image2.png)

1. On client side:
    1. Produce Master Password Hash and Stretched Master Key
        1. Salts your Master Password using your email address
        2. hash (“Master Password + “email address”) using [PBKDF2](https://en.wikipedia.org/wiki/PBKDF2) [SHA-256](https://en.wikipedia.org/wiki/SHA-2) with 100,001 iterations to produce 256-bit Master Key
        3. hash (“Master Key”) using [HKDF](https://en.wikipedia.org/wiki/HKDF) to produce 512-bit **Stretched Master Key**
        4. hash (“Master Password” + “Master Key”) using PBKDF2 SHA-256 with 1 iteration to produce 256-bit Master Password Hash
        5. Send **Master Password Hash** to server for authentication
    2. Produce Protected Symmetric Key
        1. Produce pseudorandom 512-bit [Symmetric Key](https://en.wikipedia.org/wiki/Symmetric-key_algorithm) (same key for encryption of plaintext and decryption of ciphertext, as opposed to public/asymmetric keys i.e. pair of public and private keys
        2. Produce pseudorandom 128-bit [Initialisation Vector](https://en.wikipedia.org/wiki/Initialization_vector) (to randomise a set of input blocks before encryption)
        3. encrypt (“Initialisation Vector” + “**Symmetric Key**” + “**Stretched Master Key**”) using [AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard)-[CBC](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher_block_chaining_(CBC)) to produce 256-bit Protected Symmetry Key
        4. Send **Protected Symmetry Key** to server for authentication
    3. Purge all keys from RAM
2. On server side:
    1. hash (“Master Password Hash” + “pseudorandom salt”) using PBKDF2 SHA-256 with 100,000 iterations to produce 256-bit **hash of Master Password Hash **for storage

Upon login:

![](/images/2021-08-15-Password-Manager/image3.png)

1. On client side:
    1. Produce Master Password Hash and Stretched Master Key
        1. Salts your Master Password using your email address
        2. hash (“Master Password + “email address”) using PBKDF2 SHA-256 with 100,001 iterations to produce 256-bit Master Key
        3. hash (“Master Key”) using HKDF to produce 512-bit **Stretched Master Key**
        4. hash (“Master Password” + “Master Key”) using PBKDF2 SHA-256 with 1 iteration to produce 256-bit Master Password Hash
        5. Send **Master Password Hash** to server for authentication
2. On server side:
    1. hash (“Master Password Hash” + “pseudorandom salt”) using PBKDF2 SHA-256 with 100,000 iterations to produce 256-bit **hash of Master Password Hash**
    2. Authenticate your login if the **hash of Master Password Hash **produced upon login matches the stored **hash of Master Password Hash **produced upon account creation
    3. If authenticated, send **Protected Symmetric Key** produced upn account creation to client
3. On client side:
    1. hash (“Master Key”) using HKDF to produce 512-bit Stretched Master Key
    2. decrypt (“**Stretched Master Key**” + “**Protected Symmetric Key**”) using AES-CBC to produce **Symmetric Key**
    3. decrypt vault items (e.g. username/password) using Symmetric Key
    8. Purge all keys from RAM when vault is locked or timeout

So your Master Password and Symmetric Key (the “encryption key”) are only stored in and purged from RAM, and never sent to Bitwarden servers.

The mid 2021 release of [Admin Password Reset](https://bitwarden.com/help/article/admin-reset/) introduced a new [RSA Public/Private Key Pair](https://en.wikipedia.org/wiki/Public-key_cryptography) for all Organizations. The RSA Private Key is further encrypted with the Organizationʼs pre-existing symmetric key before being stored. The [RSA-2048](https://en.wikipedia.org/wiki/RSA_numbers#RSA-2048) (2,048-bit) Key Pair is generated and encrypted client-side upon creation of a new Organization.

## Two-Factor Authentication
Even if your password manager is secure, and passwords strong, you’re still vulnerable to attacks like [keylogging](https://en.wikipedia.org/wiki/Keystroke_logging) and [phishing](https://en.wikipedia.org/wiki/Phishing), or simply people looking over your shoulder. [Two-factor authentication](https://en.wikipedia.org/wiki/Multi-factor_authentication) simply means a method additional to a password like a bankcard, your phone, or a key.

Of course, the most secure setup is a completely self-hosted offline password manager coupled with a hardware [security token](https://en.wikipedia.org/wiki/Security_token) like [FIDO2 USB security keys](https://en.wikipedia.org/wiki/FIDO2_Project) , but that comes with significant costs to convenience. 2FA using SMS is better than nothing but is [insecure](https://www.forbes.com/sites/zakdoffman/2020/10/11/apple-iphone-imessage-and-android-messages-sms-passcode-security-update/) as it is plaintext that is easily tracked and intercepted due to telephone network protocol [vulnerabilities](https://en.wikipedia.org/wiki/Signalling_System_No._7#Protocol_security_vulnerabilities), and is vulnerable to [SIM swapping attacks](https://en.wikipedia.org/wiki/SIM_swap_scam).

The next best thing is authenticator apps like [Authy](https://authy.com/), which is just as convenient as SMS but much more secure: 
1. Offline – 2FA tokens generated directly on device
2. Protected with biometric, PIN, or password
3. 2FA data encrypted without storing on their servers, only decrypted on phone RAM
4. Optional secure cloud backup
5. No lockouts if phone lost (unlike Google Authenticator)
6. Supports multiple devices (iOS, Android, Chrome, Windows, macOS)
7. Supports any site that uses TOTP (time-based one-time passcode) and Google Authenticator

Again there are multiple good options; I use Authy because it is free, most feature-rich, well supported by its parent company Twilio, best UI design, [transparent](https://authy.com/blog/why-is-the-authy-2fa-app-free-for-users/), recommended by Bitwarden, and is one of the [top](https://www.nytimes.com/wirecutter/reviews/best-two-factor-authentication-app/) recommendations in general.

## Conclusion
It does take a bit of time to enter all your accounts (I had more than a hundred) into Bitwarden and Authy at the start, but you can make the migration easier by [importing data](https://bitwarden.com/help/article/import-data/) into your vault.

Trust me: you’ll get so used to the sublime convenience of auto-fill username, password, and even card details; it brings me joy every time I use Bitwarden. They're such low-hanging fruits that you’ll wonder why you waited until now to start using a password manager and an authenticator app.

