# Namariq Matrix: deployment infrastructure and cost

`index.html` is a cost calculator for hosting Namariq Matrix on Oracle Cloud (OCI).

- Monthly and hourly cost **per client** and **per user**, with VAT shown on every price.
- Three tabs: we host everything on Oracle · client hosts everything · client hosts the database and files.
- User presets (20 / 50 / 100 / 150 / custom). Server sizes, gunicorn `WEB_WORKERS` / `WEB_THREADS` and prices change with the user count.
- Each part can be ticked or unticked. Future / optional parts start unticked.
- Domain registrar and company e-mail comparison.
- **Live Oracle prices**: the page reads Oracle's public price list and checks every part number against the saved snapshot.

## Open it

Oracle only returns live prices to pages opened from a web address, so serve the folder instead of double-clicking the file:

```
python -m http.server 8000
```

Then open http://localhost:8000. Opened as a plain file, the page still works with the saved price snapshot (Oracle price list of 2026-11-02, checked 2026-11-23).

## Accuracy notes

- Oracle prices come from `https://apexapps.oracle.com/pls/apex/cetools/api/v1/products/` (same data as Oracle's cost estimator).
- Free allowances apply once per Oracle account; the calculator adds up all clients' usage before applying them.
- Always Free Arm (A1): the page uses 1,500 OCPU-hours / 9,000 GB-hours (Oracle's Always Free page), not the 3,000 / 18,000 still shown in the price list.
- User capacity numbers are planning estimates. Confirm with `ops/loadtest.py` in the main repo.
- Domain and e-mail prices are list prices before tax, checked 2026-11-23.
