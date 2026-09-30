# Changelog

All notable changes to TrueMinutes releases.

## [0.8.11] — 2026-09-30

### New
- **First-time setup is now focused and guided** — New users start with a short setup flow for local AI models and permissions instead of the old product tour.
- **Recommended local models can download in the background** — You can continue setup and use TrueMinutes while transcription and summary models are prepared.
- **Permissions are easier to review** — Microphone, system audio, Accessibility, Calendar, and browser integrations now appear as compact cards with clear status and next steps.

### Improved
- **Fewer surprise permission prompts** — TrueMinutes now asks for access from setup, Settings, or a feature action instead of prompting automatically on ordinary launch.
- **More reliable recording during screen sharing** — Meet, Teams, Zoom, Webex, and Slack calls are less likely to stop just because a share picker or temporary call window appears.
- **Clearer meeting cleanup** — Recent recordings and meeting details recover more gracefully when transcript, summary, or stop processing finishes after the main capture ends.

### Fixed
- **Finished re-transcriptions no longer leave stale text on screen** — Meeting detail now refreshes after a successful re-transcription instead of continuing to show older polished paragraphs.

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
