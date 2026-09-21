# Changelog

All notable changes to TrueMinutes releases.

## [0.9.8] — 2026-09-01

Compared to **0.9.7**:

### Fixed
- **DMG could not open libraries upgraded by a newer Xcode build** — Register `v16_ask_chat` and `v17_embedded_local_ai` schema versions so Ollama releases recognize databases created on the embedded-AI branch (tables are additive; summarization still uses Ollama).
- **Recording stops during Teams screen share on an extended display** — When screen sharing moves UI to a second monitor, Accessibility can go completely blank or emit empty `.left` titles while Teams is still running. Recording now holds through that blackout for up to 45 seconds (aligned with the AX missing-surface grace) and ignores blank-title leave signals during capture.
- **Ollama summarization retained** — This release is built from `main` (local Ollama stack), not the embedded LlamaRuntime branch.

---

## [0.9.1] — 2026-08-18

Compared to **0.9.0** (final usable app release):

### Fixed
- **Recording stops when switching to TrueMinutes during a call** — Extended the Teams/browser “unknown audio” grace period from 5s to 15s so foregrounding TrueMinutes no longer ends an active meeting recording.
- **Accessibility surface detection** — Validates native window presence and refines Microsoft Teams retention logic so joined meetings are not dropped when the scanner temporarily loses visibility.
- **Calendar crash on recurring events** — Prevents `Duplicate values for key` fatal errors when multiple occurrences of the same Google Calendar series are fetched.
- **Build size** — Links only the WhisperKit library product (excludes the WhisperKit CLI from the app bundle).

### Install note (unsigned / no Apple Developer account)
This build is signed with a local **TrueMinutes Internal** certificate, not notarized by Apple. See the `INSTALL — bypass macOS blocker.txt` file inside the DMG for step-by-step instructions.

---

## [0.9.0] — 2026-08-16

Initial internal release: meeting detection, local capture, WhisperKit transcription, Ollama summarization, menu-bar UI, and offline recovery pipeline.
