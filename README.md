# AnyTone Web CPS v0.7

## Fixes
- RDT safety acknowledgment is now visible on the main workspace rather than hidden in Binary Lab.
- The **Save RDT copy** control is visible near the top, tracks byte patches, and downloads a separate experimental file.
- Edit errors and status messages appear in a visible live feedback box.
- Editing a field without changing any value reports **No differences to save** instead of an ambiguous failure.

## Channels, zones, and zone membership add/delete
Use the Add/Delete (plan) controls on Channels and Zones. They stage intent and allow download of a JSON operations plan. **These operations do not change the RDT.** Creating or removing variable-length records requires a validated binary serializer and reference updates that are not yet available. Do not mistake the operations plan for a usable codeplug.

Fixed-length, experimentally mapped channel/zone edits still patch the in-memory RDT and are exported only after explicit safety acknowledgment. The resulting RDT is unvalidated by official CPS and must not be flashed to the radio.

## Privacy
All RDT bytes and staged operations remain in browser memory. The website does not upload configuration data or save it in localStorage/IndexedDB. Explicit downloads are saved to the user's device.

## Deployment
Copy `index.html` and `README.md` to the root of the GitHub repository's `main` branch; GitHub Pages will redeploy.
