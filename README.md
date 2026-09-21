# TrueMinutes releases

Public Sparkle update feed and DMG distribution for [TrueMinutes](https://github.com/AbhiRishi96/TrueMinutes).

| File | Purpose |
| --- | --- |
| `appcast.xml` | Sparkle 2 feed (`SUFeedURL` in the app) |
| `CHANGELOG.md` | Human-readable release notes (embedded in the appcast as HTML) |

## Feed URL

https://raw.githubusercontent.com/AbhiRishi96/TrueMinutes-releases/main/appcast.xml

## Publishing

From the TrueMinutes source repo:

```bash
export SPARKLE_PRIVATE_KEY_FILE=/path/to/ed25519_private_sparkle.txt
./scripts/publish-sparkle-update.sh --dmg build/TrueMinutes-X.Y.Z.dmg --version X.Y.Z --build BUILD
```

Do not commit private signing keys here.
