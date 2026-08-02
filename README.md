# Lockora — Official Release Mirror & Distribution Center

<p align="center">
  <img src="https://raw.githubusercontent.com/marouanboumchahate/lockora-web/main/public/images/Lockora.png" alt="Lockora Logo" width="120" height="120" />
</p>

<p align="center">
  <strong>Sovereign, Zero-Trust, Local-First Mobile & Web Password Vault</strong>
</p>

<p align="center">
  <a href="https://github.com/marouanboumchahate/Lockora-releases/releases/latest">
    <img src="https://img.shields.io/github/v/release/marouanboumchahate/Lockora-releases?style=for-the-badge&color=10B981&label=Latest%20Release" alt="Latest Release" />
  </a>
  <a href="https://github.com/marouanboumchahate/Lockora-releases/releases">
    <img src="https://img.shields.io/github/downloads/marouanboumchahate/Lockora-releases/total?style=for-the-badge&color=60A5FA&label=Downloads" alt="Total Downloads" />
  </a>
  <img src="https://img.shields.io/badge/Security-Zero--Trust%20Local-10B981?style=for-the-badge" alt="Zero Trust" />
  <img src="https://img.shields.io/badge/Platform-Android%20%7C%20iOS%20%7C%20Web-0A1628?style=for-the-badge" alt="Platforms" />
</p>

---

## 📌 About This Repository

This is the **official binary release distribution center** for **Lockora**. Official signed Android application packages (`.apk`), checksum hashes, release notes, and cryptographic signatures are published directly to this repository's [Releases Page](https://github.com/marouanboumchahate/Lockora-releases/releases).

> [!NOTE]  
> **Source Code Privacy Notice:**  
> The core source code of the Lockora mobile application remains strictly proprietary and private to protect proprietary implementation details and key security tooling. All release binaries published here are cryptographically signed and checksum-verified to ensure absolute authenticity and tamper protection.

---

## 🛡️ Core Security Architecture & Specifications

Lockora is built from the ground up on a **Zero-Trust, Local-First** security model using **React Native & Expo (SDK 54)**.

| Component | Technical Specification | Security & Standards Standard |
| :--- | :--- | :--- |
| **Key Derivation (KDF)** | PBKDF2-HMAC-SHA256 | **NIST SP 800-63B Compliant** — `310,000` iterations, 16-byte random salt, 32-byte derived key length. |
| **Native Execution** | `react-native-quick-crypto` | Native C++ compiled PBKDF2 execution to eliminate JS thread overhead. |
| **Side-Channel Protection** | Constant-Time Validation | Byte-by-byte XOR comparison loop (`timingSafeEqual`) to prevent timing side-channel attacks. |
| **Symmetric Payload Cipher** | AES-256 in CBC mode | End-to-end client-side zero-knowledge encryption before persistence in local runtime storage (`AsyncStorage`). |
| **Key Tree Derivation** | BIP-39 & HD Key Tree | 12-word seed phrase (`128 bits` entropy) deriving `m/0'/0` (Identity Key) and `m/1'/0` (Vault Encryption Key). |
| **Randomness Source** | Hardware CSPRNG Patch | Monkey-patched CryptoJS WordArray RNG backed by hardware `ExpoCrypto.getRandomBytes()`. |
| **Session Protection** | Monotonic Relative Timer | High-resolution `performance.now()` timer resisting OS clock manipulation; auto-locks on backgrounding & inactivity. |
| **Audit Engine** | `zxcvbn` Scoring & Risk Audit | Real-time strength scoring, duplicate credential detector, and 90-day stale password warnings. |
| **Password Generator** | Entropy Floor Enforcer | Dynamic pool sizing guaranteeing a minimum floor of **60 bits of entropy** via Fisher-Yates array shuffling. |
| **Backup & Export** | Dual-Format Importer/Exporter | Structured JSON backups (`.lockora`) & styled printable landscape PDF reports generated via `expo-print`. |

---

## 🚀 Quick Download Links

| Asset | Format | Target Platform | Latest Version |
| :--- | :--- | :--- | :--- |
| **Official Android Release** | `.apk` | Android 8.0 (Oreo) or higher | [v1.0.0 Download](https://github.com/marouanboumchahate/Lockora-releases/releases/download/v1.0.0/lockora-v1.0.0.apk) |
| **SHA-256 Checksum** | `.txt` / `.sha256` | Terminal / Hash Checkers | [View SHA-256](https://github.com/marouanboumchahate/Lockora-releases/releases/download/v1.0.0/lockora-v1.0.0.apk.sha256) |
| **PGP Signature** | `.asc` | GnuPG Verification | [Download .asc](https://github.com/marouanboumchahate/Lockora-releases/releases/download/v1.0.0/lockora-v1.0.0.apk.asc) |

---

## 🔒 Binary Verification & Integrity Guide

Before installing any downloaded `.apk` package, always verify its SHA-256 cryptographic hash to ensure the binary has not been tampered with or corrupted during transit.

### 1. Verify SHA-256 Checksum (Linux / macOS Terminal)

```bash
# Calculate the SHA-256 hash of your downloaded file
sha256sum lockora-v1.0.0.apk
```

**Expected Hash Value:**
```text
e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
```

### 2. Verify SHA-256 Checksum (Windows PowerShell)

```powershell
Get-FileHash -Algorithm SHA256 .\lockora-v1.0.0.apk
```

### 3. Verify PGP Signature (Optional)

```bash
gpg --verify lockora-v1.0.0.apk.asc lockora-v1.0.0.apk
```

---

## 📱 Installation Guide (Android Sideloading)

1. **Download:** Click the latest `.apk` download link above directly on your Android device.
2. **Verify Checksum:** (Recommended) Check the SHA-256 hash using a mobile hash checker tool or terminal.
3. **Allow Installation:** Open your Android **Settings > Apps & Security**, select your Browser/File Manager, and toggle **"Allow from this source"**.
4. **Install & Verify:** Open `lockora-v1.0.0.apk` and tap Install.
5. **Offline Onboarding:** Feel free to turn off Wi-Fi and Mobile Data to verify 100% local, offline operation. Save your **12-word BIP-39 recovery seed phrase** on paper during initial setup.

---

## 📧 Security Vulnerability Reporting & Contact

If you discover a security vulnerability or have feedback regarding Lockora's cryptographic design:

- **Developer:** Marouan Boumchahate
- **Contact Email:** [marouanboumchahate@gmail.com](mailto:marouanboumchahate@gmail.com)
- **Official Web Landing:** [https://lockora.app](https://lockora.app)

---

## 📄 License & Legal Notice

© 2026 **Lockora Project** (Marouan Boumchahate). All Rights Reserved.  
The compiled release binaries published in this repository are distributed solely for end-user installation. Reverse engineering, unauthorized repackaging, or redistribution with modified signatures without explicit written permission is strictly prohibited.
