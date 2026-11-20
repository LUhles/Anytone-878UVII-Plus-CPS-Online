# AnyTone Web CPS v0.6 — RDT decoding expansion

**Status: experimental; NOT a full RDT reader/writer.**

## What is implemented
- Reads locally selected AnyTone `D878UVII` RDT with observed `V1303` / `V101` markers.
- Decodes actual channel records and zone memberships without an imported CSV.
- RDT channel table includes name, RX, calculated TX, analog/digital mode, power, bandwidth, RX color code, time slot, and TX prohibit.
- Experimental fixed-byte channel edits of those fields (when a record passes guard checks).
- Zone member reordering/replacement and default A/B selection, fixed member counts only.
- New Overview/RDT coverage panel clarifies which portions are supported.
- All existing 22-category CSV workspaces and binary lab retained; CSV edits do NOT update RDT.
- Files remain in browser memory: no account, server upload, localStorage, IndexedDB, persistence, service-worker cache, or codeplug analytics.

## Evidence / validation
Compared 2,600 channel records from the uploaded V1303 RDT against the official channel CSV. RX/TX matches 2,599 of 2,600 using TX encoding byte at record+4 and offset at +5. The one exception is `Channel VFO B` (special-purpose record) and will be read-only. The mode (+9), power (+10), bandwidth (+11), TX prohibit (+13), RX CC (+38), and slot (+39) mappings matched the exported CSV rows in the sample. These are verified *against one sample*, not independently validated against hardware or official CPS reimport after modifications.

## Important limitations
- Not a complete RDT parser: contacts, APRS, settings, scan lists and other binary sections are not yet decoded.
- No new channels, varying-length channel names, or zone member insertion/removal.
- No USB/COM-port read or write.
- Modified RDT downloads are **UNVERIFIED** for CPS round-trip. Do NOT flash a radio with these files before official CPS verification and backup.
- Frequency editing only accepts 100–999 MHz as a structural guard, not an authorization to transmit. Users must comply with spectrum licensing and their device limits.
- The stateless design avoids deliberate persistence, but browser/OS memory erasure and downloaded file retention cannot be guaranteed.

## Deploy
Replace root `index.html` and `README.md` on GitHub `main` branch. GitHub Pages redeploys automatically. Codeplug and user CSVs must not be committed to public GitHub.
