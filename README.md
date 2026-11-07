# Punjab Dairy V9 — Compact header and navigation update

This release fixes the crowded mobile header shown in the screenshot. The header now has a one-line shop name, small subtitle and compact logout action. **Back** appears immediately below the navigation tabs on all non-home screens and edit forms, rather than in the red top bar. The existing app logic, Android app ID (`pk.punjabdairy.manager`), IndexedDB database name, data schema and backup logic are unchanged.

## Upload/build

Unzip this source over your existing project (at the repository root), then run:

```sh
git add .
git commit -m "Punjab Dairy V9 compact mobile navigation"
git pull --rebase origin main
git push origin main
```

Open GitHub Actions and build the APK. Install **over the existing app only** using the same signing key; do not uninstall or clear app data. If Android reports a signature mismatch, cancel the installation and address signing before proceeding.

## Testing

JavaScript was syntax-checked and the source ZIP verified. The Android APK has **not** been compiled or tested on a device in this environment.
