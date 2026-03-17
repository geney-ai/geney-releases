# Installing Geney

## Download Pre-Built App

Download the latest `.dmg` from [GitHub Releases](https://github.com/geney-ai/geney/releases/latest).

| Platform | File |
|----------|------|
| macOS (Apple Silicon) | `Geney_*_aarch64.dmg` |
| macOS (Intel) | `Geney_*_x64.dmg` |

Open the `.dmg` and drag Geney to Applications.

### macOS Gatekeeper

The app is not yet Apple-signed, so macOS will block it on first launch with "'Geney' is damaged and can't be opened." To fix this, remove the quarantine attribute after installing:

```bash
xattr -cr /Applications/Geney.app
```

Alternatively, right-click the app and select "Open", or go to System Settings > Privacy & Security and click "Open Anyway".

### Auto Updates

Once installed, Geney checks for updates automatically. When a new version is available, a prompt appears in Settings. Updates are signed and verified before installation.

## Build from Source

### Prerequisites

| Requirement | Version | Install |
|-------------|---------|---------|
| Node.js | 22+ | [nodejs.org](https://nodejs.org/) |
| pnpm | 9+ | `corepack enable pnpm` |
| Rust | stable | [rustup.rs](https://rustup.rs/) |
| uv | latest | [astral.sh/uv](https://astral.sh/uv) |
| Python | 3.12+ | Managed by uv |

### System Dependencies (Tauri)

**macOS:**

```bash
# Xcode command line tools (if not already installed)
xcode-select --install
```

No additional system libraries needed on macOS — Tauri uses the system WebView (WKWebView).

**Ubuntu / Debian:**

```bash
sudo apt install build-essential pkg-config libssl-dev libsqlite3-dev \
  libwebkit2gtk-4.1-dev libappindicator3-dev librsvg2-dev patchelf
```

**Fedora:**

```bash
sudo dnf install gcc pkg-config openssl-devel sqlite-devel \
  webkit2gtk4.1-devel libappindicator-gtk3-devel librsvg2-devel
```

See the full [Tauri prerequisites](https://v2.tauri.app/start/prerequisites/) for other platforms.

### Build Steps

```bash
# Clone the repo
git clone git@github.com:geney-ai/desktop.git
cd geney

# Install JS + Python dependencies
make install

# Build the desktop app (builds sidecar first, then Tauri)
make build-desktop
```

The built app will be at `apps/desktop/src-tauri/target/release/bundle/`.

To install a local build on macOS:

```bash
# Copy to Applications
cp -r apps/desktop/src-tauri/target/release/bundle/macos/Geney.app /Applications/

# Remove quarantine attribute (required for unsigned builds)
xattr -cr /Applications/Geney.app
```

### Development

```bash
# Run in dev mode (hot reload)
make dev

# Run all checks (fmt, lint, types, test, build)
make check
```

## System Requirements

- **macOS:** 10.15 (Catalina) or later
- **Linux:** Ubuntu 20.04+, Debian 11+, Fedora 35+
- **Hardware:** 2 cores / 2 GB RAM minimum, 4+ cores / 4+ GB recommended
