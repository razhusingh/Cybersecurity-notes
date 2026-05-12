# Introduction
protocols  covered:
- dns
- whois
- http(s)
- ftp
- smtp
- pop3
- imap

# DNS (domain name system)

dns converts domain names into ip addresses

example:
```
example.com -> 93.184.216.34
```
dns ports

| protocol | port |
|----------|------|
|dns |53 |

dns mainly uses:
- UDP 53
- TCP 53 (fallback)

important dns records

|record |purpose |
|-------|--------|
|A |hostname -> ipv4|
|AAAA |hostname -> ipv6 |
|MX |mail server |
|CNAME |alias |
|TXT |text info |

commands 

nslookup
```
nslookup www.tryhackme.com
```

dig
```
dig tryhackme.com
```

reverse lookup
```
dig -x 8.8.8.8
```

# WHOIS
 
whois gives information about domain registration

indormation includes:
- registar
- owner
- creation date
- expiry date
- name servers

command
```
whois tryhackme.com
```

# HTTP(S)
hypertext transfer protocol used for web communication

ports
- http = 80
- https = 443

http methods
|method |purpose |
|-------|--------|
|GET |retrieve data |
|POST |send data |
|PUT |update data |
|DELETE |remove data |

example request 
```
get / http/1.1
host: example.com

```
status codes:
- 200 = ok
- 301 = redirect
- 403 = forbidden
- 404 = not found
- 500 = server error

# HTTPS
HTTPS = HTTP + TLS encryption

provides:
- encryption
- integrity
- authentication

curl commands
- get webpage

curl http://example.com

- view headers

curl -I https://example.com

# FTP (file transfer protocol)
ftp transfers files between systems

FTP commands
- user = username
- pass = password
- retr = retrieve
- stor = store

ftp ports
- control = 21
- data = 20

connect to ftp

- ftp machine_ip

anonymous login
``` 
username: anonymous
password:
```

common ftp commands

|command |purpose |
|--------|--------|
|ls |list files |
|cd |change directory |
|get |download file |
|put |upload file |
|bye |exit |

example: 
```
ftp machine_ip

ls

get file.txt

```

ASCII mode

type ascii = used for text files

# SMTP (simple mail transfer protocol)
SMTP sends emails

SMTP ports

smtp = 25
smtps = 465
submission = 587

SMTP commands 
- HELO/EHLO = identify client
- MAIL FROM = sender
- RCPT TO = recipient
- DATA = message body
- QUIT = exit
- . = indicate the end of the email message

example
```
telnet machine_ip 25


HELO example.com
MAIL FROM:test@test.com
RCPT TO:admin@test.com
DATA
Hello
.
QUIT

```

# POP3 (post office protocol)
POP3 retrieves emails from server

pop3 ports
- pop3 = 110
- pop3s = 995

commands

- USER = username
- PASS = password
- STAT = requests number of message and total size
- LIST = list emails
- RETR = retrieve email
- DELE = delete
- QUIT = exit

example:
```
telnet machine_ip 110

USER admin
PASS password
LIST 
RETR 1
QUIT

```
# IMAP (internet message access protocol)
IMAP synchronizes email across devices

IMAP ports
- imap = 143
- imaps = 993

IMAP Commands
- LOGIN = authenticate
- SELECT = select mailbox
- FETCH = retrieve eail
- LOGOUT = exit

Example:
```
telnet machine_ip 143

LOGIN admin password
SELECT inbox
FETCH 1 body[]
LOGOUT

```

POP3 VS IMAP
|feature |pop3 |imap |
|--------|-----|-----|
|sync devices |no |yes |
|stores mail on server | usually no |yes |
|modern usage |less common |common |

# important ports summary

|protocol |port |
|---------|-----|
|TELNET |23 |
|dns |53 |
|http |80 |
|https |443 |
|ftp |21 |
|smtp |25 |
|pop3 |110 |
|imap |143 |

# improtant commands summary
|command |purpose |
|--------|--------|
|nslookup |dns lookup |
|dig |dns query|
|whois |domain info |
|curl |http requests |
|ftp |ftp connection |
|telnet |manual protocol interaction |
