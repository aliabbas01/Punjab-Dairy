# Punjab Dairy – Android offline manager (Version 2)

This project is an offline-first Capacitor Android app. Records are stored on the current Android device using IndexedDB. Customers on different devices **do not** receive live data, logins or updates. No internet synchronization or remote authentication is included.

## First login (fresh installation only)

- Username: `punjab`
- Password: `dairy1`

**Important:** Change the default admin password immediately at **More → Backups and admin accounts → Change my password**. Set and safely retain a recovery code. Built-in offline credentials are not appropriate for a remotely accessible or shared public deployment. The app does not offer a public sign-up flow. An existing administrator creates additional admin accounts and customer accounts.

## Main features

- Red-and-white branding sampled from the Punjab Dairy business card, with a cropped card logo.
- Admin dashboard: **total sales = shop sales + home deliveries**, plus milk purchased, expense-adjusted estimated profit, supplier dues and customer receivables.
- Customer and supplier record editor with individual cow/buffalo/yogurt rates. Updated rates apply to **future/newly edited** transactions; recorded historical transaction rates remain on unedited entries.
- Customer daily quantities and uniquely assigned usernames with administrator-created passwords.
- Faster bulk deliveries: all customer rows prefilled, individual checkboxes, select all, editable quantities, one-tap saving. Existing same-day/same-account bulk records are updated rather than added again.
- Supplier purchase tracking and supplier overview for chosen period. Standard payment frequency per supplier: 7, 10, 14, 15, 30 days, or flexible. The overview shows date-range purchase quantity/amount and payments, plus all-time balances.
- Customer home delivery single-entry form with a date-time picker, account, cow and buffalo litres, yogurt kg. Rates are read from the account. Supplier purchases work similarly. Shop sales need manual walk-in rates because no customer account applies.
- Customer view: current month invoice/paid/account balance and previous-month selection; customer cannot edit other customers.
- Printable customer/supplier statements, expenses, staff/salaries, payment entries, JSON backup and CSV transaction export.
- Optional remembered username and keep-signed-in on the **same device** (no plaintext password saved). Do not select persistent sign-in on a shared or unsecured phone.

## Update an existing GitHub repository

Extract this archive. From the project root, copy/update these files in your existing repo: `www/`, `package.json`, `capacitor.config.json`, `README.md` and `.github/workflows/build-apk.yml`. Keep folder structure unchanged.

On your computer:

```bash
git add www package.json capacitor.config.json README.md .github/workflows/build-apk.yml
git commit -m "Punjab Dairy v2 - dashboard, bulk deliveries, suppliers and branding"
git push origin main
```

Open your repository on GitHub → Actions → Build Android APK → select the successful workflow run → Summary → Artifacts → `Punjab-Dairy-Android-APK`. Extract its ZIP for the `app-debug.apk` installer. **This archive is source code, not a compiled APK.**

This project uses `npm install` before generating the Android platform using Capacitor and Gradle. On the runner the Android SDK setup action uses v4, avoiding the removed legacy `tools` package. An APK build still requires the GitHub workflow to complete without errors.

## Backup and data safety

App storage is specific to the Android app/device. Before reinstalling, clearing app data, or switching to a new build with a changed app ID, export a JSON backup using More → Backups and admin accounts. Import this backup on the new installation to restore customers, rates, entries, payments and accounts. Never commit exported business records or credentials to a public repository.

All financial figures rely on entered data; profit is a **rough operating estimate**, not inventory-level audited profit. Monthly staff costs are prorated. Supplier periods are date filters; payment cycles are informational and do not automatically issue transfers. Historical data backup compatibility remains at schema version 1.

## Project file layout

- `www/index.html`, `www/style.css`, `www/app.js` – offline interface and logic
- `www/logo.png`, `www/icon-192.png`, `www/icon-512.png` – Punjab Dairy visual branding
- `www/sw.js`, `www/manifest.webmanifest` – web app support
- `capacitor.config.json` – Android wrapper configuration
- `.github/workflows/build-apk.yml` – GitHub Actions Android debug APK job

## Security / deployment limitations

Offline login and locally stored records are adequate only for a **trusted, controlled device** with operating system lock-screen protection. The first-run default admin password is common to every fresh installation; change it immediately. Password hashes use salted SHA-256 without dedicated password-hardening. Before distributing to unrelated customers on the Play Store, build a proper authenticated backend and synchronize records with role-based access control and secure password storage.
