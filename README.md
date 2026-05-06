# Structured Post-Quantum Signature Scheme (Module-SIS)

This repository contains the evaluation suite for a digital signature scheme derived from a parametric KEM paradigm. The security is based on the hardness of the **Module-SIS** problem.

## 📑 Project Overview
The signature scheme uses a Fiat-Shamir transform with a seed-expanded module matrix, a CDT discrete Gaussian sampler, and negacyclic NTT.

**System Compatibility:**
* Target OS: **Windows 11 (64-bit)**
* Platform: x64

### 📖 Theoretical Documentation
For a detailed mathematical explanation, security reductions, and formal proofs of the scheme, please refer to the technical paper included in this repository:
* [**signature.pdf**](./signature.pdf)

### Prerequisites
To run the executable on Windows 11, the following OpenSSL 3.x libraries must be present in the same folder:
* `libcrypto-3-x64.dll`
* `libssl-3-x64.dll`

## 🚀 Getting Started (Windows 11 PowerShell)

### 1. Generate the Master Seed
Before generating keys, you must create a 32-byte random seed. Open PowerShell in the executable's folder and run the following script:

# --- POWERSHELL SCRIPT START ---
$rng = New-Object System.Security.Cryptography.RNGCryptoServiceProvider
$bytes = New-Object byte[] 32
$rng.GetBytes($bytes)
[System.IO.File]::WriteAllBytes((Join-Path $PWD "master_seed.bin"), $bytes)
# --- POWERSHELL SCRIPT END ---

### 2. Key Generation
Use the generated seed to create your public and secret keys:
./signature_proto.exe genkey master_seed.bin pub.bin sk.bin

### 3. Signing and Verification

#### Text Messages
* Sign text:
  ./signature_proto.exe signmsg sk.bin pub.bin "Hello world" signature.sig
* Verify text:
  ./signature_proto.exe verifymsg pub.bin signature.sig "Hello world"

#### Files
* Sign a file:
  ./signature_proto.exe signfile sk.bin pub.bin test.txt signature.sig
* Verify a file:
  ./signature_proto.exe verifyfile pub.bin signature.sig test.txt

## 💻 Technical Parameters (120-bit security)
| Parameter | Value |
|-----------|-------|
| n / q     | 256 / 12289 |
| k / l     | 4 / 4 |
| σ (sigma) | 4.0 |
| PK Size   | ≈1.6 KB |
| Sig Size  | ≈5.2 KB |

## ⚖️ License
Academic Evaluation License. This project is part of a potential patent disclosure. Commercial use, redistribution, or reverse engineering is strictly prohibited. Compatible only with Windows 11 (64-bit) systems.

---
*© 2026 - Daniele Rufo | Structured Lattice Signature Project*
