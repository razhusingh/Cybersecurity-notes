# introduction
Nmap = network mapper

it is used to:
- discover live hosts
- find open ports
- identify running services
- detect service versions
- control scan speed/timings
- save scan output

# host discovery: who is online
purpose 
before scanning ports, first check which hosts are alive

list scan
- nmap -sL 192.168.0.1/27
- -sL list targets without scanning them

ping scan/host discovery
- nmap -sn target
- -sn discovers live hosts without port scanning

# port scanning: who is listening
purpose 
port scanning checks which ports are open on a target

tcp connect scan
- nmap -sT target_ip
- uses full tcp connection
- does not require root privileges

SYN scan(stealth)
- half open scan
- faster and stelthier than tcp connect scan
- requires sudo/root privileges

scan all ports
- nmap -p- target_ip

scan specific ports
- nmap -p 22,80,443 target_ip

Summary
|Option	|Explanation|
|-------|-----------|
|-sT |TCP connect scan – complete three-way handshake|
|-sS |TCP SYN – only first step of the three-way handshake|
|-sU |UDP scan |
|-F	|Fast mode – scans the 100 most common ports |
|-p[range]	|Specifies a range of port numbers – -p- scans all the ports|

# version detection: extract more information
purpose
after finding open ports, use version detecton to identify services

version detection
- nmap -sV target_ip
- -sV detects service versions

example output meaning
```
80/tcp open http apache httpd 2.4.x
```
means:
- port: 80
- state: open
- service: http
- version: apache 2.4.x
Summary
|Option |Explanation |
|-------|------------|
|-O	|OS detection |
|-sV |Service and version detection|
|-A	|OS detection, version detection, and other additions|
|-Pn |Scan hosts that appear to be down |

# timimg: how fast?
purpose
nmap timing controls scan speed

timing templates
```
nmap -t0 target
nmap -t1 target
nmap -t2 target
nmap -t3 target
nmap -t4 target
nmap -t5 target
```

| timing | meaning |
|--------|---------|
|-t0 |paranoid |
|-t1 |sneaky |
|-t2 |polite |
|-t3 |normal |
|-t4 |aggressive |
|-t5 |insane |

most common practical option:
- nmap -t4 target_ip

# output: controlling what you see
normal output
- nmap -oN scan.txt target_ip

grepable output
- nmap -oG scan.gnmap target_ip

xml output
- nmap -oX scan.xml target_ip

all formats
- nmap -oA scan target_ip

this creates:
- scan.nmap
- scan.gnmap
- scan.xml

# useful scan options
disable dns resolution
- nmap -n target_ip

increase verbosity
- nmap -v target_ip

more verbosity
- nmap -vv target_ip

show reason for result
- nmap --reason target_ip

treat host as online
- nmap -Pn target_ip
- useful when ping is blocked

Important Commands Summary
|Command |	Purpose|
|--------|---------|
|nmap -sL TARGET |List targets |
|nmap -sn TARGET |Host discovery only |
|nmap -sT TARGET |TCP connect scan |
|sudo nmap -sS TARGET |SYN scan |
|nmap -sV TARGET |Version detection |
|nmap -p- TARGET |Scan all ports |
|nmap -p 22,80,443 TARGET |Scan selected ports |
|nmap -T4 TARGET |Faster scan |
|nmap -oN file.txt TARGET |Save normal output |
|nmap -oA name TARGET |Save all output formats |
|nmap -Pn TARGET |Skip host discovery |

|Option	|Explanation |
|-------|------------|
\-sL	|List scan – list targets without scanning|
|host discovery |---------|
|-sn	|Ping scan – host discovery only|
|Port Scanning	|------------|
|-sT	|TCP connect scan – complete three-way handshake|
|-sS	|TCP SYN – only first step of the three-way handshake|
|-sU	|UDP Scan|
|-F	|Fast mode – scans the 100 most common ports|
|-p[range]	|Specifies a range of port numbers – -p- scans all the ports|
|-Pn	|Treat all hosts as online – scan hosts that appear to be down|
|Service Detection |---------------|	
|-O	|OS detection|
|-sV |Service version detection|
|-A	|OS detection, version detection, and other additions|
|Timing	|------------|
|-T<0-5> |Timing template – paranoid (0), sneaky (1), polite (2), normal(3), aggressive (4), and insane (5) |
|--min-parallelism <numprobes> and --max-parallelism <numprobes> |Minimum and maximum number of parallel probes |
|--min-rate <number> and --max-rate <number> |Minimum and maximum rate (packets/second) |
|--host-timeout |Maximum amount of time to wait for a target host |
|Real-time output |-----------------|
|-v	|Verbosity level – for example, -vv and -v4 |
|-d	|Debugging level – for example -d and -d9|
|Report	|------------------|
|-oN <filename> |Normal output |
|-oX <filename>	|XML output |
|-oG <filename>	|grep-able output |
|-oA <basename>	|Output in all major formats |