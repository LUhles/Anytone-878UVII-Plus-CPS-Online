# AnyTone 878UVII Plus Web CPS — v0.5

Privacy-first static browser editor. Upload `index.html` to the repository root on GitHub Pages. No backend, cookies, codeplug storage, service worker, analytics, or external runtime dependencies. Your files are read using browser File APIs and processed in memory. Downloads are explicitly user initiated. Browser/process-level memory and downloaded files cannot be guaranteed erased.

## Workspaces
- Overview: decoded channel/zone totals and source distinctions
- Channels: RDT-decoded channel names and RX frequencies, experimental same-length name and RX edits
- Zones: RDT-decoded zone lists; reorder/replace members and change default A/B with fixed-length binary patches
- Systems: CSV-backed talkgroups, RX groups, radio IDs and roaming
- Contacts: CSV-backed digital contacts and signaling contacts
- APRS & GPS: CSV-backed APRS and roaming
- Settings: CSV-backed optional settings, hotkeys, offsets and other settings
- Advanced / CSV: complete original CSV import, edits and export for all 22 manufacturer categories
- Binary Lab: experimental hex inspection/editing with acknowledgment

**CSV sections and RDT data are intentionally independent.** Editing an APRS or settings CSV does not change the loaded RDT. There is no complete, verified AnyTone RDT serializer. Do not program a radio with experimental edited RDTs; validate using the official CPS first.

## Publish
Upload `index.html` and `README.md` to the `main` branch root. With GitHub Pages already set to deploy `main` / `(root)`, changes redeploy automatically.

## Roadmap
1. Validate RDT TX field and channel parameters with controlled, one-variable official CPS exports.
2. Decode APRS/settings and other sections in V1303/V101 RDT, then implement validated field writers.
3. Support variable-length names, channel/zone add/remove, safe round-trip serializer.
4. Full offline RDT verification tests with checksum/section validation and official CPS reopening.
5. Consider browser USB programming only after protocol is independently proven.

This project is not affiliated with AnyTone or RadioFoundry. RadioFoundry provides UI inspiration but uses its own firmware/codeplug conventions; its format is not interchangeable with AnyTone OEM firmware.
