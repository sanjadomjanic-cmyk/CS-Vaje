# Introduction to Kali Linux

In this tutorial, you will learn about the **Kali Linux** distribution, which is the standard Linux distribution for security testing and ethical hacking. You will learn about the purpose of using Kali Linux, its main tools, and basic concepts that every security professional should know.

# 🧪 Introduction to Kali Linux

Kali Linux is a specialized Linux distribution used by security professionals to perform penetration testing, network analysis, forensic analysis, and other security tasks. It contains more than 600 pre-installed tools.
Knowing the Kali Linux environment is important because it allows you to perform attack simulations and discover vulnerabilities before attackers exploit them.

---

## 1️⃣ Introduction

The goal of the exercise is for us as users to learn how to:
✅ understand the purpose and role of Kali Linux in cybersecurity
✅ get to know the basic graphical and command environment of Kali Linux
✅ find and run some key tools
✅ execute basic commands and analyze the results

---

## 2️⃣ Working with Kali Linux

### 🖥️ Instructions

In the following, we will look at how to install and run Kali Linux. We will also look at some basic commands.

---

#### 1️⃣ Installing Kali Linux

Basic information about Kali Linux can be found at: [https://www.kali.org](https://www.kali.org)

Instructions for installing Kali Linux are available at: [https://www.kali.org/docs/installation/](https://www.kali.org/docs/installation/)

Kali Linux download images can be found at: [https://www.kali.org/get-kali/#kali-platforms](https://www.kali.org/get-kali/#kali-platforms)

I recommend using it inside a VMWare or VirtualBox virtual environment.

On Windows, you can install Kali Linux in the WSL environment: [https://www.kali.org/get-kali/#kali-wsl](https://www.kali.org/get-kali/#kali-wsl)

On Mac OS X, I suggest using WMware Fusion [https://www.kali.org/docs/virtualization/install-vmware-silicon-host/](https://www.kali.org/docs/virtualization/install-vmware-silicon-host/)

---

#### 2️⃣ Starting the Kali Linux environment

Kali Linux uses the Xfce graphical environment, other graphical environments are also available within the Linux OS: GNOME, KDE, Cinnamon, Pantheon, ...

Explore the Kali Linux graphical environment:
- Start the virtual environment with **Kali Linux**.
  Started Kali Linux virtual machine in Oracle VirtualBox.
  
- Explore the graphical environment (menus, system information).
  Explored the Kali Linux Xfce graphical environment and reviewed system information and menus.
  
- Find the security tools menu and review the 5 tools you find.
  Security tools reviewed: Nmap, Wireshark, John the Ripper, Burp Suite, Metasploit Framework
  
- find operating system settings
  <img width="645" height="535" alt="Posnetek zaslona 2026-05-26 174934" src="https://github.com/user-attachments/assets/ba066539-77aa-41e7-af12-25a436fee5f4" />
  
- sort file system
  Explored the Linux file system using the file manager.

---

#### 3️⃣ Basic Command Line Commands
Open **terminal** and run the following commands and record the results.

| Command | Meaning |
|--------------------|------|
| `whoami` | Show logged in user |
| `hostnamectl` | Show hostname and OS |
| `uname -a` | Show kernel information |
| `df -h` | Show disk usage |
| `ip a` | Show network settings |
| `wget url` | Download files from URL |
| `sudo apt install package_name` | Install packages using APT |

Example:
```bash
whoami
SaNjA

hostnamectl
 Static hostname: kali
       Icon name: computer-vm
         Chassis: vm 🖴
      Machine ID: b69758c0cad3481e967dcad827001d56
         Boot ID: ce49d74836cb4fd6a477d34f46dc4822
  Virtualization: oracle
Operating System: Kali GNU/Linux Rolling          
          Kernel: Linux 6.16.8+kali-amd64
    Architecture: x86-64
 Hardware Vendor: innotek GmbH
  Hardware Model: VirtualBox
Hardware Version: 1.2
Firmware Version: VirtualBox
   Firmware Date: Fri 2006-12-01
    Firmware Age: 19y 5month 3w 3d

uname -a
Linux kali 6.16.8+kali-amd64 #1 SMP PREEMPT_DYNAMIC Kali 6.16.8-1kali1 (2025-09-24) x86_64 GNU/Linux

df -h
Filesystem      Size  Used Avail Use% Mounted on
udev            883M     0  883M   0% /dev
tmpfs           198M  984K  197M   1% /run
/dev/sda1        79G   19G   57G  25% /
tmpfs           986M  4.0K  986M   1% /dev/shm
none            1.0M     0  1.0M   0% /run/credentials/systemd-journald.service
tmpfs           986M  100K  986M   1% /tmp
AppliedCrypto   238G  234G  4.7G  99% /media/sf_AppliedCrypto
none            1.0M     0  1.0M   0% /run/credentials/getty@tty1.service
tmpfs           198M  104K  198M   1% /run/user/1000

ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:63:b0:05 brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic noprefixroute eth0
       valid_lft 78454sec preferred_lft 78454sec
    inet6 fd17:625c:f037:2:839f:6ded:fa07:4972/64 scope global dynamic noprefixroute 
       valid_lft 86096sec preferred_lft 14096sec
    inet6 fe80::2906:7497:903f:e74e/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever


wget https://gist.githubusercontent.com/EdwardRayl/3436572afde8ce9e3faf5b7b95356a49/raw/6b25895fce480713560829dec31ac8220ffe5272/gists.txt
--2026-05-26 11:57:34--  https://gist.githubusercontent.com/EdwardRayl/3436572afde8ce9e3faf5b7b95356a49/raw/6b25895fce480713560829dec31ac8220ffe5272/gists.txt
Resolving gist.githubusercontent.com (gist.githubusercontent.com)... 185.199.110.133, 185.199.111.133, 185.199.108.133, ...
Connecting to gist.githubusercontent.com (gist.githubusercontent.com)|185.199.110.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 9634 (9.4K) [text/plain]
Saving to: ‘gists.txt’

gists.txt                                                  100%[=======================================================================================================================================>]   9.41K  --.-KB/s    in 0.001s  

2026-05-26 11:57:35 (9.50 MB/s) - ‘gists.txt’ saved [9634/9634]

sudo apt install 7zip
[sudo] password for SaNjA: 
Upgrading:                      
  7zip

Summary:
  Upgrading: 1, Installing: 0, Removing: 0, Not Upgrading: 2036
  Download size: 1,610 kB
  Space needed: 7,168 B / 60.3 GB available

Get:1 http://http.kali.org/kali kali-rolling/main amd64 7zip amd64 26.01+dfsg-2 [1,610 kB]
Fetched 1,610 kB in 1s (2,413 kB/s)
(Reading database ... 422190 files and directories currently installed.)
Preparing to unpack .../7zip_26.01+dfsg-2_amd64.deb ...
Unpacking 7zip (26.01+dfsg-2) over (25.01+dfsg-4) ...
Setting up 7zip (26.01+dfsg-2) ...
Processing triggers for kali-menu (2025.4.3) ...
Processing triggers for man-db (2.13.1-1) ...

which nmap
/usr/bin/nmap

which john
/usr/sbin/john

cd /
┌──(SaNjA㉿kali)-[~/linux-exercise/test]
└─$ cd /

┌──(SaNjA㉿kali)-[/]
└─$ 

ls -la
total 976640
drwxr-xr-x  18 root root       4096 Dec  2 22:02 .
drwxr-xr-x  18 root root       4096 Dec  2 22:02 ..
lrwxrwxrwx   1 root root          7 Nov 10  2025 bin -> usr/bin
drwxr-xr-x   3 root root       4096 Dec  2 22:03 boot
drwxr-xr-x  18 root root       3240 May 26 09:44 dev
drwxr-xr-x 180 root root      12288 May 26 11:30 etc
drwxr-xr-x   6 root root       4096 May 26 09:48 home
lrwxrwxrwx   1 root root         33 Dec  2 22:02 initrd.img -> boot/initrd.img-6.16.8+kali-amd64
lrwxrwxrwx   1 root root         33 Dec  2 22:02 initrd.img.old -> boot/initrd.img-6.16.8+kali-amd64
lrwxrwxrwx   1 root root          7 Nov 10  2025 lib -> usr/lib
lrwxrwxrwx   1 root root          9 Dec  2 21:33 lib32 -> usr/lib32
lrwxrwxrwx   1 root root          9 Nov 10  2025 lib64 -> usr/lib64
drwx------   2 root root      16384 Dec  2 22:01 lost+found
drwxr-xr-x   3 root root       4096 May 16 05:27 media
drwxr-xr-x   2 root root       4096 Dec  2 21:29 mnt
drwxr-xr-x   3 root root       4096 Dec  2 21:33 opt
dr-xr-xr-x 237 root root          0 May 26 09:44 proc
drwx------   6 root root       4096 May 26 09:49 root
drwxr-xr-x  36 root root        900 May 26 09:56 run
lrwxrwxrwx   1 root root          8 Nov 10  2025 sbin -> usr/sbin
drwxr-xr-x   3 root root       4096 Dec  2 21:34 srv
-rw-------   1 root root 1000000000 Dec  2 22:02 swap
dr-xr-xr-x  13 root root          0 May 26 09:44 sys
drwxrwxrwt  13 root root        340 May 26 11:55 tmp
drwxr-xr-x  15 root root       4096 Dec  2 21:33 usr
drwxr-xr-x  12 root root       4096 Feb  6 11:21 var
lrwxrwxrwx   1 root root         30 Dec  2 22:02 vmlinuz -> boot/vmlinuz-6.16.8+kali-amd64
lrwxrwxrwx   1 root root         30 Dec  2 22:02 vmlinuz.old -> boot/vmlinuz-6.16.8+kali-amd64

```

HTOP is a simple system diagnostics package. You can also try the btop package. The packages show the usage of system resources and processes, which helps us identify suspicious processes that may be running in the background.

```bash
htop
sudo apt install htop # install htop
htop
```
<img width="1920" height="1075" alt="VirtualBox_kali-linux-2025 4-virtualbox-amd64_26_05_2026_18_13_54" src="https://github.com/user-attachments/assets/ef51a088-a9de-4bc1-a661-e09c50a61b3b" />


Traceroute is a basic tool for checking network connectivity. Using the tool, we can print the path that packets take through the network and identify potential problems in network nodes.

```bash
htop
sudo apt install traceroute -y # install traceroute
traceroute google.com

traceroute to google.com (142.251.209.14), 30 hops max, 60 byte packets
 1  10.0.2.2 (10.0.2.2)  3.147 ms  2.994 ms  2.890 ms
 2  * * *
 3  * * *
 4  * * *
 5  * * *
 6  * * *
 7  * * *
 8  * * *
 9  * * *
10  * * *
11  * * *
12  * * *
13  * * *
14  * * *
15  * * *
16  * * *
17  * * *
18  * * *
19  * * *
20  * * *
21  * * *
22  * * *
23  * * *
24  * * *
25  * * *
26  * * *
27  * * *
28  * * *
29  * * *
30  * * *

```

For a graphical display of upload/download network traffic on the network, we can use the nload package.

```bash
sudo apt install nload -y
nload
```
<img width="1920" height="1075" alt="VirtualBox_kali-linux-2025 4-virtualbox-amd64_26_05_2026_18_22_07" src="https://github.com/user-attachments/assets/22d9415c-c1f1-4018-90d6-d8775269e069" />


For simple forensics, we can use the strings package, which can be used to read strings of ASCII or unicode characters from binary files that are readable. The technique is used in reverse engineering and digital forensics.

```bash
strings /bin/ls | head
!/lib64/ld-linux-x86-64.so.2
_ITM_deregisterTMCloneTable
__gmon_start__
_ITM_registerTMCloneTable
fgetfilecon_raw
fgetfilecon
freecon
lgetfilecon
lgetfilecon_raw
_IO_stdin_used

```

#### 3️⃣ Using tools in Kali Linux

In the following, we will look at and introduce some of the basic tools available within Kali Linux.

First, we will check the data transfer speed using the speedtest-cli package.

```bash
sudo apt install speedtest-cli -y
speedtest-cli --secure
Retrieving speedtest.net configuration...
Testing from T-2 (89.212.2.11)...
Retrieving speedtest.net server list...
Selecting best server based on ping...
Hosted by Wien Energie Superschnell (Vienna) [278.51 km]: 15.118 ms
Testing download speed................................................................................
Download: 244.07 Mbit/s
Testing upload speed......................................................................................................
Upload: 105.49 Mbit/s
```

We often need to monitor network traffic for forensic analysis or diagnostics, this can also be done using the tcpdump package.

```bash
sudo tcpdump -c 10
[sudo] password for SaNjA: 
tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
listening on eth0, link-type EN10MB (Ethernet), snapshot length 262144 bytes
12:35:57.891553 IP 10.0.2.15.41010 > 206.189.246.93.ssh: Flags [.], ack 1058626729, win 61513, length 0
12:35:57.899758 IP 206.189.246.93.ssh > 10.0.2.15.41010: Flags [.], ack 1, win 65535, length 0
12:35:57.923346 IP 10.0.2.15.47712 > dnslj1.t-2.net.domain: 6508+ PTR? 93.246.189.206.in-addr.arpa. (45)
12:35:58.133373 IP dnslj1.t-2.net.domain > 10.0.2.15.47712: 6508 NXDomain 0/1/0 (112)
12:35:58.145785 IP 10.0.2.15.49876 > dnslj1.t-2.net.domain: 28109+ PTR? 15.2.0.10.in-addr.arpa. (40)
12:35:58.152816 IP dnslj1.t-2.net.domain > 10.0.2.15.49876: 28109 NXDomain* 0/1/0 (99)
12:35:58.162302 IP 10.0.2.15.60564 > dnslj1.t-2.net.domain: 5140+ PTR? 79.209.255.84.in-addr.arpa. (44)
12:35:58.169439 IP dnslj1.t-2.net.domain > 10.0.2.15.60564: 5140 1/0/0 PTR dnslj1.t-2.net. (72)
12:36:03.062574 ARP, Request who-has 10.0.2.2 tell 10.0.2.15, length 28
12:36:03.063050 ARP, Reply 10.0.2.2 is-at 52:55:0a:00:02:02 (oui Unknown), length 50
10 packets captured
12 packets received by filter
0 packets dropped by kernel

```

NMAP and ZenMAP are useful tools for the scanning phase in Kali Linux. NMAP and ZenMAP are practically the same tools, but NMAP uses the command line, while ZenMAP has a graphical user interface.

Nmap allows you to scan by IP address. It also allows you to identify the operating system of the IP device using the -O flag.
```bash
nmap -O 192.168.1.101 # scan by operating system
Starting Nmap 7.95 ( https://nmap.org ) at 2026-05-26 12:38 EDT
Nmap scan report for 192.168.1.101
Host is up (0.0016s latency).
All 1000 scanned ports on 192.168.1.101 are in ignored states.
Not shown: 1000 filtered tcp ports (no-response)
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Aggressive OS guesses: 3Com 4500G switch (92%), H3C Comware 5.20 (92%), Huawei VRP 8.100 (92%), Microsoft Windows Server 2003 SP1 (92%), Oracle Virtualbox Slirp NAT bridge (92%), QEMU user mode network gateway (92%), AXIS 2100 Network Camera (92%), D-Link DP-300U, DP-G310, or Hamlet HPS01UU print server (92%), HP Tru64 UNIX 5.1A (92%), Sanyo PLC-XU88 digital video projector (92%)
No exact OS matches for host (test conditions non-ideal).

OS detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 15.30 seconds

nmap -p 1-65535 -T4 192.168.1.1 # scan for open TCP and UDP ports
Starting Nmap 7.95 ( https://nmap.org ) at 2026-05-26 12:39 EDT
Nmap scan report for 192.168.1.1
Host is up (0.051s latency).
All 65535 scanned ports on 192.168.1.1 are in ignored states.
Not shown: 65534 filtered tcp ports (no-response), 1 filtered tcp ports (net-unreach)

Nmap done: 1 IP address (1 host up) scanned in 273.39 seconds

nmap -sS -T4 192.168.1.11 # stealth-scan using SYN/ACK.
Starting Nmap 7.95 ( https://nmap.org ) at 2026-05-26 12:53 EDT
Nmap scan report for 192.168.1.11
Host is up (0.0030s latency).
All 1000 scanned ports on 192.168.1.11 are in ignored states.
Not shown: 1000 filtered tcp ports (no-response)

Nmap done: 1 IP address (1 host up) scanned in 11.45 seconds

```

Searchsploit is a search engine for detected vulnerabilities

```bash
searchsploit wordpress ftp # search for detected vulnerabilities in Wordpress FTP extensions
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
 Exploit Title                                                                                                                                                                                           |  Path
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
WordPress Plugin MiwoFTP 1.0.5 - Arbitrary File Download (1)                                                                                                                                             | php/webapps/36774.txt
WordPress Plugin MiwoFTP 1.0.5 - Arbitrary File Download (2)                                                                                                                                             | php/webapps/36801.txt
WordPress Plugin MiwoFTP 1.0.5 - Cross-Site Request Forgery / Arbitrary File Creation / Remote Code Execution                                                                                            | php/webapps/36763.txt
WordPress Plugin MiwoFTP 1.0.5 - Cross-Site Request Forgery / Arbitrary File Deletion                                                                                                                    | php/webapps/36761.txt
WordPress Plugin MiwoFTP 1.0.5 - Multiple Cross-Site Request Forgery / Cross-Site Scripting Vulnerabilities                                                                                              | php/webapps/36762.txt
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
Shellcodes: No Results

```

Dnsenum is a script for searching the DNS data of a domain and discovering IP addresses. The main purpose of Dnsenum is to collect as much information about a domain as possible.

```bash
dnsenum google.com # run DNS query
```
<img width="1920" height="1075" alt="VirtualBox_kali-linux-2025 4-virtualbox-amd64_26_05_2026_19_01_55" src="https://github.com/user-attachments/assets/b7e9adce-7f66-469b-92f5-058da31382aa" />


The LBD (Load Balancing Detector) tool allows you to detect whether a specific domain uses a Load Balancer or HTTP.

```bash
lbd google.com # check LB
lbd - load balancing detector 0.4 - Checks if a given domain uses load-balancing.
                                    Written by Stefan Behte (http://ge.mine.nu)
                                    Proof-of-concept! Might give false positives.

Checking for DNS-Loadbalancing: NOT FOUND
Checking for HTTP-Loadbalancing [Server]: 
 gws
 NOT FOUND

Checking for HTTP-Loadbalancing [Date]: 17:06:20, 17:06:21, 17:06:21, 17:06:21, 17:06:21, 17:06:22, 17:06:22, 17:06:22, 17:06:23, 17:06:23, 17:06:23, 17:06:23, 17:06:24, 17:06:24, 17:06:24, 17:06:25, 17:06:25, 17:06:25, 17:06:25, 17:06:26, 17:06:26, 17:06:26, 17:06:27, 17:06:27, 17:06:27, 17:06:27, 17:06:28, 17:06:28, 17:06:28, 17:06:29, 17:06:29, 17:06:29, 17:06:29, 17:06:30, 17:06:30, 17:06:30, 17:06:31, 17:06:31, 17:06:31, 17:06:31, 17:06:32, 17:06:32, 17:06:32, 17:06:32, 17:06:33, 17:06:33, 17:06:33, 17:06:34, 17:06:34, 17:06:34, NOT FOUND

Checking for HTTP-Loadbalancing [Diff]: FOUND
< Content-Security-Policy-Report-Only: object-src 'none';base-uri 'self';script-src 'nonce-wtEGOW8EDMhaQIKJLdU2RQ' 'strict-dynamic' 'report-sample' 'unsafe-eval' 'unsafe-inline' https: http:;report-uri https://csp.withgoogle.com/csp/gws/other-hp
< Expires: Thu, 25 Jun 2026 17:06:34 GMT
> Content-Security-Policy-Report-Only: object-src 'none';base-uri 'self';script-src 'nonce-d1UyZ-Le2zNlH5ao7Z6jqA' 'strict-dynamic' 'report-sample' 'unsafe-eval' 'unsafe-inline' https: http:;report-uri https://csp.withgoogle.com/csp/gws/other-hp
> Expires: Thu, 25 Jun 2026 17:06:35 GMT

google.com does Load-balancing. Found via Methods: HTTP[Diff]
```


Name-That-Hash is a tool that allows you to identify the obtained hash value of a string.

```bash
nth
sudo apt install name-that-hash # install nth
nth -t ef487f75307f96954d3bb132e5f4b035
```
<img width="1920" height="507" alt="VirtualBox_kali-linux-2025 4-virtualbox-amd64_26_05_2026_19_09_49" src="https://github.com/user-attachments/assets/e5a0d18f-c2ac-4435-b485-fdf0ef4c2969" />

⸻

## 3️⃣ Reflection and Analysis
• Why do we use Kali Linux? What is the advantage of Kali Linux compared to other Linux distributions?
Kali Linux is a Linux distribution designed for cybersecurity, penetration testing, and digital forensics. It includes many preinstalled security tools that are useful for ethical hacking, network analysis, vulnerability assessment, and system diagnostics. Compared to other Linux distributions, Kali Linux is specialized for security-related tasks and provides a ready-to-use environment for cybersecurity professionals and students.

• Which features and tools of Kali Linux attracted you the most?
The most interesting features were the large number of integrated security tools and the organization of tools by categories. I found tools such as Nmap, tcpdump, SearchSploit, and dnsenum especially useful for network analysis and security testing. I also liked the lightweight Xfce graphical environment and the ability to use both graphical and command-line tools.

## References

1. Kali Linux., *Penetration Testing Distribution*, https://www.kali.org/
2. OpenAI, (2025), *ChatGPT* (Aug 2025) [Large language model], https://chat.openai.com/
