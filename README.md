<p align="center">
  <img src="https://is1-ssl.mzstatic.com/image/thumb/Purple211/v4/7c/71/56/7c7156b5-9014-da0e-36d5-e09c4716685d/app_icon-0-0-1x_U007ephone-0-1-sRGB-85-220.png/512x512bb.jpg" width="120" alt="Locket App Icon"/>
</p>

<h1 align="center">Locket Gold</h1>

<p align="center">
  <a href="https://github.com/Long18/shadowrocket/stargazers"><img src="https://img.shields.io/github/stars/Long18/shadowrocket?style=flat&color=FFD700&logo=starship&logoColor=white"/></a>
  <a href="https://github.com/Long18/shadowrocket/network"><img src="https://img.shields.io/github/forks/Long18/shadowrocket?style=flat&color=0891b2&logo=github&logoColor=white"/></a>
  <a href="https://github.com/Long18/shadowrocket/blob/main/LICENSE"><img src="https://img.shields.io/github/license/Long18/shadowrocket?style=flat&color=22c55e"/></a>
  <img src="https://img.shields.io/badge/iOS-000000?style=flat&logo=ios&logoColor=white"/>
  <img src="https://img.shields.io/badge/NextDNS-007BFF?style=flat&logo=nextdns&logoColor=white"/>
  <img src="https://img.shields.io/badge/Shadowrocket-5B5EA6?style=flat&logo=apple&logoColor=white"/>
</p>

---

> [!IMPORTANT]
> This repository is for educational, personal DNS configuration, and privacy filtering purposes only.
> Do not use this project to bypass payment, app entitlement, or subscription verification.

---

## 📖 Table of Contents

- [Quick Start — Shadowrocket](#-quick-start--shadowrocket)
- [Quick Start — NextDNS](#-quick-start--nextdns)
- [How It Works](#-how-it-works)
- [Project Structure](#-project-structure)
- [Documentation](#-documentation)
- [Credit](#-credit)

---

## ⚡ Quick Start — Shadowrocket

### Step 1: Import Config

Copy this URL and import into Shadowrocket:

```
https://raw.githubusercontent.com/Long18/shadowrocket/main/Locket.conf
```

Or use the standalone module:

```
https://raw.githubusercontent.com/Long18/shadowrocket/main/modules/Locket.sgmodule
```

### Step 2: Enable MITM

1. Open Shadowrocket → tap the config file ⓘ
2. Go to **HTTPS Decryption**
3. Tap **Generate New CA Certificate**
4. Tap **Install Certificate**
5. On iPhone: **Settings → General → About → Certificate Trust Settings**
6. Enable trust for the Shadowrocket certificate

### Step 3: Verify

1. Make sure the config is selected and Shadowrocket is connected
2. Open the Locket app
3. Check that Gold features are active

> If not working: force-close Locket → reconnect Shadowrocket → reopen Locket.

---

## 🌐 Quick Start — NextDNS

### Step 1: Create NextDNS Account

1. Go to [https://nextdns.io](https://nextdns.io)
2. Sign up for a free account
3. Open Dashboard and copy your **Configuration ID** (e.g., `abc123`)

### Step 2: Customize the Template

Open `PersonalNextDNS.mobileconfig` and replace placeholders:

| Placeholder | Replace with | Example |
|---|---|---|
| `{{NEXTDNS_ID}}` | Your Configuration ID | `abc123` |
| `{{DEVICE_NAME}}` | Device name (shown on NextDNS dashboard) | `iPhone-16-Pro` |
| `{{PROFILE_DISPLAY_NAME}}` | Profile name on iPhone | `My Personal DNS` |
| `{{PROFILE_OWNER}}` | Your name (lowercase) | `william` |
| `{{DNS_PAYLOAD_UUID}}` | Run `uuidgen` in terminal | `A1B2C3D4-...` |
| `{{MAIN_PAYLOAD_UUID}}` | Run `uuidgen` again | `E5F6G7H8-...` |

### Step 3: Install on iPhone

1. AirDrop or email the `.mobileconfig` file to your iPhone
2. Open the file → tap **Allow**
3. Go to **Settings → General → VPN & Device Management**
4. Select the profile → tap **Install**

### Step 4: Verify

1. Open [NextDNS Dashboard](https://my.nextdns.io) → **Logs**
2. Browse Safari on iPhone
3. Confirm DNS queries appear with your device name

> If no logs: check that no other VPN/DNS app is active, and restart iPhone.

---

## 🔄 How It Works

### Shadowrocket Flow

```mermaid
flowchart TD
    A[Import Locket.conf into Shadowrocket] --> B[Enable MITM & install CA Certificate]
    B --> C[Trust certificate in iOS Settings]
    C --> D[Shadowrocket intercepts HTTPS traffic]
    D --> E[deleteHeader.js removes ETag cache header]
    E --> F[Locket.js modifies RevenueCat API response]
    F --> G[App receives spoofed entitlement data]
    G --> H[Locket Gold features unlocked]

    D --> I[hostsVN RULE-SET loaded]
    I --> J[Vietnamese ad domains blocked via REJECT]
```

### NextDNS Flow

```mermaid
flowchart TD
    A[Create NextDNS account] --> B[Copy Configuration ID]
    B --> C[Replace placeholders in mobileconfig template]
    C --> D[Install .mobileconfig on iPhone]
    D --> E[iOS routes all DNS queries via HTTPS]
    E --> F[NextDNS resolves DNS with filtering]
    F --> G[Ads & trackers blocked via Denylist]
    F --> H[DNS logs visible on Dashboard]
    H --> I[Monitor & adjust Allowlist/Denylist]
```

---

## 📁 Project Structure

```
├── Locket.conf                    # Shadowrocket config (Locket + hostsVN)
├── PersonalNextDNS.mobileconfig   # NextDNS DNS-over-HTTPS template
├── docs/
│   ├── nextdns-setup.md           # Detailed tutorial (Vietnamese)
│   └── nextdns-setup_en.md        # Detailed tutorial (English)
├── js/
│   ├── Locket.js                  # RevenueCat response modifier
│   └── deleteHeader.js            # ETag header removal
└── modules/
    └── Locket.sgmodule            # Standalone Shadowrocket module
```

---

## 📚 Documentation

| Language | Link |
|----------|------|
| 🇻🇳 Tiếng Việt | [Hướng dẫn cài NextDNS cá nhân](docs/nextdns-setup.md) |
| 🇬🇧 English | [Personal NextDNS Setup Guide](docs/nextdns-setup_en.md) |

---

## 🙏 Credit

| | |
|---|---|
| **Repository** | [`Long18/shadowrocket`](https://github.com/Long18/shadowrocket) |
| **Maintainer** | William / Long18 |
| **hostsVN** | [`bigdargon/hostsVN`](https://github.com/bigdargon/hostsVN) — MIT License |
| **License** | [MIT](LICENSE) |

If you share, fork, or repost this project, please keep the source credit.

&nbsp;

<p align="center">
	<img src="https://raw.githubusercontent.com/Long18/Long18/refs/heads/dev/assets/footers/cat_on_line.svg?sanitize=true" />
</p>

<p align="center">
	Copyright &copy; 2026-present <a href="https://github.com/long18" target="_blank">William</a>
</p>

<p align="center">
	<a href="https://github.com/Long18/shadowrocket/blob/main/LICENSE"><img src="https://img.shields.io/static/v1.svg?style=for-the-badge&label=License&message=MIT&logoColor=d9e0ee&colorA=363a4f&colorB=b7bdf8"/></a>
</p>
