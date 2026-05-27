# GPG: Key Generation, Encryption, and Signing

## 🎯 Exercise Objective
In this exercise, you will practically use **GPG (GNU Privacy Guard)** to:
- generate a key pair,
- export and import a public key,
- encrypt a file,
- digitally sign,
- decrypt and verify a signature.

---

## 🧰 Requirements
- Linux / Ubuntu
- `gnupg` package installed

Installation (if not already installed):

```bash
sudo apt update
sudo apt install gnupg
```

---

## ✅ 1) Generate GPG key pair

```bash
gpg --full-generate-key
gpg (GnuPG) 2.4.9; Copyright (C) 2025 g10 Code GmbH
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

gpg: directory '/home/SaNjA/.gnupg' created
gpg: keybox '/home/SaNjA/.gnupg/pubring.kbx' created
Please select what kind of key you want:
   (1) RSA and RSA
   (2) DSA and Elgamal
   (3) DSA (sign only)
   (4) RSA (sign only)
   (9) ECC (sign and encrypt) *default*
  (10) ECC (sign only)
  (14) Existing key from card
Your selection? 1
RSA keys may be between 1024 and 4096 bits long.
What keysize do you want? (3072) 4096
Requested keysize is 4096 bits
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0) 1y
Key expires at Thu 27 May 2027 03:43:04 AM EDT
Is this correct? (y/N) y

GnuPG needs to construct a user ID to identify your key.

Real name: Sanja Domjanic
Email address: sanja@gmail.com
Comment: 
You selected this USER-ID:
    "Sanja Domjanic <sanja@gmail.com>"

Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? O
We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
gpg: /home/SaNjA/.gnupg/trustdb.gpg: trustdb created
gpg: directory '/home/SaNjA/.gnupg/openpgp-revocs.d' created
gpg: revocation certificate stored as '/home/SaNjA/.gnupg/openpgp-revocs.d/AF3C4A692D94A7C26591AD32F8ACD198BEC2049C.rev'
public and secret key created and signed.

pub   rsa4096 2026-05-27 [SC] [expires: 2027-05-27]
      AF3C4A692D94A7C26591AD32F8ACD198BEC2049C
uid                      Sanja Domjanic <sanja@gmail.com>
sub   rsa4096 2026-05-27 [E] [expires: 2027-05-27]


```

Select:
- **Key type:** RSA and RSA
- **Key size:** 4096
- **Expiration:** 1y
- **Name:** Student Name
- **Email:** student@example.com

Check keys:

```bash
gpg --list-keys
gpg: checking the trustdb
gpg: marginals needed: 3  completes needed: 1  trust model: pgp
gpg: depth: 0  valid:   1  signed:   0  trust: 0-, 0q, 0n, 0m, 0f, 1u
gpg: next trustdb check due at 2027-05-27
/home/SaNjA/.gnupg/pubring.kbx
------------------------------
pub   rsa4096 2026-05-27 [SC] [expires: 2027-05-27]
      AF3C4A692D94A7C26591AD32F8ACD198BEC2049C
uid           [ultimate] Sanja Domjanic <sanja@gmail.com>
sub   rsa4096 2026-05-27 [E] [expires: 2027-05-27]

```

---

## ✅ 2) Export and import public key

### Export public key

```bash
gpg --armor --export student@example.com > student_pubkey.asc
```

### Importing a foreign public key

```bash
gpg --import peer_pubkey.asc
```

Tip: If you don't have a foreign public key, create another one of your own, then repeat the above process with a different identity.

Verification:

```bash
gpg --list-keys
gpg: checking the trustdb
gpg: marginals needed: 3  completes needed: 1  trust model: pgp
gpg: depth: 0  valid:   2  signed:   0  trust: 0-, 0q, 0n, 0m, 0f, 2u
gpg: next trustdb check due at 2027-05-27
/home/SaNjA/.gnupg/pubring.kbx
------------------------------
pub   rsa4096 2026-05-27 [SC] [expires: 2027-05-27]
      AF3C4A692D94A7C26591AD32F8ACD198BEC2049C
uid           [ultimate] Sanja Domjanic <sanja@gmail.com>
sub   rsa4096 2026-05-27 [E] [expires: 2027-05-27]

pub   rsa4096 2026-05-27 [SC] [expires: 2027-05-27]
      D841150EDC4AA840EB99573F4A53E4151D80CF75
uid           [ultimate] Test User <test@example.com>
sub   rsa4096 2026-05-27 [E] [expires: 2027-05-27]
```

