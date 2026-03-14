# Fork release guide

## Versioning

Format: `{upstream-version}-tb{n}`

- `0.62.2-tb1` = first TextBox release based on upstream 0.62.2
- `0.62.2-tb2` = second release on the same upstream base (bug fixes, TextBox improvements)
- `0.63.0-tb1` = first release after merging upstream 0.63.0

The `-tb` suffix distinguishes fork releases from upstream. The number after `tb` increments for each release on the same upstream base.

## Prerequisites

- `create-dmg` installed via Homebrew: `brew install create-dmg`
- `gh` CLI authenticated with access to `alumican/cmux-tb`

## Steps

### 1. Merge upstream (if applicable)

See [upstream-sync.md](upstream-sync.md) for the full merge procedure.

### 2. Set version

The `scripts/bump-version.sh` only supports `x.y.z` format, so set the version manually:

```bash
# In GhosttyTabs.xcodeproj/project.pbxproj, update both occurrences:
MARKETING_VERSION = 0.62.2-tb1;

# Bump CURRENT_PROJECT_VERSION (must be monotonically increasing):
CURRENT_PROJECT_VERSION = 78;
```

### 3. Build

```bash
xcodebuild -project GhosttyTabs.xcodeproj -scheme cmux -configuration Release -destination 'platform=macOS' build
```

Verify the app launches and TextBox works correctly.

### 4. Create DMG

```bash
BG="$(npm root -g)/create-dmg/assets/dmg-background@2x.png"

create-dmg \
  --volname "cmux-tb" \
  --background "$BG" \
  --window-size 660 400 \
  --icon-size 128 \
  --icon "cmux.app" 180 180 \
  --app-drop-link 480 180 \
  /tmp/cmux-tb-macos.dmg \
  "$(xcodebuild -project GhosttyTabs.xcodeproj -scheme cmux -configuration Release -showBuildSettings 2>/dev/null | grep ' BUILD_DIR' | awk '{print $3}')/Release/cmux.app"
```

Copy to the release directory:

```bash
cp /tmp/cmux-tb-macos.dmg /path/to/cmux-fork/release/
```

### 5. Commit, tag, and push

```bash
git add GhosttyTabs.xcodeproj/project.pbxproj
git commit -m "Prepare v0.62.2-tb1 release"
git tag v0.62.2-tb1
git push origin main
git push origin v0.62.2-tb1
```

### 6. Create GitHub release

```bash
gh release create v0.62.2-tb1 /tmp/cmux-tb-macos.dmg \
  --repo alumican/cmux-tb \
  --title "v0.62.2-tb1" \
  --notes "Release notes here"
```

The DMG download link in README points to:
`https://github.com/alumican/cmux-tb/releases/latest/download/cmux-tb-macos.dmg`

## Notes

- The DMG asset must be named `cmux-tb-macos.dmg` to match the README download link.
- Build number (`CURRENT_PROJECT_VERSION`) must always increase — never reuse or go backwards.
- The background image for the DMG comes from the npm `create-dmg` package assets.
