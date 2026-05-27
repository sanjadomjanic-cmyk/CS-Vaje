# Identifying MITM attacks on GPG keys (Web of Trust)

## 🎯 Exercise goal
The purpose of the exercise is to understand that:
- a public key in itself does not imply trust,
- MITM (Man-in-the-Middle) attacks can occur during key exchange,
- fingerprint verification is crucial,
- Web of Trust helps in detecting such attacks.

---

## 🧠 Short introduction
If an attacker manages to inject his public key instead of the real one, he can:
- read all encrypted messages,
- impersonate someone else,
- GPG cannot detect this without trust verification.

---

## 🧪 Scenario
Three people participate in the exercise:
- **Alice** – sender
- **Bob** – recipient
- **Mallory** – attacker (MITM)

Everything is done on **the same device**.

---

## 🔑 1) Key generation

Generate three GPG keys:

```bash
gpg --full-generate-key
```

Data (example):
- Alice: `alice@example.com`
- Bob: `bob@example.com`
- Mallory: `mallory@example.com`

Verify keys:
```bash
gpg --list-keys
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

```

---

## 🧾 2) Print fingerprints (very important)

```bash
gpg --fingerprint alice@example.com
pub   rsa4096 2026-05-27 [SCEAR] [expires: 2027-05-27]
      CEF4 9C5B E707 2944 6212  B22B ABE6 31BE 84E0 9797
uid           [ultimate] Alice <alice@example.com>
sub   rsa4096 2026-05-27 [SEA] [expires: 2027-05-27]

gpg --fingerprint bob@example.com
pub   rsa4096 2026-05-27 [SCEAR] [expires: 2027-05-27]
      EE53 BD16 7DED F63B B423  0336 31A1 9A87 598D 7090
uid           [ultimate] Bob <bob@example.com>
sub   rsa4096 2026-05-27 [SEA] [expires: 2027-05-27]


gpg --fingerprint mallory@example.com
pub   rsa4096 2026-05-27 [SCEAR] [expires: 2027-05-27]
      3A74 394A 2826 A54C 28CE  58E3 F6E2 64FC DFEE 4A01
uid           [ultimate] Mallory <mallory@example.com>
sub   rsa4096 2026-05-27 [SEA] [expires: 2027-05-27]

```

📌 Fingerprint is the only reliable way to verify a key.

---

## 🕵️ 3) MITM attack – key substitution

Mallory exports **her** public key and names it Bob's:

```bash
gpg --armor --export mallory@example.com > bob_pubkey.asc
└─$ gpg --show-keys --fingerprint bob_pubkey.asc                                                                                                                                                                                           
pub   rsa4096 2026-05-27 [SCEAR] [expires: 2027-05-27]
      3A74 394A 2826 A54C 28CE  58E3 F6E2 64FC DFEE 4A01
uid                      Mallory <mallory@example.com>
sub   rsa4096 2026-05-27 [SEA] [expires: 2027-05-27]
```
```text
The file bob_pubkey.asc actually contains Mallory’s public key, demonstrating a key substitution MITM attack where Alice could mistakenly trust Mallory instead of Bob.
```
Alice imports the key:
```bash
gpg --import bob_pubkey.asc
gpg: key F6E264FCDFEE4A01: "Mallory <mallory@example.com>" not changed
gpg: Total number processed: 1
gpg:              unchanged: 1

```

➡️ Alice believes she has Bob's key, but in fact she has Mallory's.

---

## 🔐 4) Alice encrypts the message

```bash
echo "Confidential message for Bob" > secret.txt
```

```bash
gpg --encrypt --recipient bob@example.com secret.txt
```

➡️ The message is encrypted with the wrong key.

---

## 👀 5) Mallory decrypts the message

```bash
gpg --decrypt secret.txt.gpg
gpg: encrypted with rsa4096 key, ID BAFD2955FB077277, created 2026-05-27
      "Bob <bob@example.com>"
Confidential message for Bob
```

✔ MITM attack is successful.

---

## 🚨 6) Attack detection – fingerprint verification

Bob sends Alice **correct fingerprint via another channel** (in person, phone).

Alice checks:
```bash
gpg --fingerprint bob@example.com
```

❌ Fingerprint does not match → MITM attack detected.

---

## 🛡️ 7) Web of Trust – trust setting

Alice sets trust on the verified key:

```bash
gpg --edit-key bob@example.com
```

In the console:
```text
trust
5
quit
```

---

## 🧠 Reflection
Answer:
1. Why doesn't GPG detect MITM attacks automatically?
   ```text
   GPG does not automatically detect MITM attacks because it only encrypts data using the public key provided by the user and cannot verify whether the key truly belongs to the intended person without external trust verification.
   ```
2. What is a fingerprint and why is it important?
    ```text
    A fingerprint is a unique hash that identifies a public key. It is important because users can verify the fingerprint through a trusted channel to confirm that the key truly belongs to the intended person and has not been replaced in a MITM attack.
    ```
3. Why is email not a secure channel for exchanging keys?
    ```text
   Email is not a secure channel for exchanging keys because attackers can intercept or replace public keys during transmission, enabling MITM attacks without the users noticing.
    ```
5. How does the Web of Trust reduce the risk of MITM attacks?
    ```text
   The Web of Trust reduces the risk of MITM attacks by allowing users to verify and sign trusted public keys, helping others confirm that a key genuinely belongs to the claimed person.
   ```
---

## ⭐ Additional challenge

Signing Bob's key with Alice's key:
```bash
gpg --sign-key bob@example.com
```

Explain the difference between:
- trust
- signed key
- ultimate trust

 ```text
Trust means confidence that a user verifies keys correctly, a signed key is a key confirmed by another user’s digital signature, and ultimate trust is the highest trust level assigned to a fully trusted key owner, usually your own key.

 ```
---

## 📌 Summary
- Cryptography works properly as long as we trust the right key.
- Fingerprinting is the foundation of trust.
- Web of Trust helps detect MITM attacks.
