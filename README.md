# Password Vault

A small encrypted password vault that runs entirely in the browser. Open `index.html`, create a master password, and save logins. Nothing is ever sent over the internet.

Built while learning about cyber security, with help from Claude (Anthropic's AI assistant).

> This is a learning project. For real passwords, use a well-tested password manager such as Bitwarden, 1Password or KeePassXC.

## Features

- Master password (at least 12 characters) to create, lock and unlock the vault
- Add, search, show, copy and delete saved logins
- Built-in strong password generator
- Auto-lock after 5 minutes without activity
- Encrypted backup export and import

## How the encryption works

1. **Key derivation (PBKDF2-SHA256, 600,000 rounds):** turns the master password plus a random salt into a 256-bit key. The high round count makes each guess slow for an attacker.
2. **Encryption (AES-256-GCM):** the saved logins are encrypted with that key, using a fresh random IV on every save.
3. **Tamper detection:** GCM's authentication tag makes decryption fail if the password is wrong or the stored data was changed.
4. **Nothing secret is stored:** only the salt, IV and ciphertext are saved (in the browser's localStorage). The master password and key exist only in memory while unlocked.

## Notes

- The vault lives in the browser's storage, so clearing browsing data deletes it. Use **Export backup**.
- Each browser (and opening via `file://` vs. a local server) has its own separate vault.
