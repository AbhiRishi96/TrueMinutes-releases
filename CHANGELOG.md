# Changelog

All notable changes to TrueMinutes releases.

## [0.8.9] — 2026-10-09

### Improved
- Browser meetings retain recording through tab switches and hidden controls while the meeting host remains running without hang-up evidence.
- Installed meeting web apps receive better background Accessibility detection.
- Live Whisper transcription retains more quiet and accented speech, with longer default chunks and improved decode recovery.
- Native titlebar and traffic lights stay visible, with green-button fullscreen toggling and Escape to exit fullscreen.
- Meeting prompts and the recording pill follow fullscreen meeting Spaces and display the meeting app icon.
- The recording waveform moves more smoothly and stays inside the compact pill.
- Meeting audio capture prefers a built-in device clock when listening through USB, Bluetooth, or external outputs, and discovers browser/Electron audio helpers.

### Fixed
- Transient system-audio startup failures receive bounded retries; failed starts can be retried from the menu panel.
- Recording hold uses sustained meeting-input inactivity as additional hang-up evidence, while retaining browser mute and Accessibility-blackout safeguards.
- Green-button click interception is limited to the actual button and preserves modified clicks.

### Notes
- Browser capture still requires explicit confirmation for that meeting and may include other tabs from the same browser.
- This update uses the existing internal signing channel and is not Apple notarized.

## [0.8.8] — 2026-10-05

### Improved
- **Join island** is a 280×55 capsule with violet Transcribe, then a countdown chip, a one-line news-ticker headline, and a 5px full-width bottom bar that moves green → amber → red as the timer runs out. The teardrop drop / bounce intro is unchanged.
- **Live prompts** keep a smooth 15s countdown; the timer chip turns amber at 10s and red at 5s. **Calendar prompts** show no timer and dismiss manually or one minute after the scheduled start.
- **Recording pill** keeps the deployed compact→expanded morph; Mic uses a slash/color mute affordance with a fixed “Mic” label.
- **Keychain credentials** load from one Data Protection vault item after the first migrate, so launch should present at most one Always Allow instead of a prompt per saved key.

### Fixed
- **Speaker-off meeting capture** uses a Core Audio process tap for native Teams/Zoom and, after the usual per-meeting confirm, for browser Meet/Teams/Zoom, so remote audio is still recorded when Mac speakers are muted or off.
- **Menu bar panel** sizes to its actions instead of collapsing to a header-only strip, so Open, export, recent meetings, Settings, and Quit stay usable.
- **Teams Accessibility scan** no longer crashes the app when a meeting UI node is released while TrueMinutes is reading controls.
- **Internal signing pin** follows the active TrueMinutes Internal leaf so local and CI builds verify against the same certificate.

### Notes
- Browser capture still requires explicit confirmation for that meeting and may include other tabs from the same browser.
- Meeting leave detection, screen-share retention, and recording cutoff behavior are unchanged.
- This update uses the existing internal signing channel and is not Apple notarized.

## [0.8.7] — 2026-10-05

### Improved
- **Join island** drops from the camera as a water drop and settles into a compact 240×40 pill, with the dismiss control on the rim.
- **Calendar pre-join** uses the same island size and motion, with a starting-soon countdown that does not hide the later live-join island.
- **Recording pill** grows from a center hole into the vertical compact pill (including a standard mic control) and the smaller Mic/Stop card, then collapses back into that hole when capture ends.
- **Overlay policy** keeps the island and recording pill visible over fullscreen meeting Spaces without collapsing the recording chrome.

### Notes
- Meeting leave detection, screen-share retention, and recording cutoff behavior are unchanged.
- This update uses the existing internal signing channel and is not Apple notarized.

## [0.8.6] — 2026-10-05

### New
- **Calendar day, week, and month views** with account colors, event details, upcoming countdowns, and Join controls.
- **Home shortcuts** for open action items, recent meetings with processing status, and chats with message previews.
- **Optional Google Calendar connection during setup**, with connection status and a Skip for now action.
- **Custom database row notes** accessible from the Notes workspace.

### Improved
- **Meeting review** has responsive action buttons and audio controls, clearer transcript bubbles, summary previews, and source labels.
- **Library search** covers titles, notes, and transcripts, supports Command-F, and preserves archive and folder scope as results refresh.
- **Notes pages and databases** adapt to narrow windows, filter immediately, restore results when filters clear, and show loading and saving errors.
- **Summary editing** preserves unsaved drafts and reports save failures without closing the editor.
- **Home and sidebar navigation** retain the original scrolling sidebar and remove layout crossfades; chat dates and singular counts are corrected.
- **Privacy and setup** use consistent cards, clearer Google connection states, and isolated keyboard focus.
- **Floating meeting prompts** receive first-click and keyboard input and expose compact Transcribe and dismiss controls.
- **Menu panel** shows all meeting opportunities and distinguishes verified calls from calendar events awaiting a verified join.

### Fixed
- **Recording-start confirmation recovery** shows browser-audio consent in the main window and menu, uses the current pending session for confirmation, and clearly labels the pending decision instead of appearing stuck in detection.
- **Meeting overlay consistency** applies shared fullscreen/Space window configuration to the meeting prompt, browser confirmation, recording pill, and menu panel.
- **Native title-bar layout** leaves scene geometry under SwiftUI ownership to avoid conflicting AppKit layout overrides.
- **Menu dropdown over fullscreen apps** uses a nonactivating panel that opens in the foreground Space without activating the main window.
- **Release notes formatting** renders headings, bold text, and lists in the update window; GitHub releases include the full feature changelog.
- **Final audio transcription** improves recovery of trailing audio and transcript coverage during offline re-transcription.
- **Saved Google credentials** handle Keychain access failures explicitly and preserve usable connection state.
- **Workspace navigation and empty states** refresh selected views, expose row actions, and report failures clearly.

