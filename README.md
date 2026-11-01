# Lockora — Official Release Mirror & Distribution Center

<p align="center">
  <img src="/icon.svg" alt="LoQ Logo" width="120" height="120" />
</p>

<p align="center">
  <strong>Sovereign, Zero-Trust, Local-First Mobile & Web Password Vault</strong>
</p>

<p align="center">
  <a href="https://github.com/marouan-boumchahate/Lockora-releases/releases/latest">
    <img src="https://img.shields.io/github/v/release/marouan-boumchahate/Lockora-releases?style=for-the-badge&color=10B981&label=Latest%20Release" alt="Latest Release" />
  </a>
  <a href="https://github.com/marouan-boumchahate/Lockora-releases/releases">
    <img src="https://img.shields.io/github/downloads/marouan-boumchahate/Lockora-releases/total?style=for-the-badge&color=60A5FA&label=Downloads" alt="Total Downloads" />
  </a>
  <a href="https://lockora.duckdns.org/">
    <img src="https://img.shields.io/badge/Web%20Deployment-lockora.duckdns.org-2563EB?style=for-the-badge" alt="Web Deployment" />
  </a>
  <img src="https://img.shields.io/badge/Security-Zero--Trust%20Local-10B981?style=for-the-badge" alt="Zero Trust" />
  <img src="https://img.shields.io/badge/Platform-Android%20%7C%20iOS%20%7C%20Web-0A1628?style=for-the-badge" alt="Platforms" />
</p>

---

## About This Repository

This repository serves as the official distribution center and binary release mirror for **Lockora**. Cryptographically signed Android application packages (`.apk`), cryptographic checksums, detached PGP signatures, and release notes are published directly to this repository's [Releases Portal](https://github.com/marouan-boumchahate/Lockora-releases/releases).

> [!NOTE]  
> **Source Code Privacy Notice:**  
> The core source code of the Lockora mobile application remains strictly proprietary to safeguard cryptographic implementation nuances and internal security tooling. All binaries distributed through this channel are deterministically signed, checksum-verified, and authenticated to guarantee software supply chain integrity.

---

## Core Security Architecture & Specifications

Lockora is architected from the ground up on a **Zero-Trust, Local-First** security model implemented via **React Native (0.88) & Expo SDK 58**.

| Component | Technical Specification | Standard & Cryptographic Guarantee |
| :--- | :--- | :--- |
| **Key Derivation Function (KDF)** | PBKDF2-HMAC-SHA256 | **NIST SP 800-63B Compliant** — 310,000 iterations, 16-byte cryptographically secure salt, 32-byte derived key. |
| **Native Cryptographic Acceleration** | `react-native-quick-crypto` | Native C++ execution bindings for PBKDF2 and AES operations, eliminating JavaScript bridge latency and memory leakage risks. |
| **Side-Channel Attack Mitigation** | Constant-Time Evaluation | Byte-by-byte XOR comparison (`timingSafeEqual`) across all passphrase validations and hash verifications to prevent timing analysis. |
| **Authenticated Payload Cipher** | AES-256-GCM (AEAD) | Native authenticated encryption with 96-bit CSPRNG nonces and 128-bit authentication tags, preventing ciphertext bit-flipping attacks. |
| **Deterministic Key Hierarchy** | BIP-39 & HD Key Derivation | 12-word mnemonic seed (128 bits of initial entropy) deriving `m/0'/0` (Identity Key) and `m/1'/0` (Vault Encryption Key). |
| **Cryptographic Entropy Source** | Hardware CSPRNG | Entropy generated directly from platform hardware via `ExpoCrypto.getRandomBytes()`. |
| **Hardware Keystore & Biometrics** | Hardware Secure Enclave | Biometric authentication (Fingerprint, Face ID, Touch ID) via `expo-local-authentication` and key encapsulation in `expo-secure-store`. |
| **Session Protection** | Monotonic Relative Clock | High-precision `performance.now()` monotonic timers immune to OS system clock manipulation; automatic vault locking on inactivity or background state. |
| **Memory Buffer Sanitation** | Volatile Clipboard Scrubbing | In-memory countdown timer automatically purges copied credentials and secrets from the system clipboard after 60 seconds. |
| **Smart Security & PIN Auditor** | Real-Time Vulnerability Analysis | Dual audit engines evaluating password entropy (`zxcvbn`), duplicate passwords, 90-day stale credentials, and numeric PIN pattern exploits. |
| **Cryptographic Generator** | Entropy Floor Enforcement | Dynamic character pool selection enforcing a strict minimum floor of 60 bits of entropy via Fisher-Yates array shuffling. |
| **In-App Update Engine** | Authenticated GitHub API Checks | Direct release tag checking against the official release repository; vault contents and sensitive data remain strictly offline. |
| **Data Portability** | Dual-Format Importer / Exporter | Client-side encrypted JSON archives (`.lockora`) and structured printable cryptographic backup reports. |

