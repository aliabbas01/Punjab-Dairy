# Punjab Dairy V10 — entry amounts, range reports, Urdu supplier bills

Updated on the existing V9 source. The `pk.punjabdairy.manager` Android application ID, `punjab-dairy-data` IndexedDB database and storage version remain unchanged. **Do not uninstall the existing app**. An Android upgrade must be signed with the same certificate to preserve local data. Export and verify a JSON backup first.

## Changes

- Fixed the entry edit preview to use historical rates, matching the recalculated history amount and saved record. Editing a delivery keeps existing rate snapshots.
- The dashboard has Today / This week / This month / Quarter / Year / Custom range filters, with both from/to shown above reporting cards. All-time customer/supplier balances remain labeled all-time.
- Bills have Customer and Supplier tabs and their own account dropdowns. Admin can choose any from/to period for a customer invoice.
- Supplier payment receipt: no individual payment-date list, milk totals only, and dated purchase rows showing milk quantity and amount. No yogurt or buffalo separate rows. Bank and Easypaisa remain customer-only.
- Supplier receipt PDF and PNG exports use the same renderer.

## Build

Unzip over the repository root and run:

```sh
git add .
git commit -m "Punjab Dairy V10 bills and dashboard range updates"
git pull --rebase origin main
git push origin main
```

Then build from GitHub Actions. The source has been syntax-checked; it has **not** been compiled or verified on an Android phone.


## Version 11 – customer address visibility
- Bulk home delivery entry rows show each customer's saved address below the name.
- Home Delivery history grid shows the customer's address below their name.
- Missing addresses show “Address not set”; no database migration or data modification.