---

## ✅ 3) Preparing the message

```bash
echo "To: peer@example.com
From: student@example.com
Date: $(date)
Secret message: Confidential message" > message.txt
```

---

## ✅ 4) Encrypting and signing

```bash
gpg --encrypt --sign --armor --recipient peer@example.com message.txt
```

Result:
```
message.txt.asc

cat message.txt.asc                                                                                                                                                                                                                    
-----BEGIN PGP MESSAGE-----

hQIMA4T3Ua6VB2tTARAAs7/bPuCLnCK6OrxFol9bajXJI2HCBxxgi/i4mymMEl5u
XE3Qrj83HwenV64ULn24MFm8WI+bZ+Tzv8TuvZqHRrVPuR9nuHLLnit2PbsdhFCe
7u9NLudwj4ML2ZN/ZxpG9CZRRwWDwYCJK29e4nby+jdiLhdS+RaxF+bmB0LSJf73
9P0BmrjFfVNf6Wug4fdGrMrP41L+qh5b4LJNvexQkgR6i1wMnaj05vmAmAf76yZL
b8Hsam9MEu8ZXuKLJWSKh+gTMFd/4SzTZ8PMwl0hUwo/qjhq4Z1/XS7s984ZqHk1
h8J5GYpeqUepHe3vCWydSGXaSPaTLfJ+RnAFjwjBiuchHgGvmmeN75X7szkKF36a
Hz/Qi8SXHZDZcO2Qq5GqG42N3N/JDdUttlSdTk5lTOfPd6KwJyn1nruvtVXxwRSR
jelt8exmIP7iwuPBk3JefAXO2DnQAkoQ1XiTBvBrUC4KwECvnr2hipzYqs2FkeDm
bOFmlnNsi8+TX7Njes2Rlp3yfFPXBMWTjoK+iuDVnqxi4hRu6xVljCvqrHvhhGdm
mXc5YscVvjxGZsG/U18kv9a5k/EE7WlAQvK1FrY0gCIerDBmFsH0nWiV4/8ygFal
K0y5dx3GRLuhx2Je5RVgs4GHCJr2Mi9BPpK3gnQj8GZ5JizZl3AV23dEjTTcRO3S
6QE9/mpBXkHzISL6zR1AKxh11Sx1w75U5pVCkPAFvD2IQ6OBJWw5Xtk8Kk0626yn
uye4IUDfrHv6q1UfxT0aHAeR7kJrcfN6X7XfsFh6Px7PZBy5bO7YRZSLhKs6wiRw
1ez7qHxNZAcGoknpPhPy/p65ZE+wMK5k0s/Gr+g9pC2FFWlf1uIDCf2ZyMa4+5vp
fGKJYNN1UKJkCg5+VK9jtO3QWF7bIuhPAEmxaOnhKZmMXGsQLXJCpcdfmH9eK/nj
sqB7CRz4ZDYzj6ge23n2CSMKWPjCaB9q1Y/a1a6S4kF/ZEgQK6VTOEPXk+a2ktY4
oF8Ff8Zv+heijbgtg5aMgbdFe4kq/8R/PjEm4+IDb10NA3jYI4UeoG1pzlBoEdXO
xESrBC0upHpmiLxD6QOUJLNvbz4y1OrHHuSCg+julwMNtdqMT5VJwlOXkNmpDbci
0MeNgn8JFmY4NSBn/T0tE/JMfNu8nFKL0pdBJfhc0BeJ1WDfJEvP5S66bN19OqM2
GRRmDU6IKkjPF1T/+dSxv5Sgwtu1GeHwXO7lC8YzzKc2Ta7J5Zbyrlmam0w2y4AF
xaUEgOrR52V7OBhc+fTPn40wydvr6DtZTOjJrqm5h/Y3WnFsbMCtH24UERUCHQek
2zwuFRwfcY46CjmmZX3HY9erOyEm/FSqUGfexxYQMMNkwEQ/U4mJlUEYpOdZWHJv
6tVTeM4V7AW62FxThCrkvWGRkO7iKsk3Ua3kL5s6AyRhdifHDpdk3Bo+730YqlN/
hhLJ3g24LkEIEMQvR84PzK8DyXPVIHt9D/J1zBjJ3dCUxCKUzrZu155YRmXXcZmg
6CfpZfnS8rX+BYMNBP9GYgNYb2qWeh2nhpJ4vVhG5sEQCVw8chFwYv/HZXREwTKU
laOYsMie3B0z4kF8W9BhcMp7kIhUOUX8Z8vU9JTiafdf5XnpEOe24xFvwqkJIJis
mAiGf6oMXKvEKsAROblx689hgxZNBZSFxgS2RpHz48S8OrV7jKFnl6sFG85QBXmK
fcFqK456bg==
=c6q0
-----END PGP MESSAGE-----

```

