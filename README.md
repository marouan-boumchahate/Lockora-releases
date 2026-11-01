# LoQ releases

<p align="center">
  <img src="/icon.svg" alt="LoQ Logo" width="100" height="100" />
</p>

<p align="center">
  <strong>Offline password vault for Android</strong>
</p>

<p align="center">
  <a href="https://github.com/marouan-boumchahate/Lockora-releases/releases/latest">
    <img src="https://img.shields.io/github/v/release/marouan-boumchahate/Lockora-releases?style=flat-square&color=10B981&label=Latest%20Release" alt="Latest Release" />
  </a>
  <a href="https://github.com/marouan-boumchahate/Lockora-releases/releases">
    <img src="https://img.shields.io/github/downloads/marouan-boumchahate/Lockora-releases/total?style=flat-square&color=60A5FA&label=Downloads" alt="Total Downloads" />
  </a>
  <a href="https://lockora.duckdns.org/">
    <img src="https://img.shields.io/badge/Website-lockora.duckdns.org-2563EB?style=flat-square" alt="Website" />
  </a>
</p>

LoQ stores your passwords, PINs, and private notes locally on your device. It has no accounts or cloud servers, and the application requires zero network permissions to store your vault.

This repository is where signed APK packages, SHA-256 checksums, and GPG signatures are published.

> [!NOTE]
> The application source code is currently private. Every build released here is signed and published alongside SHA-256 checksums so you can independently verify binary integrity before installation.

## Downloads

| File | Target | Link |
| :--- | :--- | :--- |
| **Android APK** (v2.2.0) | Android 8.0+ | [Download lockora-v2.2.0.apk](https://github.com/marouan-boumchahate/Lockora-releases/releases/download/v2.2.0/lockora-v2.2.0.apk) |
| **GPG signature** | Detached signature | [Download lockora-v2.2.0.asc](https://github.com/marouan-boumchahate/Lockora-releases/releases/download/v2.2.0/lockora-v2.2.0.asc) |
| **All releases** | Changelog and history | [GitHub releases portal](https://github.com/marouan-boumchahate/Lockora-releases/releases) |
| **Web page** | Documentation and preview | [lockora.duckdns.org](https://lockora.duckdns.org/) |

**Expected SHA-256 checksum:**
```text
c671e307e1bb34ede0ae60a6ba4fb69471c6769605de2646b82ebe27da389343
```

Reference digests:
- MD5: `bc5238dc5bd9bb9f84035c7a4fadd341`
- SHA-1: `c71d0ae0bb74e1be5a8b5f7c65bdd3815e50e644`

## Verifying the download

Checking the hash before opening the package confirms that the file downloaded intact and matches what was built.

### Linux and macOS
```bash
sha256sum lockora-v2.2.0.apk
```

### Windows (PowerShell)
```powershell
Get-FileHash -Algorithm SHA256 .\lockora-v2.2.0.apk
```

### GPG signature check (optional)
```bash
gpg --verify lockora-v2.2.0.asc lockora-v2.2.0.apk
```

- Signer: Marouan Boumchahate (`marouanboumchahate@gmail.com`)
- Key fingerprint: `BA48B90E2A10D8097B6454F21F492807B5BA4741`

## How to install on Android

1. Download `lockora-v2.2.0.apk` to your phone.
2. If Android prompts you that installation is blocked, tap **Settings** and turn on **Allow from this source** for your browser or file manager.
3. Open the downloaded file and tap **Install**. If you already have LoQ installed, Android updates it in place and leaves your local database untouched.
4. Open the app, choose your master password, and write down your **12-word recovery seed** on paper. Because there is no central server, nobody can reset your password if you lose both your master credentials and recovery words.

## Security architecture

LoQ is built with React Native (0.88) and Expo SDK 58. Cryptographic primitives run through native C++ bindings (`react-native-quick-crypto`) to avoid JavaScript bridge latency and prevent secret material from lingering in unmanaged heaps.

- **Password hashing:** PBKDF2-HMAC-SHA256 with 310,000 iterations, a 16-byte random salt, and a 32-byte derived key.
- **Symmetric encryption:** AES-256-GCM authenticated encryption. Every entry gets its own 96-bit random nonce and a 128-bit authentication tag to prevent tampering.
- **Seed recovery:** Standard 12-word BIP-39 mnemonic phrase (128 bits of entropy) created on vault setup. If you ever forget your master password, the seed phrase mathematically reconstructs your vault keys.
- **Biometric unlock:** Optional fingerprint or facial recognition via Android Keystore (`expo-local-authentication` and `expo-secure-store`).
- **Timing protections:** Constant-time XOR comparison (`timingSafeEqual`) on password and hash checks to protect against timing analysis.
- **Auto-lock:** Monotonic timers (`performance.now()`) lock the vault on inactivity or when the app is backgrounded. Using a monotonic clock means changing the phone clock does not bypass the lock timer.
- **Clipboard clearing:** Secrets copied to your clipboard are purged after 60 seconds.
- **Vault auditing:** Local password strength evaluation using `zxcvbn`, duplicate detection, and checks for passwords older than 90 days, all calculated entirely on your device.
- **Backups:** Export encrypted `.loq` archive files or printable landscape backup sheets to store on an offline drive or physical safe.
- **Update checks:** The app queries the GitHub Releases API to notify you when a new release tag is available. The check transfers version numbers only; your passwords and vault entries never touch the network.

## Contact and security reports

For questions, feedback, or responsible vulnerability disclosure:

- Maintainer: Marouan Boumchahate
- Email: [marouanboumchahate@gmail.com](mailto:marouanboumchahate@gmail.com)
- Release repository: [https://github.com/marouan-boumchahate/Lockora-releases](https://github.com/marouan-boumchahate/Lockora-releases)
- Web page: [https://lockora.duckdns.org/](https://lockora.duckdns.org/)

## License

Compiled release packages and release assets are distributed for personal and end-user installation.
