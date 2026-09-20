# 记续 / Oncekeep — Public Beta Downloads

This repository contains public engineering-beta downloads for Oncekeep. The development source repository remains private during first-user testing. Distributed application bundles contain the runtime code needed to run locally, but no personal Vault, credentials or model weights.

## Install v1.8.0-beta.4 on an Apple Silicon Mac

Open Terminal as your normal user, **without sudo**, and run:

```bash
curl -fsSL https://github.com/hpcll/oncekeep-releases/releases/download/v1.8.0-beta.4/install-oncekeep.sh | bash
```

**Use the fixed URL above. `releases/latest` still points to the older stable channel, not this beta.** No source checkout or preinstalled Node/Python is required.

[Release notes and downloads](https://github.com/hpcll/oncekeep-releases/releases/tag/v1.8.0-beta.4) · [Second-Mac acceptance checklist](first-user-mac-acceptance.md)

The script checks the platform, downloads the versioned archive and checksum over HTTPS, verifies SHA-256, installs bundled Node/Python plus a user-level background service, and opens the local admin page. Existing installations take the upgrade/rollback path; back up first.

- Program: `~/.local/share/localbrain`
- Default memory Vault: `~/Documents/Oncekeep`
- Reopen the admin page after installation:

```bash
~/.local/share/localbrain/app/bin/oncekeep ui
```

### Choose a shared Vault before installing

For the first run, choose either a new local Vault (default) or your already-synced iCloud Vault. The default local Vault does **not** automatically connect to the other Mac's library.

If your existing iCloud Vault is at the example path below, wait until its files are fully downloaded on the second Mac, then run:

```bash
ONCEKEEP_VAULT="$HOME/Library/Mobile Documents/com~apple~CloudDocs/Obsidian/LocalBrain" /bin/bash -c "$(curl -fsSL https://github.com/hpcll/oncekeep-releases/releases/download/v1.8.0-beta.4/install-oncekeep.sh)"
```

Replace the Vault path if yours differs. Install each Mac separately: the shared Vault has one vault ID and each machine must have a different full device ID. **Never copy config/state, SQLite, spool or the entire installation from another Mac.** Automatic writes are partitioned by device; iCloud timing, real cross-device recall and conflicts still need two-Mac acceptance. Concurrent manual edits to the same ordinary note can still conflict.

## First-run flow

1. Confirm the version, Vault path and service status in the opened local admin page.
2. Explicitly choose whether to download the local quantized multilingual MiniLM model: **135,392,488 bytes / 129.1 MiB**, with at least 300 MiB free for installation. The page shows progress, verification, loading and retry. No embedding API key or per-use model fee is required.
3. Until the model is ready, saving/browsing remain available; semantic retrieval and new chunk indexing are unavailable, and keyword retrieval may be incomplete.
4. Preview discovered Agents, configuration changes and history-import counts. Confirm only the Agents/history you want; restart or trust the connector in the Agent if prompted.
5. Write a harmless unique marker in one Agent and ask another to find it. Follow the checklist for reboot, backups, isolated restore and two-Mac sync.

Cloud filtering is **optional and disabled by default**. If enabled, it sends the query and limited redacted candidate snippets to your configured provider, which may charge. Redaction does not guarantee the absence of sensitive information. Model downloads contact Hugging Face/CDN for model files, not to send memories. No developer credentials are included.

## Support boundary

- Apple Silicon macOS only; **unsigned and not notarized**.
- Public engineering beta, not a production-ready claim. Real second-Mac, Agent, iCloud and login/reboot acceptance remain pending.
- One-line terminal installation is the primary flow. Signing/notarization are follow-up distribution improvements, not a reason to disable macOS protections.
- If macOS blocks an operation, record the exact prompt. Do not disable Gatekeeper or delete security metadata as a default workaround.
- Do not post private conversations, API keys, cookies, launcher keys or bootstrap URLs in public issues.

Every release includes `install-oncekeep.sh`, the versioned zip and its `.sha256`. The zip also has four offline `.command` entry points; verify the checksum before using them.

Copyright © Oncekeep project owner. No source-code license is granted by this binary download repository.
