# 记续 / Oncekeep — Public Beta Downloads

Public engineering-beta downloads for Apple Silicon Macs. The development repository remains private. Bundles contain application runtime code, but no personal Vault, credentials or model weights. **Unsigned and not notarized; real second-Mac acceptance is still pending.**

## One-line installation — v1.8.0-beta.7

Enable **iCloud Drive → Sync this Mac** in macOS System Settings and open iCloud Drive in Finder. Back up important data first. Run in Terminal as your normal user, **without sudo**:

```bash
curl -fsSL https://github.com/hpcll/oncekeep-releases/releases/download/v1.8.0-beta.7/install-oncekeep.sh | bash
```

[Release notes / downloads](https://github.com/hpcll/oncekeep-releases/releases/tag/v1.8.0-beta.7) · [Second-Mac acceptance checklist](first-user-mac-acceptance.md)

**Use this fixed URL. `releases/latest` remains v1.7.1, the older stable channel.** No source checkout or preinstalled Node/Python is required.

## Upgrading an existing installation

Run the same command above. No uninstall or new Vault is needed. Existing memories, identity, location and local model cache stay in place. Conflicting location overrides are refused; migration must be a separate backed-up operation. Refresh any old browser tab after upgrading.

beta.7 brings a unified admin interface and guided assistant selection with optional history import, previews, confirmation and results. It fixes duplicate rows after the first assistant scan, rejects empty installation IDs, avoids default-port fallback during history import, and refreshes the memory list's catalog after new conversations are archived. Already-configured assistants are not preselected for repeat onboarding. Configuration alone is not proof of successful capture, recall or host trust. The visual direction is still provisional.

## New installations default to your iCloud Drive

- Memory Vault: **iCloud Drive / Oncekeep**, physically `~/Library/Mobile Documents/com~apple~CloudDocs/Oncekeep`.
- Program, databases, indexes, spool, logs, models and credentials: local `~/.local/share/localbrain`.
- Memory files, archived attachments and sync events in the Vault are synchronized by macOS to **your own iCloud**. External attachment references are not automatically uploaded.

The installer checks account availability, existing directory permissions and macOS's iCloud directory marker. If these checks fail, installation stops with an actionable message. It never silently falls back to local storage, creates a fake CloudDocs root or changes system settings. It does not search or merge other libraries such as Obsidian/LocalBrain. Existing installations retain their saved location; an upgrade does not move a local Vault to iCloud.

**Saving locally is not proof that uploading completed.** Network, cloud quota and paused sync can delay or prevent upload. Check Finder and the other device for completion. iCloud synchronization is not an independent backup.

If iCloud Drive/Oncekeep already contains the workspace under the same account, that vault ID is reused and this Mac gets its own device ID. Wait for existing files to fully download before installing on another Mac. Never copy another device's config/state/SQLite or entire installation. Automatic writes use device partitions; ordinary manual edits can still conflict.

## Explicit alternative for a new installation

To choose the Documents directory instead of iCloud:

```bash
curl -fsSL https://github.com/hpcll/oncekeep-releases/releases/download/v1.8.0-beta.7/install-oncekeep.sh | ONCEKEEP_STORAGE=local bash
```

This uses `~/Documents/Oncekeep`; whether Documents syncs depends on macOS settings. For another absolute path, use `ONCEKEEP_VAULT` instead; do not set both options.

## After installation

The admin page opens automatically. To reopen it later:

```bash
~/.local/share/localbrain/app/bin/oncekeep ui
```

1. Check the version, Vault location and service status.
2. If needed, explicitly download the local quantized multilingual MiniLM model (129.1 MiB, at least 300 MiB free recommended). Progress, hashes, loading and retries are shown. No embedding API key or per-use fee. Until ready, saving/browsing work, but semantic retrieval and new chunk indexing do not; keyword retrieval may be incomplete.
3. Review detected assistants, choose whether to import history, inspect the configuration/history previews and confirm only the items you want. Cancelling does not connect or import. Restart/trust the connector if required.
4. Use harmless unique markers to test cross-Agent/cross-Mac recall, then reboot and test persistence. See the checklist for backups and isolated restore.

Cloud filtering remains **optional and off by default**. If enabled, queries and limited redacted candidate snippets go to your configured provider and may incur charges. Redaction is not a guarantee of no sensitive content. Model downloads contact Hugging Face/CDN for files, not to send memories. History processing runs locally; writing those memories into iCloud does synchronize the resulting files.

## Verified delivery and remaining limits

Anonymous HTTPS downloads of beta.7's three assets match the tested local files and GitHub SHA-256 digests. Temporary-HOME public-script clean installation, beta.6 → beta.7 upgrade, repeated upgrade and installed-file verification passed. Identity, location, port, a synthetic Vault note, model-cache sentinel and launcher key were preserved. The public ZIP also passed the guarded two-daemon smoke test. Service registration was simulated; these tests did not upgrade the current user's installation.

Real iCloud upload/download, login/reboot and real Agent acceptance are not claimed by isolated tests. Record any macOS security prompt rather than disabling Gatekeeper or deleting security metadata. Do not post private conversations, keys, cookies or bootstrap URLs in public issues.

Every release includes an installer script, versioned ZIP and matching `.sha256`; four offline `.command` entry points remain in the ZIP. beta.6 and earlier assets are unchanged. Signing/notarization remain follow-up distribution improvements.

Copyright © Oncekeep project owner. No source-code license is granted by this binary download repository.
