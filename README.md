# AnyTone Web CPS — RDT Lab & CSV Workbench (v0.2 alpha)

Static, client-side HTML/JavaScript editor. Host `index.html` on GitHub Pages or your own web server. No backend is required.

## RDT support (experimental, raw binary editing)
- Open an existing AT-D878UVII `.rdt` binary locally in the browser.
- Verify recognizable matching header/trailer 5-byte markers and the `D878UVII` model identifier (not a full file integrity or firmware check).
- Navigate a hex/ASCII preview of any offset and search hex byte sequences.
- Inspect and patch individual bytes with explicit acknowledgment and a protected header/trailer region.
- Undo the last patch, and export a fixed-length, experimental modified copy (`_EXPERIMENTAL_PATCHED.rdt`).
- Never overwrite the uploaded original file.

**Critical:** Arbitrary byte-level editing is NOT semantic RDT editing. This code does not understand channel, zone, APRS, DMR contact, checksums, or dependent structures. It cannot guarantee that output opens in official CPS or is safe to write to a radio. Do not flash experimental output to a radio. This lab is for research only.

## CSV support
- Import multiple official CSV exports; browse/search/edit/add/delete and export all fields.
- Columns are kept as written, without semantic validation or cross-reference reconciliation.
- CSV exports are not written back into the `.rdt` yet.

## Build and hosting
1. Put `index.html` in a GitHub repository root.
2. Under Settings → Pages, deploy the `main` branch root.
3. Open the Pages URL in your browser or copy it to your HTTPS site.
4. Do not publish real `.rdt` and contact files in the public repository.

## Roadmap for real RDT editing
1. Document exact RDT channel and zone binary blocks for CPS 4.00 / V1303 with known test pairs.
2. Build a typed parser that preserves unknown bytes.
3. Make reversible semantic edits, with full field and reference checks.
4. Compare official-CPS-produced before/after codeplugs byte-for-byte; verify the edited file opens in official CPS.
5. Only then consider enabling semantic `.rdt` save and radio programming.

No native radio programming in this version.
