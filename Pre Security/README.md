# Offensive Security Intro
I learned how to use gobuster to fuzz URLs, for example:

`(base) ➜  workspace git:(main) ✗ gobuster dir -u https://www.kali.org/ -w rockyou.txt`

# Defensive Security Intro
I know some definitions about blue team like SOC, DFIR, malware,...
Also learn how to basically trace logs:

`inspect alerts -> check IP malicious or not -> contact with responsible people -> if can, block that IP`

# Careers in Cyber
I know the learning path leads to each careers related to security.

# What is Networking?
- Know private network and the networks connecting these small networks are called public networks -- or the Internet.
- To communicate and maintain order, devices must be both identifying and identifiable on a network. Therefore, each device uses: IP Address and a Media Access Control (MAC) Address -- like serial number.
## IP Addresses

![images](ex4.png)

A public address is used to identify the device on the Internet, whereas a private address is used to identify a device amongst other devices. Here we have two devices on a private network:

| Device Name     | IP Address   | IP Address Type |
| --------------- | ------------ | --------------- |
| DESKTOP-KJE57FD | 192.168.1.77 | Private         |
| DESKTOP-KJE57FD | 86.157.52.21 | Public          |
| CMNatic-PC      | 192.168.1.74 | Private         |
| CMNatic-PC      | 86.157.52.21 | Public          |

![images](ex1.png)

These two devices use their private IP addresses to communicate with each others, while any data sent to the Internet will be identified by the same public IP address.
Public IP address are given by our Internet Service Provider (or ISP) at a monthly fee (our bill!!!)

![images](ex2.png)

One version of the Internet Protocol addressing scheme known as IPv4, which can go up to $2^{32}$ IP addresses (4.29 billion) -- too small to satisfy the needs.

IPv6 is a new iteration to help tackle this issue: supports up to $2^{128}$ of IP addresses and more efficient due to new metholodogies.

![images](ex3.png)

## MAC Addresses
All devices have a physical network interface, which is a microchip board found on the device's motherboard. This network interface is assigned a unique address factory it was built at, called a MAC (Media Access Control) address.

The MAC Address is a twelve-char hex number split into two's and separated by a colon which is considered separators. The first six chars represents the company that made the network interface, and the last six is a unique number.

![images](ex5.png)

However, an interacting things with MAC addresses is that they can be faked or 'spoofed' in a process known as spoofing.

Places such as cafes, coffee shops, and hotels alike often use MAC address control when using their "Guest" or "Public" Wi-fi. This configuration could offer better services, i.e. a faster connection for a price if you are willing to pay the fee per device.

## Ping (ICMP)
Ping uses ICMP (Internet Control Message Protocol) packets to determine the performance of a connection between devices, i.e. if the connection exists or is reliable.

The syntax to do a simple ping is: `ping IP address or website URL`.

![images](ex6.png)

Here we are pinging a device that has the private address of 192.168.1.254. Ping informs us that we have sent six ICMP packets, all of which were received with an average time of 4.16 miliseconds. 

# DNS in Detail
DNS (Domain Name System) provides a simple way to communicate with devices on the Internet without remember complexing numbers, which is IP addresses. So instead of remembering 132.12.13.109, you can remember [r1muru2006.github.io](https://r1muru2006.github.io/) instead.

## Domain Hierarchy
![images](ex7.png)
TLD (Top-Level Domain) includes gTLD (Generic Top Level) and ccTLD (Country Code Top Level).
Second-Level Domain is the part `tryhackme` in `tryhackme.com`, while `.com` part is the TLD. SLD is limited to 63 characters + the TLD and can only use `a-z 0-9` and hyphens (not start or end with hyphens or have consecutive hyphens)

Subdomain sits on the left-hand side of the SLD using a period to separate it, i.e. `admin.tryhackme.com` has the subdomain is `admin`. A subdomain name has the same creation restrictions as a SLD. There is no limit to the number of subdomains in a domain name, but the length must be kept to 253 chars or less, i.e. `ronaldo.messi.football.world-cup.youtube.com`.

## DNS Record Types

- A Record: Resolve to IPv4 addresses.
- AAAA Record: Resolve to IPv6 addresses.
- CNAME Record: Resolve to another domain name.
- MX Record: Resolve to the address of the servers that handle the email for the domain you are querying.
- TXT Record: Free text fields where any text-based data can be stored.

## Making a request
![images](ex8.png)

- First, the computer checks its local cache to see if the address were previously looked up recently; if not, a request to Recursive DNS server will be made.
- A Recursive DNS Server is usually provided by our ISP. This server also has a local cache of recently looked up domain names, If a result found, this is sent back to the computer, and our request ends here. If not, it starts with the internet's root DNS servers to find the right answers.
- Then, the root servers redirect us to the correct TLD Server.
- This TLD server holds records for where to find the authoritative server (also known as the nameserver for the domain) to answer the DNS request. There are often multiple nameservers for a domain name to act as a backup in case one goes down.
- Finally, the DNS records is stored in the authoritative DNS server for each particular domain name and also their updates. This record is sent back to the Recursive DNS Server, where a local copy will be cached for future requests and then relayed back to the original client.

**NOTE**: DNS records all come with a TTL (Time To Live) value, which is a number represents in seconds that the response should be saved for locally until we have to look it up again. Caching saves on having to make a DNS request everytime we communicate with a server.

# HTTP in Detail