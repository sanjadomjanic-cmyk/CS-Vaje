# Verifying Software Integrity (SHA256 & GPG)

## 🎯 Objectives

In this lab, students will learn how to:

- verify file integrity using SHA256 checksums  
- understand why checksums alone are not enough  
- use GPG to sign and verify files  
- detect tampered software before execution  
- apply secure practices when downloading scripts  

---

## 🧠 Background

When downloading scripts or software from the internet, there is always a risk that:

- the file was modified (tampered)  
- the file was replaced by a malicious version  
- the source cannot be trusted  

To mitigate this, we use:

- **Checksums (SHA256)** → verify integrity  
- **Digital signatures (GPG)** → verify authenticity  

---

## 📁 Lab Setup

You are given the following file:

install.sh

This script simulates a simple software installation.

---

## ⚙️ Task 1: Inspect the Script

Before running any script, always inspect it.

    cat install.sh

👉 Question:
- What does this script do?
  ```text
  The script creates a src directory, creates a run.sh script containing echo Hello, moves it into the src directory, and executes it to display “Hello”.
  ```
FIrst lets install the required packages:

    sudo apt install gnupg coreutils

---

## ⚙️ Task 2: Generate SHA256 Checksum

Create a checksum file:

    sha256sum install.sh > install.sh.sha256

View the checksum:

    cat install.sh.sha256
    b6a4bb8b9df5723e279a46e3090c933402145f7b94532e9165efb53f71f15ae3  install.sh

---

## ⚙️ Task 3: Verify File Integrity

Check if the file is unchanged:

    sha256sum -c install.sh.sha256

Expected output:

    install.sh: OK

---

## ⚙️ Task 4: Generate GPG Key Pair

Generate your GPG key:

    gpg --full-generate-key

Recommended:

- RSA and RSA  
- 4096 bits  
- Set name and email  

List keys:

    gpg --list-keys
    pg: checking the trustdb
    pg: checking the trustdb
    gpg: marginals needed: 3  completes needed: 1  trust model: pgp
    gpg: depth: 0  valid:   4  signed:   0  trust: 0-, 0q, 0n, 0m, 0f, 4u
    gpg: next trustdb check due at 2027-05-27
    /home/SaNjA/gpg-lab/pubring.kbx
    -------------------------------
    pub   rsa4096 2026-05-27 [SCEAR] [expires: 2027-05-27]
      EE53BD167DEDF63BB423033631A19A87598D7090
    uid           [ultimate] Bob <bob@example.com>
    sub   rsa4096 2026-05-27 [SEA] [expires: 2027-05-27]

    pub   rsa4096 2026-05-27 [SCEAR] [expires: 2027-05-27]
      CEF49C5BE70729446212B22BABE631BE84E09797
    uid           [ultimate] Alice <alice@example.com>
    sub   rsa4096 2026-05-27 [SEA] [expires: 2027-05-27]

    pub   rsa4096 2026-05-27 [SCEAR] [expires: 2027-05-27]
      3A74394A2826A54C28CE58E3F6E264FCDFEE4A01
    uid           [ultimate] Mallory <mallory@example.com>
    sub   rsa4096 2026-05-27 [SEA] [expires: 2027-05-27]

    pub   rsa4096 2026-05-27 [SCEAR] [expires: 2027-05-27]
      3C511F2B8A18956E9371A948DA67B138A1D33DCA
    uid           [ultimate] Student <student@example.com>
    sub   rsa4096 2026-05-27 [SEA] [expires: 2027-05-27]



---

## ⚙️ Task 5: Sign the Checksum File

Sign the checksum file:

    gpg --detach-sign install.sh.sha256
    
This creates:

    install.sh.sha256.sig
    

Note to use the same key:

    gpg --list-secret-keys --keyid-format LONG
      --local-user DA67B138A1D33DCA \
    --detach-sign install.sh.sha256
    File 'install.sh.sha256.sig' exists. Overwrite? (y/N) y
    

---

## ⚙️ Task 6: Verify the Signature

Verify that the checksum is authentic:

    gpg --verify install.sh.sha256.sig install.sh.sha256
    gpg: Signature made Wed 27 May 2026 08:57:56 AM EDT
    gpg:                using RSA key 0CD4C13351480065C9FCADB548C8EE8580241043
    gpg: Good signature from "Student <student@example.com>" [ultimate]
```text
The digital signature verification confirms that the checksum file was created by the legitimate private key owner and was not modified.
```
---

## ⚙️ Task 7: Simulate a Tampering Attack

Modify the script:

    echo "echo MALICIOUS CODE EXECUTED" >> install.sh

Now verify again:

    sha256sum -c install.sh.sha256

Expected:

    install.sh: FAILED

---

## ⚙️ Task 8: Safe Execution Workflow

1. Download file  
2. Verify checksum  
3. Verify signature  
4. Execute only if valid  

---

## 📝 Questions

1. Why should you never execute scripts without inspection?
   ```text
   Scripts should never be executed without inspection because they may contain malicious or harmful commands that can compromise the system or steal data.
   ```
2. What does SHA256 guarantee?
```text
   SHA256 guarantees file integrity by detecting any modification or tampering of the file contents.
```
3. What does GPG guarantee?
    ```text
   GPG guarantees authenticity and integrity by verifying that a file or checksum was created by the legitimate private key owner and was not modified.
    ```
4. Can SHA256 prove the author of a file?
   ```text
   No, SHA256 can only verify file integrity, but it cannot prove who created the file.
   ```
5. Why is signing the checksum important?
    ```text
    Signing the checksum is important because it proves that the checksum was created by a trusted author and was not modified by an attacker.
    ```
6.  What happened after the script was modified?
   ```text
After the script was modified, the SHA256 checksum verification failed, indicating that the file integrity had been compromised.
   ``` 

---

## 🧪 Bonus Task (Optional)

- Download a Linux ISO  
- Verify its checksum  
- Verify its GPG signature
- Source: https://www.kali.org/docs/introduction/download-images-securely/

---

## 🧹 Cleanup

    rm -f install.sh.sha256 install.sh.sha256.sig
    rm -rf src

---

## 🔑 Key Takeaways

- Integrity ≠ authenticity  
- Checksums detect changes  
- GPG proves origin  
- Always verify before execution  

---

## ⚠️ Important

Running unverified scripts can lead to:

- system compromise  
- data theft  
- malware infection  

Always follow secure practices.
