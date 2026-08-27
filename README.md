# Sito Homebrew Tap

Homebrew tap for Sito's macOS apps:

| Cask | App | Description |
|------|-----|-------------|
| [`sito-file-browser`](https://github.com/sito8943/sito-file-browser) | Sito File Browser | File browser that ships an AI-friendly `sfb` command-line tool. |
| [`sito-wireguard-vpn`](https://github.com/sito8943/sito-wireguard-vpn) | Sito WireGuard VPN | Plug-and-play WireGuard client — import a `.conf`, click Connect. |

`brew` adds the tap automatically the first time you install any cask from it. (Equivalent to
`brew tap sito8943/tap && brew install --cask <name>`.)

## Sito File Browser

```bash
brew install --cask sito8943/tap/sito-file-browser
```

Installing does two things:

1. Puts **Sito File Browser.app** in `/Applications`.
2. Symlinks the embedded **`sfb`** CLI onto your `PATH`, so you can use it right away:

   ```bash
   sfb --help
   sfb list --path ~/Documents
   ```

## Sito WireGuard VPN

```bash
brew install --cask --no-quarantine sito8943/tap/sito-wireguard-vpn
```

- Installs **Sito WireGuard VPN.app** in `/Applications` and pulls in
  [`wireguard-tools`](https://formulae.brew.sh/formula/wireguard-tools) automatically (the app
  drives `wg-quick` under the hood).
- `--no-quarantine` skips the Gatekeeper quarantine flag so the unsigned app opens on first
  launch — see below for the manual alternative.

## First launch (unsigned builds)

The apps are currently **not code-signed / notarized**, so macOS Gatekeeper blocks the first
launch. Either install with `--no-quarantine`, or clear the quarantine flag once, right after
installing:

```bash
xattr -dr com.apple.quarantine "/Applications/Sito File Browser.app"
xattr -dr com.apple.quarantine "/Applications/Sito WireGuard VPN.app"
```

Or open the app once via **right-click → Open** in Finder and confirm the dialog. After that it
launches normally.

## Update

```bash
brew update && brew upgrade --cask sito-file-browser
brew update && brew upgrade --cask sito-wireguard-vpn
```

`brew update` refreshes the tap so the newest cask is picked up before upgrading.

New releases are published automatically: each GitHub release rebuilds the Intel and Apple-Silicon
DMGs and pushes the updated cask here.

## Uninstall

```bash
brew uninstall --cask <name>        # remove the app (and the sfb symlink, for the file browser)
brew uninstall --zap --cask <name>  # also remove app settings & caches
```

## Requirements

- **macOS 14 (Sonoma) or later** — a single Apple-Silicon build covers Sonoma and Sequoia.
- **Apple Silicon and Intel** are both supported (each cask picks the right DMG for your Mac).

---

Issues and source: [sito-file-browser](https://github.com/sito8943/sito-file-browser) ·
[sito-wireguard-vpn](https://github.com/sito8943/sito-wireguard-vpn)
