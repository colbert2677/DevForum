Original by [u/Inobservatus](https://devforum.roblox.com/u/inobservatus), taken from the [raw](https://devforum.roblox.com/raw/1195334). To be moved to Gist.

___

# Maintaining Privacy and Security Online
**[Keeping your Roblox account safe](https://en.help.roblox.com/hc/en-us/articles/203313380-Account-Security-Keeping-your-Account-Safe-)**

>“If you think privacy is unimportant for you because you have nothing to hide, you might as well say free speech is unimportant for you because you have nothing useful to say.” ~ Edward Snowden

I got asked about privacy online for the average user, and I ended up compiling some info regarding such. This is a broad topic and most of this information isn't coming directly from me, rather it is being compiled from multiple sources. I won't take credit for anything, and I'll attempt to link to sources where I can.

---
### Encryption of data

I use VeraCrypt full disk encryption for all of my drives and partitions, not just my OS. VeraCrypt adds enhanced security to the algorithms used for system and partitions encryption making it immune to new developments in attacks.

VeraCrypt also solves many vulnerabilities and security issues found in TrueCrypt, the old industry standard for full disk encryption.

#### Key disclosure law

Who is required to hand over the encryption keys to authorities?

Mandatory key disclosure laws require individuals to turn over encryption keys to law enforcement conducting a criminal investigation. How these laws are implemented (who may be legally compelled to assist) vary from nation to nation, but a warrant is generally required. Defenses against key disclosure laws include steganography and encrypting data in a way that provides plausible deniability.

Steganography involves hiding sensitive information (which may be encrypted) inside of ordinary data (for example, encrypting an image file and then hiding it in an audio file). With plausible deniability, data is encrypted in a way that prevents an adversary from being able to prove that the information they are after exists (for example, one password may decrypt benign data and another password, used on the same file, could decrypt sensitive data).

---

### Virtual Private Networks

I always recommend using a good VPN, even for normal everyday browsing. View more information on how VPNs work and why using one is important [here](https://fried.com/vpn-ultimate-guide/). [View](https://docs.google.com/spreadsheets/d/1kKfpAbKMrILTqomZHsbX7cB5hrHZMmgT6yAeH4_j37I/pubhtml) this large spreadsheet that I put up on Google Docs (note that I did not compile this data, source is at the bottom of the spreadsheet).

>Random Note: I strongly recommend using wired connections for your internet connection at home as opposed to wireless. There have been many cases of government snooping by them breaking into networks and collecting wireless data. A classic example is the arrest of Iserdo, the creator of the Butterfly Botnet (Mariposa). Ultimately his arrest and conviction was solidified when Law Enforcement broke into his Wireless Network and monitored him, gathering all the evidence necessary.

---

### Browser Choice and Security

First things first, I will never recommend using Google Chrome and nothing any of you can say will change my mind on this.

Firefox is fast, reliable, open source and respects your privacy.

Tor Browser is your choice if you need an extra layer of anonymity. It's a modified version of Firefox, it comes with pre-installed privacy add-ons, encryption and an advanced proxy.

#### Browser Fingerprint

Is your browser configuration unique?

When you visit a web page, your browser voluntarily sends information about its configuration, such as available fonts, browser type, and add-ons. If this combination of information is unique, it may be possible to identify and track you without using cookies. EFF created a Tool called Panopticlick to test your browser to see how unique it is.

WebRTC IP Leak Test - Is your IP address leaking?

WebRTC is a new communication protocol that relies on JavaScript that can leak your actual IP address from behind your VPN. While software like NoScript prevents this, it's probably a good idea to block this protocol directly as well, just to be safe.

#### How to test for WebRTC leaks

Check your VPN for any potential WebRTC leaks. You can perform a WebRTC leak test by following these simple steps:

  1. Disconnect and exit whatever VPN you’re using.
  2. Find out and note down your IP address by typing “What’s my IP” into Google and hitting Enter – your original IP address will display.
  3. Exit the browser.
  4. Re-launch your VPN and refresh the webpage. Re-do step 2.
  5. If your WebRTC is NOT leaking your IP address should display as something completely different. If your IP address is the same, after you re-do step do with your VPN on – a WebRTC leak is likely exposing your IP address.

Note: your original IP usually begins with 10.xxx or 192.xxx or sometimes an alpha-numeric IPv6).

Improve your security with these Firefox add ons:

Stop tracking with "Disconnect"
>Founded in 2011 by former Google engineers and a consumer-and privacy-rights attorney. The addon is open source and loads the pages you go to 27% faster and stops tracking by 2,000+ third-party sites. It also keeps your searches private.

Block Ads with "uBlock Origin"
>An efficient wide-spectrum-blocker that's easy on memory, and yet can load and enforce thousands more filters than other popular blockers out there. It has no monetization strategy and is completely open source. We recommend FireFox but uBlock Origin also works in other browsers such as Safari, Opera, and Chromium. Unlike AdBlock Plus, uBlock does not allow so-called "acceptable ads".

Hinder Browser Fingerprinting with "Random Agent Spoofer"
>A privacy enhancing firefox addon which aims to hinder browser fingerprinting. It does this by changing the browser/device profile on a timer.

Automatically Delete Cookies with "Self-Destructing Cookies"
>Automatically removes cookies when they are no longer used by open browser tabs. With the cookies, lingering sessions, as well as information used to spy on you, will be expunged.

Encryption with "HTTPS Everywhere"
>A Firefox, Chrome, and Opera extension that encrypts your communications with many major websites, making your browsing more secure. A collaboration between The Tor Project and the Electronic Frontier Foundation.

Block Content Delivery Networks with "Decentraleyes"
>Emulates Content Delivery Networks locally by intercepting requests, finding the required resource and injecting it into the environment. This all happens instantaneously, automatically, and no prior configuration is required.

Stop cross-site requests with uMatrix
>Many websites integrate features which let other websites track you, such as Facebook Like Buttons or Google Analytics. uMatrix gives you control over the requests that websites make to other websites. This gives you greater and more fine grained control over the information that you leak online.

Be in total control with "NoScript Security Suite"
>Highly customizable plugin to selectively allow Javascript, Java, and Flash to run only on websites you trust. Not for casual users, it requires technical knowledge to configure.

Content control with "Policeman"
>This addon has purpose similar to RequestPolicy and NoScript. It's different from the former in that it supports rules based on content type. For example, you can allow images and styles, but not scripts and frames for some sites. It can also be set up to act as a blacklist.

---

### Email

Privacy Conscious Email Providers:

- ProtonMail
- CounterMail
- NeoMailbox

#### Email Clients:

Mozilla Thunderbird - Mozilla Thunderbird is a free, open source, cross-platform email, news, and chat client developed by the Mozilla Foundation. Thunderbird is an email, newsgroup, news feed, and chat (XMPP, IRC, Twitter) client.

MailPile.is (BETA) - A modern, fast web-mail client with user-friendly encryption and privacy features.

#### Privacy Email Tools

gpg4usb - A very easy to use and small portable editor to encrypt and decrypt any text-message or -file. For Windows and Linux.

Mailvelope - A browser extension that enables the exchange of encrypted emails following the OpenPGP encryption standard.

Enigmail - A security extension to Thunderbird and Seamonkey. It enables you to write and receive email messages signed and/or encrypted with the OpenPGP standard.

TorBirdy - This extension configures Thunderbird to make connections over the Tor anonymity network.

Email Privacy Tester - This tool will send an Email to your address and perform privacy related tests.

#### Email Alternatives

Bitmessage
>Bitmessage is a P2P communications protocol used to send encrypted messages to another person or to many subscribers. It is decentralized and trustless, meaning that you need-not inherently trust any entities like root certificate authorities. It uses strong authentication which means that the sender of a message cannot be spoofed, and it aims to hide "non-content" data.

I2P-Bote
>I2P-Bote is a fully decentralized and distributed email system. It supports different identities and does not expose email headers. Currently (2015), it is still in beta version and can be accessed via its web application interface or IMAP and SMTP. All bote-mails are transparently end-to-end encrypted and, optionally, signed by the sender's private key.

RetroShare
>Retroshare creates encrypted connections to your friends. Nobody can spy on you. Retroshare is completely decentralized. This means there are no central servers. It is entirely Open-Source and free. There are no costs, no ads and no Terms of Service.

---

### Privacy Respecting Search Engines

If you are currently using search engines like Google, Bing or Yahoo you should pick an alternative here.

DuckDuckGo
>The search engine that doesn't track you. Some of DuckDuckGo's code is free software hosted at GitHub, but the core is proprietary. The company is based in the USA.

Disconnect Search
>Search privately using your favorite search engine: Google, Yahoo, Bing and DuckDuckGo are available for selection. It masks your IP address, cookies, and other personal info.

MetaGer
>A metasearch engine, which is based in Germany. It focuses on protecting the user's privacy. Supported by 24 own crawlers of small scale web search engines.

ixquick com
>Returns the top ten results from multiple search engines. It uses a "Star System" to rank its results by awarding one star for every result that has been returned from a search engine. Based in the USA and the Netherlands.

---

### Password Managers

If you are currently using a password manager software like 1Password, LastPass, Roboform or iCloud Keychain you should pick an alternative here.

Master Password - Cross-platform
>Master Password is based on an ingenious password generation algorithm that guarantees your passwords can never be lost. Its passwords aren't stored: they are generated on-demand from your name, the site and your master password. No syncing, backups or internet access needed.

KeePass / KeePassX - Local
>KeePass is a free open source password manager, which helps you to manage your passwords in a secure way. All passwords in one database, which is locked with one master key or a key file. The databases are encrypted using the best and most secure encryption algorithms currently known: AES and Twofish. See also: KeePassX.

Encryptr - Cloud Based - (SpiderOak)
>Encryptr is simple and easy to use. It stores your sensitive data like passwords, credit card data, PINs, or access codes, in the cloud. However, because it was built on the zero knowledge Crypton framework, Encryptr ensures that only the user has the ability to access or read the confidential information.

---

### Self Contained Networks

I2P Anonymous Network
>The Invisible Internet Project (I2P) is a computer network layer that allows applications to send messages to each other pseudonymously and securely. Uses include anonymous Web surfing, chatting, blogging and file transfers. The software that implements this layer is called an I2P router and a computer running I2P is called an I2P node. The software is free and open source and is published under multiple licenses.

GNUnet Framework
>GNUnet is a free software framework for decentralized, peer-to-peer networking and an official GNU package. The framework offers link encryption, peer discovery, resource allocation, communication over many transports (such as tcp, udp, http, https, wlan and bluetooth) and various basic peer-to-peer algorithms for routing, multicast and network size estimation.

The Freenet Project
>Freenet is a peer-to-peer platform for censorship-resistant communication. It uses a decentralized distributed data store to keep and deliver information, and has a suite of free software for publishing and communicating on the Web without fear of censorship. Both Freenet and some of its associated tools were originally designed by Ian Clarke, who defined Freenet's goal as providing freedom of speech on the Internet with strong anonymity protection.

Tor Project
>Provides anonymity to websites and other servers. Servers configured to receive connections only through Tor are called hidden services.

RetroShare
>Open Source cross-platform, Friend-2-Friend and secure decentralised communication platform.

---

### Domain Name System (DNS)

CloudNS - Service
> An Australian based security focused DNS provider. Features: DNSCrypt Support to provide confidentially and message integrity, complete trust validation of DNSSEC enabled names, namecoin resolution of .bit domain names and no domain manipulation or logging.

DNSCrypt - Tool
>DNSCrypt is a protocol for securing communications between a client and a DNS resolver. The DNSCrypt protocol uses high-speed high-security elliptic-curve cryptography and is very similar to DNSCurve, but focuses on securing communications between a client and its first-level resolver.

OpenNIC - Service
>OpenNIC is an alternate network information center/alternative DNS root which lists itself as an alternative to ICANN and its registries. Like all alternative root DNS systems, OpenNIC-hosted domains are unreachable to the vast majority of the Internet. Only specific configuration in one's DNS resolver makes these reachable, and very few Internet service providers have this configuration.

NoTrack
>A network-wide DNS server which blocks Tracking sites. Currently works in Debian and Ubuntu.

Namecoin
>A decentralized DNS open source information registration and transfer system based on the Bitcoin cryptocurrency.
---

### Encrypted Cloud Storage Services
If you are currently using a Cloud Storage Services like Dropbox, Google Drive, Microsoft OneDrive or Apple iCloud you should pick an alternative here.

Remember to manually encrypt your files before uploading them to the cloud!

#### Hosted

Seafile - 100 GB Storage for $10/month
>Seafile offers 100 GB Storage for $10/month but also gives you the opportunity to host on your own server. Your data is stored in Germany or with Amazon Web Service in the US for the cloud version. Encrypt files with your own password.

ownCloud - Choose your hoster
>Similar functionally to the widely used Dropbox, with the difference being that ownCloud is free and open-source, and thereby allowing anyone to install and operate it without charge on a private server, with no limits on storage space or the number of connected clients.

Least Authority S4 - For Experts
>S4S4 (Simple Secure Storage Service) is Least Authority's verifiably secure off-site backup system for individuals and businesses. 100% client-side encryption and open source transparency. $25/month for unlimited storage. Servers are hosted with Amazon S3 in the US.

#### Self Hosted

Seafile
>Seafile is a file hosting software system. Files are stored on a central server and can by synchronized with personal computers and mobile devices via the Seafile client. Files can also be accessed via the server's web interface.

Pydio
>Pydio is open source software that turns instantly any server (on premise, NAS, cloud IaaS or PaaS) into a file sharing platform for your company. It is an alternative to SaaS Boxes and Drives, with more control, safety and privacy, and favorable TCOs.

Tahoe-LAFS
>Tahoe-LAFS is a Free and Open decentralized cloud storage system. It distributes your data across multiple servers. Even if some of the servers fail or are taken over by an attacker, the entire file store continues to function correctly, preserving your privacy and security.

ownCloud - Host your own
>Similar functionally to the widely used Dropbox, with the difference being that ownCloud is free and open-source, and thereby allowing anyone to install and operate it without charge on a private server, with no limits on storage space or the number of connected clients.

#### Related Information
Cryptomator - Free client-side AES encryption for your cloud files. Open source software: No backdoors, no registration.

---

### Text and Video Messaging

Secure your text messages, Instant Messaging and Chat

Pidgin + OTR (Windows)
>Pidgin is a popular free and open source IM client that lets you chat to users on AIM, Google Talk, MSN, Yahoo and many more. OTR (Off-the-road) is a plugin that combines AES encryption, perfect forward secrecy, and the SHA-1 hash function to ensure strong encryption for IM sessions. As with GnuPG for emails, initial setup is a bit of a pain, but once done operation is seamless (we now have a detailed guide for this).

*Tox.im / Tox.chat is not a secure solution any longer. There is internal conflict between the devs, a break off with IP being stolen, and some devs claiming the NSA have been pushing bug fixes (open source) with exploits that allow them to monitor things. If anyone knows more about this, let me know. Information isn't very clear, but due to everything that has been happening, I would not trust my privacy with them.*

Adium (OSX)
>Adium is a free and open source messaging client for Mac that also lets you talk to friends on lots of different networks. Even better, Addium comes with OTR support built-in!

* TorChat
* ChatSecure
* SilentCircle
* Surespot
* Jitsi
* Textsecure
* CryptoCat
