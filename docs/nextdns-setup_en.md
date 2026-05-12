# Personal NextDNS Setup Guide for iOS/macOS

## ⚠️ Important Disclaimer

> This guide is for personal DNS configuration, privacy filtering, and network troubleshooting only.
> It does **not** unlock, bypass, spoof, or retain any paid subscription feature.
> Do not use this guide to bypass payment, app entitlement, or subscription verification.

## Introduction

NextDNS is a personal DNS service that allows you to:

- Block ads and trackers at the DNS level
- View DNS query logs from your devices
- Protect your browsing privacy
- No VPN or third-party app required

This guide uses a `.mobileconfig` file to configure DNS-over-HTTPS at the system level.

## Prerequisites

- iPhone/iPad running iOS 14+ or Mac running macOS 11+
- NextDNS account (free)
- Text editor (to customize the template)

## Step 1: Create a NextDNS Account

1. Go to [https://nextdns.io](https://nextdns.io)
2. Sign up for a free account
3. Open the Dashboard
4. Find your **Configuration ID** (6 characters, e.g., `abc123`)
5. Copy this ID

## Step 2: Customize the MobileConfig Template

This repository contains a template file:

```
PersonalNextDNS.mobileconfig
```

Open the file and replace the placeholders:

| Placeholder | Replace with | Example |
|---|---|---|
| `{{NEXTDNS_ID}}` | Your Configuration ID | `abc123` |
| `{{DEVICE_NAME}}` | Device name (shown on NextDNS) | `iPhone-15-Pro` |
| `{{PROFILE_DISPLAY_NAME}}` | Profile name shown on iPhone | `My Personal DNS` |
| `{{PROFILE_OWNER}}` | Owner name | `william` |
| `{{DNS_PAYLOAD_UUID}}` | New UUID (run `uuidgen` in terminal) | `A1B2C3D4-...` |
| `{{MAIN_PAYLOAD_UUID}}` | Another new UUID | `E5F6G7H8-...` |

Generate UUIDs using terminal:

```bash
uuidgen
uuidgen
```

After replacement, the DNS URL will look like:

```
https://apple.dns.nextdns.io/abc123/iPhone-15-Pro
```

## Step 3: Install on iPhone

1. Send the customized `.mobileconfig` file to your iPhone (AirDrop, iCloud, email)
2. Open the file on iPhone
3. Go to **Settings > General > VPN & Device Management**
4. Select the downloaded profile
5. Tap **Install**
6. Enter passcode if prompted
7. Confirm installation

> Note: Menu names may vary depending on iOS version and language.

## Step 4: Verify It Works

1. Open [NextDNS Dashboard](https://my.nextdns.io)
2. Go to **Logs** or **Analytics**
3. Open Safari on iPhone, visit any website
4. Check if DNS queries appear on the Dashboard
5. Confirm the device name is displayed correctly

## Step 5: Configure Denylist

Denylist is used to block unwanted domains (ads, trackers, etc.).

Go to NextDNS Dashboard > **Denylist** > add domains to block.

| Domain | Reason | Notes |
|---|---|---|
| `example-tracker.com` | Tracking | Replace with your own domain |
| `example-ads.com` | Ads | Replace with your own domain |

**Do not block:**

- Payment verification domains (Apple, Google)
- App backend domains
- Subscription verification domains
- Apple system domains (captive.apple.com, etc.)

## Troubleshooting

### No DNS logs appear on Dashboard

- Verify the NextDNS ID was replaced correctly
- Check if the profile is installed successfully
- Disable other VPN/DNS apps
- Restart iPhone
- Regenerate the profile if needed

### Some apps stop working

- Check NextDNS Logs for blocked domains
- Move false-positive domains to **Allowlist**
- Reduce the number of blocklists

### Battery concern

Native `.mobileconfig` DNS usually has very low battery impact. If battery drains fast, it may be caused by blocked domains triggering repeated retry requests from apps.

## Privacy & Security

- NextDNS can see queried domains if Logs are enabled
- **Do not** share your NextDNS ID publicly if you want clean logs
- **Do not** share `.mobileconfig` files containing your personal NextDNS ID
- **Do not** install profiles from unknown people
- **Do not** install profiles containing root certificates, VPN, proxy, or MDM payloads unless you fully understand them

## Credit / Source

If you share, fork, or repost this tutorial, please keep the source credit.

Original source:
- Repository: [Long18/shadowrocket](https://github.com/Long18/shadowrocket)
- Maintainer: William / Long18

You may modify this guide for personal use, but please do not remove the source credit when sharing publicly.
