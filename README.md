# aidoku-builds

GitHub Actions workflow that builds official [Aidoku](https://github.com/Aidoku/Aidoku)
release tags with a personal `com.zhelearn.Aidoku` bundle identifier, publishes the
unsigned IPA as a GitHub Release, and updates `app-repo.json`.

## Usage

1. Go to **Actions** → **Build Aidoku (Personal) from official Release** → **Run workflow**.
   Tick `force` to rebuild a release that was already built.
2. The workflow checks the latest official release. If it was already built it stops;
   otherwise it builds and publishes a `<official-tag>-personal` release.
3. Add this source in Feather:

```
https://raw.githubusercontent.com/zHElEARN/aidoku-builds/main/app-repo.json
```

The IPA is unsigned on purpose. Sign it with your own certificate/profile in Feather.

## Notes

- **Toolchain**: the job runs on the `xcode-27` image, matching upstream Aidoku's own
  CI. Since v0.9-4 the source uses iOS 27-only APIs (`submitTaskRequest`,
  `@ContentBuilder`), so older images/Xcodes (e.g. `macos-26` + Xcode 26.6) no longer
  compile. The image ships the iOS platform, so no `setup-xcode` / `downloadPlatform`
  step is needed.
- **Version fields** in `app-repo.json` come from the built app's Info.plist
  (`CFBundleShortVersionString` / `CFBundleVersion`), not from the git tag: tags such as
  `v0.9-4` are not valid semver and would make AltStore mis-order updates
  (`0.9-4` sorts *below* `0.9`).
- Entries in `versions` are de-duplicated by `version` + `buildVersion`, so a forced
  rebuild does not append a duplicate row.
