```
nmap -Pn --min-rate 5000 -T4 -p- 10.129.109.18
Starting Nmap 7.95 ( https://nmap.org ) at 2026-07-19 17:03 EDT
Nmap scan report for 10.129.109.18
Host is up (7.9s latency).
Not shown: 64352 filtered tcp ports (no-response), 1177 closed tcp ports (reset)
PORT     STATE SERVICE
21/tcp   open  ftp
22/tcp   open  ssh
80/tcp   open  http
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
8080/tcp open  http-proxy

Nmap done: 1 IP address (1 host up) scanned in 29.11 seconds
```
```
(root㉿kali)-[~/Desktop/HTB/sts]
└─# nmap -Pn -sV -sC -p 8080 10.129.109.18 
Starting Nmap 7.95 ( https://nmap.org ) at 2026-07-19 17:18 EDT
Nmap scan report for 10.129.109.18
Host is up (1.0s latency).

PORT     STATE SERVICE VERSION
8080/tcp open  http    Apache Tomcat
|_http-open-proxy: Proxy might be redirecting requests
|_http-title: Apache Tomcat

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 29.48 seconds
```
