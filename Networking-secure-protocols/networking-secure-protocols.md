# Introduction
this room explains how secure protocols protect:
- confidentiality
- integrity
- authenticity

plaintext protocols like:
- http
- ftp
- pop3
- smtp

can expose sensitive information because data is transmitted unencrypted

# TLS(transport layer security)

Purpose
- tls secures communication over networks

provides:
- encryption
- integrity
- authentication

# SSL vs TLS
- SSL = old/deprecated
- TLS = modern secure version

TLS replaced SSL because it had vulnerabilties.

TLS usage
- tls is added to insecure protocols
| insecure |secure|
|----------|------|
|HTTP |HTTPS |
|SMTP |SMTPS |
|POP3 |POP3S |
|IMAP |IMAPS |

# HTTPS
HTTPS = HTTP + TLS
- default port = 443

HTTPS benefits
- encrypts traffic
- prevents sniffing
- prevents MITM attacks
- protects credentials

TLS handshake
- steps:
1. client hello 
2. server hello
3. certificate exchange
4. key exchange
5. secure communication begins

# important point
- client hello contains tls version?
=> yes

- tls certificate
certificates prove server identity issued by: certificate authority (CA)

- CSR
CSR(certificate signing request) = used to request a signed certificate from a CA

# secure email protocols
TLS secure email protocols

Secure SMTP
- smtp = port 25
- smtps = port 465

secure POP3
- POP3 = PORT 110 
- POP3S = 995

secure IMAP
- IMAP = PORT 143
- IMAPS = PORT 993

# PGP GPG
PGP(pretty good privacy)

Used for:
- Email encryption
- file encryption
- digital signatures

GPG (gnu privacy guard)
open source implementation of pgp

# generate GPG key pair
command:
- gpg --gen -key

# SSH
SSH(Secure shell)
ssh securely replaces: telnet

purpose
- remote administration
- secure command execution
- secure file transfer

ssh default port = 22

important comparison
|protocol | secure? |
|---------|---------|
|rlogin |no |
|telnet |no |
|ssh |yes |

ssh example
- ssh user@ip

SCP (secure copy)
secure file transfer over ssh
- scp file.txt user@ip:/home/user

# VPN
virtual private network creates a secure tunnel over an insecure network

vpn benefits
- encrypts traffic
- hides traffic from attackers
- protects public wifi usage
- enables secure remote access

vpn types
- site to site = connect networks
- remote access = connect user to network

# Extra usefull concepts

# SOCKS5
SOCKS5 is a proxy protocol

supports:
- authentication
- tcp
- udp

important question
socks version if first byte = 0*05?
=> 5

# wireshark tls analysis
browser launched with:
- chromium --ssl-key-log-file=~/ssl-key.log

purpose:
- store tls session keys
- decrypt https traffic in wireshark
