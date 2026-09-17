# 记续 / Oncekeep — Public Beta Downloads

This repository contains public beta binary releases for Oncekeep. The application source repository remains private during the first-user test period.

## Install on Apple Silicon Mac

Open Terminal and run:

```bash
curl -fsSL https://github.com/hpcll/oncekeep-releases/releases/latest/download/install-oncekeep.sh | bash
```

The installer checks the platform, downloads the versioned archive and SHA-256 file over HTTPS, verifies the archive, installs the bundled Node and Python runtimes, and opens the local management page.

Default locations:

- Program: `~/.local/share/localbrain`
- Memory Vault: `~/Documents/Oncekeep`

To select another Vault:

```bash
ONCEKEEP_VAULT="/absolute/path/to/vault" /bin/bash -c "$(curl -fsSL https://github.com/hpcll/oncekeep-releases/releases/latest/download/install-oncekeep.sh)"
```

## Current support boundary

- macOS on Apple Silicon only
- Unsigned and not notarized public beta
- No `sudo` required
- Existing installations use the upgrade and automatic rollback path
- If the Vault is stored in iCloud, only one Mac may write to it at a time during this beta

Each release contains `install-oncekeep.sh`, a versioned zip, and the matching `.sha256` file. Verify the checksum independently when using the offline zip path.

Copyright © Oncekeep project owner. No source-code license is granted by this binary download repository.
