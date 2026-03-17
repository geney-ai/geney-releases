# Installing Geney

## Download

Download the latest `.dmg` from [GitHub Releases](https://github.com/geney-ai/geney-releases/releases/latest).

| Platform | File |
|----------|------|
| macOS (Apple Silicon) | `Geney_*_aarch64.dmg` |
| macOS (Intel) | `Geney_*_x64.dmg` |

Open the `.dmg` and drag Geney to Applications.

## macOS Gatekeeper

The app is not yet Apple-signed, so macOS will block it on first launch with "'Geney' is damaged and can't be opened." To fix this, remove the quarantine attribute after installing:

```bash
xattr -cr /Applications/Geney.app
```

Alternatively, right-click the app and select "Open", or go to System Settings > Privacy & Security and click "Open Anyway".

## Auto Updates

Once installed, Geney checks for updates automatically. When a new version is available, a prompt appears in Settings. Updates are signed and verified before installation.
