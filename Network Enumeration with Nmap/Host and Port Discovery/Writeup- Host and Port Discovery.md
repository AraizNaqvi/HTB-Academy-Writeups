
## **Overview**

- **Difficulty:** Easy
- **Operating System:** Linux
- **Objective:** Scan and find TCP ports open and hostname
- **Tools Used:** `nmap`

---
## **Scanning all TCP ports**

Let's first start with scanning all popular default ports using the `-sS` flag:
```
$ sudo nmap -sS 10.129.143.118 -disable-arp-ping -n -Pn -oA finding-TCP-ports
 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-01-09 14:55 IST
Stats: 0:01:21 elapsed; 0 hosts completed (1 up), 1 undergoing SYN Stealth Scan
SYN Stealth Scan Timing: About 99.99% done; ETC: 14:56 (0:00:00 remaining)
Nmap scan report for 10.129.143.118
Host is up (0.33s latency).
Not shown: 993 closed tcp ports (reset)
PORT      STATE SERVICE
22/tcp    open  ssh
80/tcp    open  http
110/tcp   open  pop3
139/tcp   open  netbios-ssn
143/tcp   open  imap
445/tcp   open  microsoft-ds
31337/tcp open  Elite

Nmap done: 1 IP address (1 host up) scanned in 131.63 seconds

```

Clearly, there are 7 open ports.
Now, let's enumerate the services which will also reveal the service versions.

- - -
## **Scanning Service Versions**

Now, we will scan (I should've scanned for the specific ports I found above, but I missed out on that) using the `-sV` flag:
```
$ sudo nmap -sV 10.129.143.118 --disable-arp-ping -n -Pn -oA service-scans

Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-01-09 14:58 IST
Stats: 0:01:26 elapsed; 0 hosts completed (1 up), 1 undergoing Service Scan
Service scan Timing: About 85.71% done; ETC: 15:00 (0:00:11 remaining)
Stats: 0:02:27 elapsed; 0 hosts completed (1 up), 1 undergoing Service Scan
Service scan Timing: About 85.71% done; ETC: 15:01 (0:00:22 remaining)
Nmap scan report for 10.129.143.118
Host is up (0.45s latency).
Not shown: 993 closed tcp ports (reset)
PORT      STATE SERVICE     VERSION
22/tcp    open  ssh         OpenSSH 7.6p1 Ubuntu 4ubuntu0.7 (Ubuntu Linux; protocol 2.0)
80/tcp    open  http        Apache httpd 2.4.29 ((Ubuntu))
110/tcp   open  pop3        Dovecot pop3d
139/tcp   open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
143/tcp   open  imap        Dovecot imapd (Ubuntu)
445/tcp   open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
31337/tcp open  Elite?
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port31337-TCP:V=7.94SVN%I=7%D=1/9%Time=677F96D2%P=x86_64-pc-linux-gnu%r
SF:(GetRequest,1F,"220\x20HTB{pr0F7pDv3r510nb4nn3r}\r\n");
Service Info: Host: NIX-NMAP-DEFAULT; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 187.90 seconds

```

At the end you'll see:
![[Pasted image 20250109150947.png]]

This is the hostname.
A1: `7`
A2: `NIX-NMAP-DEFAULT`

---

**Prepared by Araiz Naqvi**