---

## Release Downloads & Direct Links

The current release version is dynamically tracked via the repository release pipeline. Production binaries, checksum manifests, and detached signatures are available below:

| Distribution Asset | Format | Target Environment | Latest Version |
| :--- | :--- | :--- | :--- |
| **Official Android Release** | `.apk` | Android 8.0 (API 26) or higher | [Download v2.2.0 APK](https://github.com/marouan-boumchahate/Lockora-releases/releases/download/v2.2.0/lockora-v2.2.0.apk) · [Latest Release Redirect](https://github.com/marouan-boumchahate/Lockora-releases/releases/latest) |
| **SHA-256 Checksum** | `.txt` / `.sha256` | Hash Checkers / CLI | `c671e307e1bb34ede0ae60a6ba4fb69471c6769605de2646b82ebe27da389343` |
| **PGP Signature** | `.asc` | GnuPG Verification | [Download v2.2.0 Signature](https://github.com/marouan-boumchahate/Lockora-releases/releases/download/v2.2.0/lockora-v2.2.0.asc) |
| **Official Web Application** | HTTPS | Modern Web Browsers | [lockora.duckdns.org](https://lockora.duckdns.org/) |

> [!TIP]
> Always verify that your downloaded package hash matches the official cryptographic digest published in the release manifest prior to execution.

---

## Binary Verification & Cryptographic Integrity

To verify that the downloaded `.apk` package has not been tampered with or corrupted during transit, compute and compare its SHA-256 cryptographic digest before installation.

### 1. Verify SHA-256 Checksum (Linux / macOS Terminal)

```bash
sha256sum lockora-v2.2.0.apk
```

**Expected SHA-256 Hash:**
```text
c671e307e1bb34ede0ae60a6ba4fb69471c6769605de2646b82ebe27da389343
```

### 2. Verify SHA-256 Checksum (Windows PowerShell)

```powershell
Get-FileHash -Algorithm SHA256 .\lockora-v2.2.0.apk
```

### 3. Auxiliary Hashes for Reference

| Algorithm | Digest |
| :--- | :--- |
| **MD5** | `bc5238dc5bd9bb9f84035c7a4fadd341` |
| **SHA-1** | `c71d0ae0bb74e1be5a8b5f7c65bdd3815e50e644` |

### 4. Verify Detached PGP Signature (Optional)

```bash
gpg --verify lockora-v2.2.0.apk.asc lockora-v2.2.0.apk
```

- **Signer Identity:** Marouan Boumchahate (`marouanboumchahate@gmail.com`)
- **Key Fingerprint / Key ID:** `BA48B90E2A10D8097B6454F21F492807B5BA4741`

---

## Installation & Sideloading Guide (Android)

1. **Obtain Package:** Download `lockora-v2.2.0.apk` directly to your Android device from the release download link or the [Releases Portal](https://github.com/marouan-boumchahate/Lockora-releases/releases/latest).
2. **Verify Digest:** Confirm that the package SHA-256 matches the official digest above using a terminal or mobile verification utility.
3. **Authorize Package Installation:** Navigate to **Settings > Security > Install Unknown Apps** (or **Settings > Apps & Security** depending on your Android vendor), select your browser or file manager, and enable **"Allow from this source"**.
4. **Deploy Application:** Open `lockora-v2.2.0.apk` and confirm the installation. If updating from an earlier v2 release, Android performs an in-place upgrade while preserving your encrypted vault database.
5. **Offline Setup & Seed Custody:** You may disable Wi-Fi and mobile data during initial onboarding to verify zero network dependency. Securely write down your **12-word BIP-39 recovery mnemonic** on physical media during vault setup.

---

## Vulnerability Reporting & Contact

Security inquiries, cryptographic peer reviews, and responsible vulnerability disclosure should be directed to the lead maintainer:

- **Maintainer:** Marouan Boumchahate
- **Security Contact:** [marouanboumchahate@gmail.com](mailto:marouanboumchahate@gmail.com)
- **Official Web Deployment:** [https://lockora.duckdns.org/](https://lockora.duckdns.org/)
- **Release Portal:** [https://github.com/marouan-boumchahate/Lockora-releases](https://github.com/marouan-boumchahate/Lockora-releases)

---

## License & Legal Terms

© 2026 **Lockora Project** (Marouan Boumchahate). All Rights Reserved.  
Compiled release binaries and accompanying release distributions are provided strictly for end-user installation. Unauthorized decompilation, binary repackaging, key injection, or distribution with altered cryptographic signatures without explicit written authorization is prohibited.
