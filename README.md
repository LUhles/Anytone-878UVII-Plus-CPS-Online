# AnyTone Web CPS v0.4 — experimental RDT channel and zone editor

A static, privacy-first client-side web application intended for the AnyTone AT-D878UVII series. Deploy the `index.html` and `README.md` in the root of a GitHub Pages repository. There is no server, account, codeplug upload endpoint, telemetry, browser storage, or radio USB programming.

## New in v0.4

Against the supplied 14,387,405-byte `D878UVII` RDT file with `V1303` and `V101` markers, the browser successfully decoded:

- 2,600 channel records, including each channel's *logical channel number* (different from the CSV row position), name, and receive frequency.
- 53 zones, including all 2,738 zone memberships, member order, and A/B default channels. The member names were verified against the provided official CPS 4.00 CSV exports.
- The raw second frequency field is shown as **unverified TX data**. It matches official CSV for some records but not all; it is not editable in this version.

The RDT zone manager can reorder members, replace an existing member with a channel from the same RDT (keeping total member count unchanged), and select default A/B channels. The channel editor can edit RX MHz and replace a channel name with **printable ASCII text of exactly the same character count**. All changes patch fixed-length fields in a copy held in memory, with undo and experimental RDT download.

**Limitations:** Creating/deleting zones, adding/removing zone members, renaming zones, changing channel-name length, editing TX/DMR/APRS/tones, and direct USB programming are **not supported**. Modifying variable-length records without a verified serializer risks damaging the rest of the codeplug.

## Safety

The application is an **experimental file editor**. Binary mappings are confirmed against one sample and its reference CSV exports, but modified RDTs have **not been validated by the official CPS**. Never write these exported RDTs to a radio until the relevant compatibility, integrity, and write-safety tests are completed. All downloads get the `_EXPERIMENTAL_PATCHED.rdt` suffix. Keep a known-good original backup.

The application retains codeplug bytes in temporary browser JavaScript memory. It does not use localStorage, IndexedDB, backend APIs, or service workers. JavaScript cannot guarantee secure memory erasure; exported files and OS/browser caches are separate concerns. Do not commit real radio configurations or personal contacts to a public GitHub repository.

## Publish

1. Place `index.html` and `README.md` **at the root** of `main` in your GitHub repository.
2. Settings → Pages → Deploy from a branch → `main` and `/(root)`.
3. After the deployment, hard refresh the site if the older version still displays.

## Verification performed

In headless Chromium, a real uploaded RDT opened and displayed 2,600 channels and 53 zones. The first zone loaded 24 matching member names. Moving a zone member, applying the patch, undoing it, changing an RX frequency and undoing it, renaming a channel with the same length and undoing it, and exporting an experimental RDT were tested without uncaught JavaScript errors. This is **not** an official CPS compatibility test.

## Next milestones

1. Decode/verify TX frequency encoding and channel flags, analog/DMR settings from independently generated reference codeplugs.
2. Develop and test a complete zone serializer to permit adding/removing member slots without corrupting other sections.
3. Test export/import round trips in official CPS 4.00 before enabling a radio-ready export mode.
