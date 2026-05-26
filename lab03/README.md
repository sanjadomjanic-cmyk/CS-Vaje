# Testing SSH Security with Nmap and Hydra

In this exercise, you will test two key techniques for testing the security of remote systems:
- detecting open ports and services with the `nmap` tool
- brute-force attacking an SSH service with the `hydra` tool

The purpose of this exercise is to show how attackers obtain information about a system and why securing the SSH service and closing unused ports is crucial for security.

---

# 🐳 Preparing the environment with Docker

Before starting the exercise, set up the target system with Docker on your host computer.
You will have a Docker image with a vulnerable SSH server that allows you to test attacks.

### 🔷 Step 0: Starting the Docker SSH Server

If you haven't already, first build a Docker image named `dvws`:
```bash
sudo apt update
sudo apt install docker-cli
sudo apt install docker.io
wget https://raw.githubusercontent.com/rpritr/KV-Vaje/refs/heads/main/lab09/dvws/Dockerfile
docker build -t dvws .
```

Then start the container:
```bash
sudo docker run -d -p 2222:22 --name dvws-ssh dvws
```

The SSH server will now be available on the host computer at `<target_ip>`, port `2222`, with user `testuser` and password `test123`.

---

# 🧪 Testing SSH Security with Nmap and Hydra

SSH (Secure Shell) is a standard protocol for remote login to a server. Weak passwords or open unnecessary services allow attackers to quickly gain access.
In this exercise, you will first use `nmap` to identify open ports and services, and then use `hydra` to check the strength of passwords.

---

## 1️⃣ Introduction

The goal is for users to learn how to:
✅ Use Nmap to detect open ports and services
✅ Use Hydra to check SSH passwords
✅ Understand the dangers of weak passwords and open services

---

## 2️⃣ Activity

### 🖥️ Instructions

Students will perform the following steps and document the results:

---

### 🔷 Step 1: Scan for open ports with Nmap

First, check which services are available on the target system:

```bash
nmap -sS -sV -O -p- <target_ip>

┌──(SaNjA㉿kali)-[~/lab03-docker]
└─$ sudo nmap -sS -sV -O -p- 127.0.0.1                                                                                                                                                                                                     
Starting Nmap 7.95 ( https://nmap.org ) at 2026-05-26 15:07 EDT
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00020s latency).
Not shown: 65532 closed tcp ports (reset)
PORT      STATE SERVICE VERSION
22/tcp    open  ssh     OpenSSH 10.2p1 Debian 2 (protocol 2.0)
2222/tcp  open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.15 (Ubuntu Linux; protocol 2.0)
43323/tcp open  http    Golang net/http server
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port43323-TCP:V=7.95%I=7%D=5/26%Time=6A15EF60%P=x86_64-pc-linux-gnu%r(G
SF:enericLines,67,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nContent-Type:\x20
SF:text/plain;\x20charset=utf-8\r\nConnection:\x20close\r\n\r\n400\x20Bad\
SF:x20Request")%r(GetRequest,8F,"HTTP/1\.0\x20404\x20Not\x20Found\r\nDate:
SF:\x20Tue,\x2026\x20May\x202026\x2019:07:12\x20GMT\r\nContent-Length:\x20
SF:19\r\nContent-Type:\x20text/plain;\x20charset=utf-8\r\n\r\n404:\x20Page
SF:\x20Not\x20Found")%r(HTTPOptions,8F,"HTTP/1\.0\x20404\x20Not\x20Found\r
SF:\nDate:\x20Tue,\x2026\x20May\x202026\x2019:07:12\x20GMT\r\nContent-Leng
SF:th:\x2019\r\nContent-Type:\x20text/plain;\x20charset=utf-8\r\n\r\n404:\
SF:x20Page\x20Not\x20Found")%r(RTSPRequest,67,"HTTP/1\.1\x20400\x20Bad\x20
SF:Request\r\nContent-Type:\x20text/plain;\x20charset=utf-8\r\nConnection:
SF:\x20close\r\n\r\n400\x20Bad\x20Request")%r(Help,67,"HTTP/1\.1\x20400\x2
SF:0Bad\x20Request\r\nContent-Type:\x20text/plain;\x20charset=utf-8\r\nCon
SF:nection:\x20close\r\n\r\n400\x20Bad\x20Request")%r(SSLSessionReq,67,"HT
SF:TP/1\.1\x20400\x20Bad\x20Request\r\nContent-Type:\x20text/plain;\x20cha
SF:rset=utf-8\r\nConnection:\x20close\r\n\r\n400\x20Bad\x20Request")%r(Fou
SF:rOhFourRequest,8F,"HTTP/1\.0\x20404\x20Not\x20Found\r\nDate:\x20Tue,\x2
SF:026\x20May\x202026\x2019:07:27\x20GMT\r\nContent-Length:\x2019\r\nConte
SF:nt-Type:\x20text/plain;\x20charset=utf-8\r\n\r\n404:\x20Page\x20Not\x20
SF:Found")%r(LPDString,67,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nContent-T
SF:ype:\x20text/plain;\x20charset=utf-8\r\nConnection:\x20close\r\n\r\n400
SF:\x20Bad\x20Request")%r(SIPOptions,67,"HTTP/1\.1\x20400\x20Bad\x20Reques
SF:t\r\nContent-Type:\x20text/plain;\x20charset=utf-8\r\nConnection:\x20cl
SF:ose\r\n\r\n400\x20Bad\x20Request")%r(Socks5,67,"HTTP/1\.1\x20400\x20Bad
SF:\x20Request\r\nContent-Type:\x20text/plain;\x20charset=utf-8\r\nConnect
SF:ion:\x20close\r\n\r\n400\x20Bad\x20Request")%r(OfficeScan,A3,"HTTP/1\.1
SF:\x20400\x20Bad\x20Request:\x20missing\x20required\x20Host\x20header\r\n
SF:Content-Type:\x20text/plain;\x20charset=utf-8\r\nConnection:\x20close\r
SF:\n\r\n400\x20Bad\x20Request:\x20missing\x20required\x20Host\x20header");
Device type: general purpose
Running: Linux 5.X|6.X
OS CPE: cpe:/o:linux:linux_kernel:5 cpe:/o:linux:linux_kernel:6
OS details: Linux 5.0 - 6.2
Network Distance: 0 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 29.59 seconds


```

