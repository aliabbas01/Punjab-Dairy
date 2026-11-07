# Punjab Dairy v4 — Android offline source

This package updates the previous Punjab Dairy Capacitor app. **Do not uninstall your existing app**: IndexedDB data is stored under the same Android application ID (`pk.punjabdairy.manager`) and database (`punjab-dairy-data`), with the same state schema (`version: 1`). Existing transactions, customers, suppliers, logins and payments remain in place when Android accepts a signed in-place update.

## v4 updates

- Dashboard: supplier dues and **View all suppliers**, customer balances and **View all customers**, plus a sales-vs-purchases chart by selected reporting period.
- Entries: three separate one-tap cards for home delivery, supplier purchase and shop sale; default entries list filtered to today; no time field. Shop sales take **amount in PKR only**.
- Delivery forms prefill the selected customer's cow milk, buffalo milk and yogurt amounts; if already entered on that date, show existing amounts. Saving the same party/type/date updates that entry instead of creating another one.
- Active / inactive customers and suppliers, with inactive accounts excluded from **new entry dropdowns and bulk entry** but retained in all history, bills and balances.
- Compact edit and delete icons with accessible tooltips; pagination (12 rows/page) on customers, suppliers, staff, expenses, entries, payments, remaining stock, customer month details, supplier overview and feedback. This is **local in-memory page rendering**, not server-side pagination; a real backend is required for server-side queries.
- Customer and supplier Urdu bills with logo, date range, quantities, historical transaction rates, opening balance, payments and closing balance. Open the Bills tab, select an account, choose period and Generate; or use the bill icon next to a customer/supplier. Export/share the HTML invoice or print to PDF where supported. Bills use the existing data; no duplicate invoice records are created. Note: HTML sharing is more reliable in Android than WebView printing, but exact native PDF creation is not included.
- Backup import **replaces the whole local state** in one IndexedDB write, rather than appending duplicates, and signs out after restore. Existing JSON backup exports use the same schema. CSV export remains transactional only.

## APK build

1. Extract this ZIP over the **root of your existing Git repository**, keeping `.github/workflows/build-apk.yml` and directories intact.
2. In Git Bash:

   ```bash
   git add .
   git commit -m "Punjab Dairy v4 entries, pagination, invoices, balances"
   git pull --rebase origin main
   git push origin main
   ```

   If there are conflicts, stop and resolve them before continuing. If `android/` has been committed previously, ensure it uses the same `appId` and native settings.
3. GitHub Actions → Build Android APK → latest run → Artifacts → Punjab-Dairy-Android-APK.

## IMPORTANT: preserve your existing phone data

An Android update requires **the same application ID and signing certificate** as the installed app. The package maintains the application ID, but GitHub Actions can generate a new debug keystore on each clean runner. A newly signed debug APK may **refuse to update** the currently installed app. DO NOT uninstall it or clear its storage to work around the error. Keep your old APK/keystore and use a persistent signing key for future builds. Restore from a checked JSON backup *only* after a valid install and if necessary. Backup JSON contains private business details and login hashes: store it securely.

**Testing:** Source code has been syntax checked. An Android emulator/device build and real on-phone invoices/import/export have **not** been verified in this environment. Test using a spare device or separate test installation and sample data. This is an offline-first app; it does not sync to other phones.

## Features intentionally not described as implemented

- Server-side pagination / remote database: not possible in the current offline-only architecture, though UI lists are paginated for lower rendering cost.
- Native one-click PDF export: invoice can be shared as HTML and printed/saved as PDF where Android supports printing. A dedicated native PDF engine is a later task.
- True server-side account access: customer credentials and profile limits apply on-device, not across devices.


## V5 targeted fixes
- Entries screen has **three independent tables** (home delivery, supplier purchases, shop sales) with independent pagination; shared date filter defaults to today.
- Bills: fixed the missing `id` attributes on account and date selectors that caused the false “Select an account and dates” validation error; button is now “Generate Bill”.
- Payments: separate **Customer payments received** and **Supplier payments paid** tabs with independent paginated records.
- No database schema, database name, application ID, or import/export format changed. In-place installation still requires matching Android signing key. Make a verified backup before upgrading.

- Browser PWA service-worker cache bumped to v5 so existing browser installations receive new app assets. The Android build does not register this service worker.
