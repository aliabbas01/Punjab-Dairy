# Punjab Dairy V6 — offline-first Android app

This package updates V5 in place and preserves the existing `pk.punjabdairy.manager` Android application ID, the `punjab-dairy-data` IndexedDB database and its `state/all` record. No database reset/migration is performed by the V6 source.

## Changes

- Home: monthly daily *gross trading profit* line chart (shop sales + deliveries − purchases). Tap a daily point to see that day's PKR value. Month picker; chart automatically moves to the new month when the calendar month changes, without deleting prior transactions.
- Home: monthly gross and estimated net after recorded expenses and allocated active staff salaries. A recorded salary expense isn't charged a second time. This estimate doesn't account for changes in inventory value; rent/other expenses must be recorded in Expenses to be deducted.
- Entries: Home Delivery, Supplier Purchase and Shop Sale have 3 tabs. Only one history grid is shown at a time; each tab has its entry action and separate pagination, using today's date initially.
- Compact edit/delete icons displayed side by side, a Back control on interior screens/forms.
- Bills: an invoice-only additional outstanding field (avoids modifying ledger), redesigned bilingual green invoice, Easypaisa and HBL payment information (as supplied on the user's invoice), PNG share/download, plus an image-backed A4 PDF share/download.
- Supplier bills: purchase totals, payments made, closing balance, payment details and a status marker for recorded paid bills; generate, save and send PNG to WhatsApp using the Android share sheet.

## Install/build on GitHub

1. Extract all contents at the root of your existing `Punjab-Dairy` repository (not inside a second nested folder).
2. From the project directory run:

```sh
git add .
git commit -m "Punjab Dairy V6 monthly profit, tabs and invoice exports"
git pull --rebase origin main
git push origin main
```

3. Visit GitHub → Actions → Build Android APK → latest run → Artifacts.
4. Build output is a **debug APK**; it is NOT a Play Store-ready release.

### Critical: protect live data

**Never uninstall the existing app, clear app data, or use an APK with a different signing certificate to attempt an upgrade.** The debug APK generated on a fresh GitHub runner may be signed with a new debug certificate and **will not update** an already installed app. Keep the previous installed app and secure a known signing key before upgrading. Back up your customer and supplier records and verify the backup on a separate test installation before any destructive operation. If installation says uninstall first, **cancel**.

The backup import continues to replace the existing local data in one snapshot; it does not append duplicate records. Backup secrets/financial records should be stored securely.

## Testing notes

- JavaScript syntax checked with Node 22.
- Daily/monthly profit function passed a synthetic ledger test.
- Generated PDF embedding a JPEG was structurally validated with PyMuPDF.
- Device-level tests for Android filesystem share, PNG/PDF rendering, Urdu fonts and in-place APK installation still required. The browser test environment restricted local navigation, so interactive UI testing could not be completed.

## Future online app

Cloud synchronization would need new authenticated user identities, server database and authorization rules so each customer can see only their records, a safe migration of existing IndexedDB data, conflict handling, secure backups, and signed Play Store builds. This offline package does **not** sync between devices or provide true server-side pagination.