Parameters:
- `-sS` — SYN scan (quieter)
- `-sV` — detect service versions
- `-O` — detect operating system (if possible)
- `-p-` — scan all ports (1-65535)

Write down:
- which ports are open
  ```text
  - 22/tcp
  - 2222/tcp
  - 43323/tcp
   ```
- which services are running
  ```text
  - SSH service (OpenSSH 10.2p1 Debian 2) on port 22
  - SSH service (OpenSSH 8.9p1 Ubuntu 3ubuntu0.15) on port 2222
  - HTTP service (Golang net/http server) on port 43323
  ```
- which operating system version was detected
   ```text
  Linux 5.0 - 6.2
  ``` 
💡 Reflection: why close unused ports?
```text
Unused open ports increase the attack surface of a system. Attackers can use open ports to discover running services, identify vulnerabilities, and attempt unauthorized access. Closing unnecessary ports improves system security and reduces the risk of attacks.
```

We can find the IP of the server inside the docker environment with the command
```bash
sudo docker inspect dvws-ssh | grep IPAddress
                                                                                                                                                                                        
            sudo docker inspect dvws-ssh | grep IPAddress
            "SecondaryIPAddresses": null,
            "IPAddress": "172.17.0.2",
                    "IPAddress": "172.17.0.2",

```
---

### 🔷 Step 2: Verify SSH connection

Make sure SSH service is working:
```bash
ssh testuser@<target_ip> -p 22
```
Password: `test123`
```bash
└─$ ssh testuser@172.17.0.2 -p 22                                                                                                                                                                                                          
The authenticity of host '172.17.0.2 (172.17.0.2)' can't be established.
ED25519 key fingerprint is: SHA256:GWWMIFUnvWOJuHlCgxUBsitI96T9RCR4GuC6oQhcI2I
This host key is known by the following other names/addresses:
    ~/.ssh/known_hosts:1: [hashed name]
    ~/.ssh/known_hosts:4: [hashed name]
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '172.17.0.2' (ED25519) to the list of known hosts.
testuser@172.17.0.2's password: 
Welcome to Ubuntu 22.04.5 LTS (GNU/Linux 6.16.8+kali-amd64 x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

This system has been minimized by removing packages and content that are
not required on a system that users do not log into.

To restore this content, you can run the 'unminimize' command.

The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

testuser@5ba0b9d2b580:~$ 
```
---

