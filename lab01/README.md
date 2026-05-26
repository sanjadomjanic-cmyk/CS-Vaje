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


```

HTOP is a simple system diagnostics package. You can also try the btop package. The packages show the usage of system resources and processes, which helps us identify suspicious processes that may be running in the background.

```bash
htop
sudo apt install htop # install htop
htop
```

Traceroute is a basic tool for checking network connectivity. Using the tool, we can print the path that packets take through the network and identify potential problems in network nodes.

```bash
htop
sudo apt install traceroute -y # install traceroute
traceroute google.com
```

For a graphical display of upload/download network traffic on the network, we can use the nload package.

```bash
sudo apt install nload -y
nload
```

For simple forensics, we can use the strings package, which can be used to read strings of ASCII or unicode characters from binary files that are readable. The technique is used in reverse engineering and digital forensics.

```bash
strings /bin/ls | head
```

#### 3️⃣ Using tools in Kali Linux

In the following, we will look at and introduce some of the basic tools available within Kali Linux.

First, we will check the data transfer speed using the speedtest-cli package.

```bash
sudo apt install speedtest-cli -y
speedtest-cli --secure
```

We often need to monitor network traffic for forensic analysis or diagnostics, this can also be done using the tcpdump package.

```bash
sudo tcpdump -c 10
```

NMAP and ZenMAP are useful tools for the scanning phase in Kali Linux. NMAP and ZenMAP are practically the same tools, but NMAP uses the command line, while ZenMAP has a graphical user interface.

Nmap allows you to scan by IP address. It also allows you to identify the operating system of the IP device using the -O flag.
```bash
nmap -O 192.168.1.101 # scan by operating system
nmap -p 1-65535 -T4 192.168.1.1 # scan for open TCP and UDP ports
nmap -sS -T4 192.168.1.11 # stealth-scan using SYN/ACK.
```

Searchsploit is a search engine for detected vulnerabilities

```bash
searchsploit wordpress ftp # search for detected vulnerabilities in Wordpress FTP extensions
```

Dnsenum is a script for searching the DNS data of a domain and discovering IP addresses. The main purpose of Dnsenum is to collect as much information about a domain as possible.

```bash
dnsenum google.com # run DNS query
```

The LBD (Load Balancing Detector) tool allows you to detect whether a specific domain uses a Load Balancer or HTTP.

```bash
lbd google.com # check LB
```

Name-That-Hash is a tool that allows you to identify the obtained hash value of a string.

```bash
nth
sudo apt install name-that-hash # install nth
nth -t ef487f75307f96954d3bb132e5f4b035
```
⸻

## 3️⃣ Reflection and Analysis
• Why do we use Kali Linux? What is the advantage of Kali Linux compared to other Linux distributions?
• Which features and tools of Kali Linux attracted you the most?

## References

1. Kali Linux., *Penetration Testing Distribution*, https://www.kali.org/
2. OpenAI, (2025), *ChatGPT* (Aug 2025) [Large language model], https://chat.openai.com/
