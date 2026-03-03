# WidgetGitReleaseChecker

A lightweight Flutter widget that checks a GitHub repository for newer releases and displays an in-app update notification when a newer version is available.

It automatically:

* Fetches releases from GitHub
* Compares semantic versions
* Filters prereleases (optional)
* Displays release information
* Provides a download button (if asset exists)
* Adapts to light & dark themes

---

## ✨ Features

* ✅ Automatic GitHub release check
* ✅ Semantic version comparison (`v1.2.3`)
* ✅ Optional prerelease filtering
* ✅ Download button if asset exists
* ✅ Safe null handling
* ✅ Dark mode compatible (Material 3 friendly)

---

## 📦 Installation

Add dependency in your `pubspec.yaml`:

```yaml
dependencies:
  http: ^1.0.0
  url_launcher: ^6.0.0
```

Then run:

```bash
flutter pub get
```

---

## 🚀 Usage

```dart
WidgetGitReleaseChecker(
  user: "flutter",
  repo: "flutter",
  currentRelease: "v1.0.0",
  filterOutPreRelease: true,
  showLoading: true,
)
```

---

## 🛠 Parameters

| Parameter             | Type     | Required | Description                         |
| --------------------- | -------- | -------- | ----------------------------------- |
| `user`                | `String` | ✅        | GitHub username or organization     |
| `repo`                | `String` | ✅        | Repository name                     |
| `currentRelease`      | `String` | ✅        | Current app version (`v1.0.0`)      |
| `filterOutPreRelease` | `bool`   | ✅        | Skip prereleases                    |
| `showLoading`         | `bool`   | ✅        | Show loading spinner while checking |

---

## 📌 How It Works

1. Calls GitHub API:

   ```
   https://api.github.com/repos/{user}/{repo}/releases
   ```

2. Selects first valid release

3. Compares version numbers numerically

4. If newer → renders update container

5. If not → renders nothing

---

## 🧠 Version Comparison Logic

Versions are parsed numerically:

```
v1.2.10 > v1.2.3
```

The comparison is done segment-by-segment to avoid string comparison issues.

---

## 🎨 Theming

The widget uses:

```dart
Theme.of(context).colorScheme.secondaryContainer
Theme.of(context).colorScheme.secondary
```

This ensures:

* ✅ Dark mode support
* ✅ Material 3 compatibility
* ✅ Custom theme support

---

## 📥 Download Button Behavior

If the release contains at least one asset, the first asset’s `browser_download_url` will be used.

The button opens the link using:

```dart
launchUrl(Uri.parse(url));
```

Make sure your platform supports `url_launcher`.

---

## ⚠️ Important Notes

* GitHub API rate limits unauthenticated requests.
* Version string must follow format like `v1.2.3`.
* Only the first valid release is evaluated.
* Only the first asset is used for download.

---

## 🧩 Example UI Result

If a newer version exists, the widget displays:

```
Release Name
v2.0.0 new
Date Published 2025-01-01
[Download latest]
```

---

## 📜 License

You may use, modify, and distribute this widget freely within your projects.