### 🔷 Step 3: Create a password list

For a faster test, create your own password list:
```bash
echo -e "password
123456
test123
admin" > passwords.txt
```

---

### 🔷 Step 4: Brute-force attack with Hydra

Use Hydra to attack:
```bash
hydra -l testuser -P passwords.txt -s 22 <target_ip> ssh
```

Parameters:
- `-l testuser` — username
- `-P passwords.txt` — password list
- `-s 22` — number port
- `<target_ip>` — Server IP address
- `ssh` — protocol

On success, Hydra will print something like this:
```
[22][ssh] host: <target_ip> login: testuser password: test123

┌──(SaNjA㉿kali)-[~/lab03-docker]
└─$ hydra -l testuser -P passwords.txt -s 22 172.17.0.2 ssh                                                                                                                                                                                
Hydra v9.6 (c) 2023 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2026-05-26 15:18:26
[WARNING] Many SSH configurations limit the number of parallel tasks, it is recommended to reduce the tasks: use -t 4
[DATA] max 4 tasks per 1 server, overall 4 tasks, 4 login tries (l:1/p:4), ~1 try per task
[DATA] attacking ssh://172.17.0.2:22/
[22][ssh] host: 172.17.0.2   login: testuser   password: test123
1 of 1 target successfully completed, 1 valid password found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2026-05-26 15:18:30


```

---

## 3️⃣ Analysis and report

Submit a report with the following contents:
- Output of `nmap` results (which services/ports are open)
  ```text
  ## Nmap Scan Results

```bash
sudo nmap -sS -sV -O -p- 127.0.0.1
```

```text
PORT      STATE SERVICE VERSION
22/tcp    open  ssh     OpenSSH 10.2p1 Debian 2
2222/tcp  open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.15
43323/tcp open  http    Golang net/http server
```
The Nmap scan detected multiple open ports and services on the local system. The vulnerable Docker SSH server was running on port 2222.


- Output of `hydra` results (whether the password was found)
  ## Hydra Results

```bash
hydra -l testuser -P passwords.txt -s 22 172.17.0.2 ssh
```

```text
[22][ssh] host: 172.17.0.2   login: testuser   password: test123
1 of 1 target successfully completed, 1 valid password found.
```

The Hydra attack successfully identified the correct SSH password for the user `testuser`.

  
- Screenshots of both results
<img width="1920" height="980" alt="VirtualBox_kali-linux-2025 4-virtualbox-amd64_26_05_2026_21_27_14" src="https://github.com/user-attachments/assets/33c32aba-4730-4ba6-bf30-88bdb7fbd1a1" />


- Short comment: why using weak passwords is dangerous and why closing unused ports
  ```text
  Weak passwords are dangerous because attackers can easily guess or brute-force them using automated tools such as Hydra. This can lead to unauthorized access to systems and sensitive data. Unused open ports increase the attack surface of a system. Attackers can scan open ports to discover running services and possible vulnerabilities. Closing unnecessary ports improves overall system security.
  ```

## 4️⃣ Reflection and analysis

- How would you protect the SSH server from brute-force attacks?
 ```text
SSH servers can be protected from brute-force attacks by using strong passwords, disabling password authentication, and using SSH keys instead. Additional protection methods include changing the default SSH port, limiting login attempts, configuring a firewall, and using tools such as Fail2Ban to automatically block suspicious login attempts.
  ```
- What additional measures (e.g. limits on the number of logins, use of public-private keys, firewall) would you recommend?
   ```text
   Additional security measures include limiting the number of login attempts, enabling firewall rules, using public-private SSH keys instead of passwords, disabling root login, and using tools such as Fail2Ban to block repeated failed login attempts.
    ```
- How does the result change if we use a very strong password?
 ```text
- If a very strong password is used, brute-force attacks become significantly more difficult and time-consuming. Hydra would require many more attempts, making it much less likely that the password could be successfully guessed.
   ```
