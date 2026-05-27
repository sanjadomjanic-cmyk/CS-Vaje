# Secrets Management using GPG

## 🎯 Exercise Objective
The exercise objective is to understand:
- what are secrets in information systems,
- why secrets do not belong in source code or repositories,
- how can we protect sensitive data using GPG,
- the basic concept of **Secrets Management** without specialized tools.

---

## 🧠 Brief Introduction
Secrets (passwords, API keys, tokens, certificates) are often:
- stored in configuration files,
- part of CI/CD environments,
- a target for attackers when hacking or leaking code.

Error:
```text
API_KEY=abc123
```
in Git repository ❌

---

## 🧪 Scenario
A company is developing an application that uses an external API.
The API key must be:
- stored locally,
- protected from unauthorized access,
- accessible only to an authorized user.

---

## 🧰 Requirements
- Linux / Ubuntu
- `gnupg` installed

Installation:
```bash
sudo apt update
sudo apt install gnupg
```

---

## 🔑 1) Prepare secrets

Create a file with secrets:

```bash
echo "API_KEY=super-secret-key-123
DB_PASSWORD=VeryStrongPassword" > secrets.env
```

⚠️ This file is in **unencrypted** form and is not secure.

---

## 🔐 2) Symmetric encryption of secrets (password)

Encrypt the file with the password:

```bash
gpg -c secrets.env
```

Result:
```
secrets.env.gpg
```

Remove the original:
```bash
rm secrets.env
```

---

## 🔓 3) Decrypt the secrets

When an application or administrator needs the secrets:

```bash
gpg secrets.env.gpg
gpg: AES256.CFB encrypted data
gpg: encrypted with 1 passphrase

```
The `secrets.env` file is recreated.

Or we can just print it to the screen:

```bash
gpg -d secrets.env.gpg
gpg: AES256.CFB encrypted data
gpg: encrypted with 1 passphrase
API_KEY=super-secret-key-123
DB_PASSWORD=VeryStrongPassword
```

---

## 🔐 4) Asymmetric encryption (recommended)

Instead of a password, we use the public key.

```bash
gpg --encrypt --recipient student@example.com secrets.env
```

Result:
```
secrets.env.gpg
gpg: encrypted with rsa4096 key, ID 837FDD78EB9D8322, created 2026-05-27
      "Alice <alice@example.com>"
API_KEY=super-secret-key-123
DB_PASSWORD=VeryStrongPassword

```

Advantage:
- no shared password,
- only the owner of the private key can decrypt.

---

## 🔁 5) Using secrets in an application (simulation)

Load variables into the environment:

```bash
source secrets.env
echo $API_KEY
super-secret-key-123

```

After use:
```bash
unset API_KEY
unset DB_PASSWORD
```

---

## 🧪 6) Simulating a repository leak

Assume that the repository only contains:

```text
secrets.env.gpg
```

Attacker without a key:
```bash
gpg secrets.env.gpg
```

➡️ Access is not possible.

---

## 🧠 Reflection (required)
Answer:
1. Why don't secrets belong in the source code?
```text
Secrets do not belong in source code because they can be exposed through repositories, backups, or shared projects, allowing unauthorized users to access sensitive credentials and systems.
  ```
2. What is the difference between symmetric and asymmetric secret encryption?
   ```text
   Symmetric encryption uses the same password for encryption and decryption, while asymmetric encryption uses a public key for encryption and a private key for decryption.
   ```
   
3. What happens if we lose the private key?
   ```text
   If the private key is lost, the encrypted data can no longer be decrypted, which means access to the protected secrets is permanently lost.
    ```
6. How would you handle this in a larger enterprise?
```text
In a larger enterprise, secrets would be managed using centralized secret management systems, secure backups, access control policies, key rotation, and hardware security modules to protect encryption keys and ensure recovery.
```
---

## ⭐ Additional challenge

### Multiple users
Encrypt secrets for multiple recipients:

```bash
gpg --encrypt --recipient alice@example.com --recipient bob@example.com secrets.env
```
```text
Encrypting for multiple recipients allows each authorized user to decrypt the secrets with their own private key, without sharing one common password.
```
### Automatic use (script)
```bash
gpg --decrypt secrets.env.gpg | source /dev/stdin
gpg: encrypted with rsa4096 key, ID BAFD2955FB077277, created 2026-05-27
      "Bob <bob@example.com>"
gpg: encrypted with rsa4096 key, ID 837FDD78EB9D8322, created 2026-05-27
      "Alice <alice@example.com>"
```
```text
The decrypted secrets can be directly loaded into environment variables through a script, reducing the exposure of plaintext secrets on the filesystem.
```
---

## 📌 Summary
- Secrets management is a key part of cybersecurity.
- GPG provides basic but effective secret protection.
- In practice, tools such as Vault, SOPS, AWS Secrets Manager are used.
