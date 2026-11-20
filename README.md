# AnyTone Web CPS — v0.3 alpha (self-hosted, stateless)

Static GitHub Pages website, no backend, telemetry, radio data upload, or browser persistence APIs.

## Actual RDT channel decoder

The v0.3 browser application now decodes **real channel names and receive frequencies from the binary `.rdt`**, without requiring a CSV import. This was confirmed against all **2,600** channel records in one uploaded `D878UVII` / `V1303` / `V101` RDT and the original CPS 4.00 channel CSV: exact names and RX MHz matched all records. The observed layout has a channel count at offset 456, channel records beginning at offset 460, a little-endian 32-bit RX frequency at each record start in units of 10 Hz, and a name at +46 bytes, 16-byte maximum. The record length varies with name length: `77 + name length` bytes for shorter names, 92 for 16-byte names.

**Do not assume this layout works with other firmware or CPS versions.** Full-codeplug integrity, the manufacturer validation rules, checksums, and other fields are unverified.

### Experimental changes

The GUI can change RX MHz in the loaded RDT copy by patching the known 4-byte binary field, keeping all other bytes intact. Exported RDTs are explicitly named `_EXPERIMENTAL_PATCHED.rdt` and must not be written to radios. The official CPS must independently validate that the file opens and retains settings before radio use. Names, TX frequencies, tones, DMR configuration, zones, scan lists and APRS **cannot** be edited from RDT in this version. The separate hex lab remains experimental.

### Other functions

- Upload RDT directly from your computer, parse and page/search actual RDT channels.
- Import/export/edit manufacturer CSV files as a separate workflow.
- Download an experimental RDT copy. Original file never overwritten.
- No USB communication.

## Host via GitHub Pages

Put `index.html` and `README.md` at repository root, then enable Settings → Pages → Deploy from branch → `main` / `/(root)`. Upload **only source code**, never your real `.rdt` or contact exports.

## Privacy notes

File content is read via the browser File API and kept in temporary JavaScript memory. This application makes no outgoing requests and deliberately uses no localStorage, sessionStorage, IndexedDB, backend, telemetry, or service worker. The browser, OS, and user-selected file downloads may still leave recoverable copies or caches; absolute memory erasure cannot be guaranteed. Avoid third-party scripts, analytics and hosting modifications that add network requests.

## Development and validation roadmap

1. Validate decoding against independently generated CPS 4.00 RDT examples, including changed values.
2. Map transmit frequency encoding, channel type, digital and analog fields, contact/group indexes, and zone structures.
3. Add round-trip tests and CPS compatibility tests before enabling a production RDT writer.
4. Only then investigate USB programming.