### Notes
- Meeting leave detection, screen-share retention, and recording cutoff behavior are unchanged.
- This update uses the existing internal signing channel and is not Apple notarized.

## [0.8.5] — 2026-10-04

### Improved
- Ask TrueMinutes composes on-device explanations and compares discussed options using cited meeting evidence, with facts separated from interpretation and recommendations.
- Follow-up questions retain meeting scope and date context; reasoning questions include more of the surrounding discussion so later alternatives are less likely to be missed.
- Answers and native tables, task lists, and charts receive citation validation and a separate evidence review before appearing in chat.
- Ask requests can be stopped, with more reliable cancellation and clearer generation errors.

### Fixed
- Fixed a local-model capability check that prevented Ask generation and displayed transcript excerpts instead of a composed answer. Failed generation now reports an error rather than saving a misleading fallback answer.
- Question phrases such as “and what options” no longer become unintended person filters.
- Extractive “Qwen not run” notes are excluded from answer evidence.
- A completed inference request no longer disconnects a healthy helper when its old timeout fires.
- Startup Keychain migration checks existing items without decrypting credentials or presenting authentication prompts.

### Notes
- Ask processing remains local. Evidence review improves grounding but does not guarantee correctness; larger meeting contexts can still take over a minute to answer.
- This update uses the existing internal signing channel and is not Apple notarized.

## [0.8.4] — 2026-10-04

### Fixed
- Google Calendar and Drive sign-in use a secure OAuth service; the Google client secret is no longer bundled in the app.
- Google token refresh preserves saved sessions and protects sign-out and account changes from late refresh results.
- Existing Google connections need one reconnect to migrate to the new sign-in service. Local meetings and encrypted vault data are preserved.

### Changed
- Google connections offer separate sign-out and revoke-access actions.
- Release packages are checked for bundled credentials before publishing.

## [0.8.3] — 2026-10-03

### New
- Encrypted Google Drive sync for meetings, transcripts, summaries, Ask chats, folders, and automation rules across Macs using the same Google account. Audio files stay on this Mac.

### Fixed
- Google Calendar and Drive connections retain their tokens across app relaunch; Keychain saves are verified before reporting a successful connection.
- Older remote snapshots and deletes cannot overwrite newer synced content.
- Drive sync completes the full listing, including libraries spanning more than twenty pages.
- Historical content is uploaded on first connection; interrupted uploads resume from the durable outbox.
- Sync progress and remote changes refresh in the app. Unexpected bulk remote deletes pause for review.

---

## [0.8.2] — 2026-10-02

### New
- **Ask TrueMinutes is now conversational** — Ask follow-up questions about a meeting transcript, summary, decisions, and action items from the meeting detail view.
- **First-time setup is now focused and guided** — New users start with a short setup flow for local AI models and permissions instead of the old product tour.
- **Recommended local models can download in the background** — You can continue setup and use TrueMinutes while transcription and summary models are prepared.
- **Permissions are easier to review** — Microphone, system audio, Accessibility, Calendar, and browser integrations now appear as compact cards with clear status and next steps.

### Improved
- **Meeting answers use better local context** — Ask TrueMinutes retrieves transcript and summary snippets more carefully before generating an answer.
- **Fewer surprise permission prompts** — TrueMinutes now asks for access from setup, Settings, or a feature action instead of prompting automatically on ordinary launch.
- **More reliable recording during screen sharing** — Meet, Teams, Zoom, Webex, and Slack calls are less likely to stop just because a share picker or temporary call window appears.
- **Clearer meeting cleanup** — Recent recordings and meeting details recover more gracefully when transcript, summary, or stop processing finishes after the main capture ends.

### Fixed
- **Ask answers parse more reliably** — JSON decoding and query parsing are more tolerant of model output variation.
- **Finished re-transcriptions no longer leave stale text on screen** — Meeting detail now refreshes after a successful re-transcription instead of continuing to show older polished paragraphs.

---

## [0.8.1] — 2026-09-27

This update focuses on making meeting recording stop and microphone-follow behavior more reliable across Google Meet, Microsoft Teams, and Slack Calls.

### Fixed
- **Google Meet recordings stop after you leave** — TrueMinutes no longer keeps recording just because the browser still has residual audio activity after a Meet call ends.
- **Google Meet microphone follow is safer** — the local microphone now stays off when mute state is missing, stale, ambiguous, or no longer tied to an active call.
- **Microsoft Teams screen share stability** — recording is retained through brief Accessibility blackouts during Teams screen sharing, VDI sessions, tab/window switches, and extended-display transitions.
- **Slack Calls mute sync** — Slack mute/unmute state is detected across sibling call windows so local microphone capture follows the actual call controls more accurately.
- **Release/update reliability** — Sparkle update publishing now builds, signs, uploads the DMG, and updates the public appcast from CI.

### Notes
- This build is internally signed, not Apple notarized. If macOS blocks first launch, use the install instructions included in the DMG.

---

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