---

## ✅ 5) Decrypting and verifying the signature

```bash
gpg --decrypt message.txt.asc > decrypted_message.txt
gpg: encrypted with rsa4096 key, ID 84F751AE95076B53, created 2026-05-27
      "Test User <test@example.com>"
gpg: Signature made Wed 27 May 2026 04:13:03 AM EDT
gpg:                using RSA key AF3C4A692D94A7C26591AD32F8ACD198BEC2049C
gpg: Good signature from "Sanja Domjanic <sanja@gmail.com>" [ultimate]

```

```bash
cat decrypted_message.txt
To: test@example.com
From: sanja@gmail.com
Date: Wed May 27 04:11:22 AM EDT 2026
Secret message: Confidential message

```

Expected output:
```
gpg: Good signature from "Student Name <student@example.com>"
```
```text
The encrypted message was successfully decrypted and the digital signature was verified.
```
---

## 📝 Report preparation
Include in the report:
- commands used,
```bash
gpg --full-generate-key
gpg --list-keys
gpg --armor --export "sanja@gmail.com" > student_pubkey.asc
gpg --armor --export "test@example.com" > peer_pubkey.asc
gpg --import peer_pubkey.asc
echo "To: test@example.com
From: sanja@gmail.com
Date: $(date)
Secret message: Confidential message" > message.txt
gpg --pinentry-mode loopback --encrypt --sign --armor --recipient test@example.com message.txt
gpg --pinentry-mode loopback --decrypt message.txt.asc > decrypted_message.txt
cat decrypted_message.txt
```
  
- screenshot of the terminal,
  <img width="852" height="1025" alt="VirtualBox_kali-linux-2025 4-virtualbox-amd64_26_05_2026_21_27_14" src="https://github.com/user-attachments/assets/92a25532-b34a-4451-b622-99ef79771e86" />

- short answers:
1. Difference between encryption and signing
```text
Encryption protects the confidentiality of data by making the message unreadable to unauthorized users. Only the intended recipient can decrypt and read the message.
Digital signing is used to verify the authenticity and integrity of the message. It confirms that the message was created by the sender and was not modified during transmission.
```
3. Role of public and private key
  ```text
The public key is used to encrypt messages and verify digital signatures. It can be shared publicly with other users.
The private key is used to decrypt messages and create digital signatures. It must be kept secret and protected by the owner.
```
5. What happens when an encrypted file is modified
```text
If an encrypted or digitally signed file is modified, the integrity check will fail during verification. The digital signature will no longer match the original content, indicating that the file has been altered or corrupted.
```
---

## ⭐ Additional tasks

### Revocation certificate

```bash
gpg --gen-revoke student@example.com > revoke.asc
```

### Signing only (no encryption)

```bash
gpg --clearsign message.txt
```

### Verifying the signature

```bash
gpg --verify message.txt.asc
```

---

## 🧠 Summary
- Encryption provides **confidentiality**
- Digital signature provides **authentication and integrity**
- GPG uses **asymmetric cryptography (RSA)**
