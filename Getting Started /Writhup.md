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

```
root㉿kali)-[~/Desktop/HTB/sts]
└─# nmap -sV -p- -Pn 10.129.110.173
Starting Nmap 7.95 ( https://nmap.org ) at 2026-07-20 14:37 EDT
Nmap scan report for 10.129.110.173
Host is up (0.60s latency).
Not shown: 65528 closed tcp ports (reset)
PORT     STATE SERVICE     VERSION
21/tcp   open  ftp         vsftpd 3.0.3
22/tcp   open  ssh         OpenSSH 8.2p1 Ubuntu 4ubuntu0.1 (Ubuntu Linux; protocol 2.0)
80/tcp   open  http        Apache httpd 2.4.41 ((Ubuntu))
139/tcp  open  netbios-ssn Samba smbd 4
445/tcp  open  netbios-ssn Samba smbd 4
2323/tcp open  telnet      Linux telnetd
8080/tcp open  http        Apache Tomcat
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 3014.26 seconds
```

