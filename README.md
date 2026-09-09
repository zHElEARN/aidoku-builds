# aidoku-builds

GitHub Actions workflow that builds official [Aidoku](https://github.com/Aidoku/Aidoku)
release tags with a personal `com.zhelearn.Aidoku` bundle identifier, publishes the
unsigned IPA as a GitHub Release, and updates `app-repo.json`.

## Usage

1. Go to **Actions** → **Build Aidoku (Personal) from official Release** → **Run workflow**.
2. The workflow checks the latest official release. If it was already built, it stops;
   otherwise it builds and publishes a `<official-tag>-personal` release.
3. Add this source in Feather:

```
https://raw.githubusercontent.com/zHElEARN/aidoku-builds/main/app-repo.json
```

The IPA is unsigned on purpose. Sign it with your own certificate/profile in Feather.
