# Vocare — Privacy Policy

**Effective date:** to be set at first public release (YYYY-MM-DD)
**Last updated:** 2026-04-30 (draft v3 — added Calibre as a local read source; corrected privacy contact address)
**Controller:** MestreShao Studios, Switzerland (operating under trade name "Mestre Shao Tools")
**Contact for privacy matters:** legal@mestreshao.studio
**General contact:** support@mestreshao.studio

> **Human-legal-review status.** This draft has been reviewed by the author (Claude Code, April 2026) against the relevant legal frameworks cited above to the best of its ability. It is not a substitute for review by a human lawyer licensed in your jurisdiction, but it is written to match what the code actually does and to satisfy Apple App Store submission requirements and GDPR/Swiss FADP structural requirements. Before publishing as the App Store-linked privacy URL, Caio Marsili should read it end-to-end and confirm every factual claim matches his understanding of Vocare's behaviour.

---

## 1. The One-Line Summary

Vocare runs entirely on your Mac. Your books, highlights, API keys, and generated flashcards never leave your device except when **you deliberately trigger** an action that sends a word to a third-party AI service **you have configured** with **your own API key**. MestreShao Studios has no servers and receives no data about you.

## 2. Who We Are (Data Controller Under GDPR / Swiss FADP)

- **Legal entity:** MestreShao Studios
- **Jurisdiction:** Switzerland
- **Trade name for software products:** Mestre Shao Tools
- **Privacy contact:** legal@mestreshao.studio
- **Supervisory authority (right to lodge a complaint):** Swiss Federal Data Protection and Information Commissioner (FDPIC), https://www.edoeb.admin.ch/. If you are in the EU/EEA, you may also lodge a complaint with your local supervisory authority under GDPR Art. 77.

## 3. Summary of What Personal Data We Process

Under Apple's App Privacy Details framework and GDPR's data-category convention, the answer is:

| Data category | Collected by MestreShao Studios? | Stored where? |
|---|---|---|
| Contact Info (email, name, phone) | **No** | — |
| Health & Fitness | **No** | — |
| Financial Info | **No** | — |
| Location | **No** | — |
| Sensitive Info | **No** | — |
| Contacts | **No** | — |
| User Content (books, highlights, cards) | **No — stored only on the user's own Mac** | `~/.vocare/` on your Mac |
| Browsing History | **No** | — |
| Search History | **No** | — |
| Identifiers (user ID, device ID) | **No** | — |
| Purchases | **No** | — |
| Usage Data | **No** | — |
| Diagnostics (crash logs) | **No — stored locally, uploaded only if the user manually attaches one to a bug report** | `~/.vocare/logs/` on your Mac |
| Other (API keys for third-party services) | **No — stored only on the user's own Mac** | `~/.vocare/config.json` on your Mac |

**We are not a data controller for any of this data.** Every item above is held by you, on your own device, under your own user account.

**We are also not a data processor for any of it.** No data flows to us.

## 4. What Vocare Stores Locally on Your Mac

All of the following lives only on your Mac, inside `~/.vocare/`:

| File / folder | Contents | Purpose | Retention |
|---|---|---|---|
| `config.json` | API keys, chosen providers, field mappings, language settings | App remembers your setup | Until you delete or edit |
| `library.json` | Your scanned books, import status, highlight counts | Library grid state | Until you delete |
| `result_cache.json` | AI translations keyed by (book, word) | Avoid paying to re-translate | Until you clear the cache |
| `images/` | AI-generated illustrations | Image cache | Until you clear the cache |
| `audio/` | AI-generated pronunciation audio | Audio cache | Until you clear the cache |
| `trash/` | Soft-deleted cache awaiting cleanup or restore | Safety net | Auto-purged after the period set in Settings (default 30 days) |
| `logs/vocare.log` | Diagnostic log of in-app actions | Troubleshooting | Rotated at 5 MB, 3 backups kept |
| `logs/crash_*.log` | Crash traceback + app version + time | Bug reports | Auto-deleted after 30 days on next launch |

You can delete the entire `~/.vocare/` folder at any time. Next launch will recreate it empty.

## 5. What Data Leaves Your Device, When, and to Where

Vocare opens an outbound network connection **only in response to an explicit user action**. No background sync. No telemetry. No analytics beacons. No update pings.

### 5.1 AI service calls (only when you process a highlight)

When you click "Create Anki Cards" or trigger auto mode, Vocare sends the following to whichever third-party AI service you configured in Settings, **using your own API key**:

| Provider (role) | What is sent | Purpose |
|---|---|---|
| Anthropic Claude or OpenAI GPT-4o (translation) | The highlighted word; the surrounding passage from the book (±2 sentences); your target language setting | Generate translation, example, explanation, alt-meanings |
| ElevenLabs or macOS `say` or gTTS (TTS) | The highlighted word; target language | Generate pronunciation audio |
| OpenAI GPT Image 1.5 or Ideogram or FAL.AI Flux (image) | A prompt derived from the word, translation, explanation, and example | Generate illustration |

**You are the direct customer of each provider.** Each request uses your own API key stored in your `config.json`. MestreShao Studios is not a party to any of these transactions, does not see the request or response, and has no access to the data exchanged.

Each provider has its own privacy policy governing the data they receive from you:

- Anthropic — https://www.anthropic.com/legal/privacy
- OpenAI — https://openai.com/policies/privacy-policy
- ElevenLabs — https://elevenlabs.io/privacy
- Ideogram — https://ideogram.ai/legal/privacy-policy
- FAL.AI — https://fal.ai/privacy-policy

### 5.2 AnkiConnect (local only, never over the internet)

When you send a card to Anki, Vocare POSTs to `http://127.0.0.1:8765` — **your own machine**. This is the local AnkiConnect plugin inside the Anki desktop app. The payload contains the card fields, audio file path, and image file path. This traffic never leaves your Mac.

### 5.3 What Vocare **never** does

- Does not open outbound connections unprompted.
- Does not send analytics, telemetry, usage statistics, error reports, device info, installation info, or any other "phone-home" data to MestreShao Studios, to any Mestre Shao server, or to any third party not listed in § 5.1.
- Does not read, index, or upload your book files, highlight data, or card content **except** during the actions described in § 5.1 and § 5.2.
- Does not require an account, login, signup, or email address.
- Does not place tracking cookies. There is no web content in the app that could.
- Does not profile you. There is no "user profile" concept in the codebase.
- Does not use third-party SDKs for advertising, attribution, crash reporting, analytics, or engagement tracking.
- Does not cross-reference user data with any other source.

## 6. Lawful Basis for Processing (GDPR Art. 6)

Because MestreShao Studios does not collect any personal data from you, GDPR Art. 6 lawful-basis requirements apply to **you and the third-party AI services** you choose to use, not to us. When you trigger an AI call:

- The basis is your **explicit action** (clicking a button). In GDPR terms this aligns with "consent" and "performance of a contract" (the contract is between you and the AI provider, arising from your API key use).
- You can withdraw at any time by: not clicking the button, deleting your API key from Settings, or uninstalling Vocare.

## 7. Reading Your Highlights (Local-Only)

When you point Vocare at a source of highlights, Vocare reads them directly from your local filesystem. Three sources are supported:

**Kobo e-reader via USB.** Vocare reads from the device's filesystem:

- KOReader `.sdr` sidecar files (if present)
- The Kobo native SQLite database (`.kobo/KoboReader.sqlite`, read-only)

**Your Calibre library.** Vocare reads from the local Calibre database to surface highlights you marked in Calibre's viewer:

- `metadata.db` SQLite (opened read-only, with a 1-second timeout if Calibre has the database locked — Vocare backs off cleanly and shows a status-bar message rather than blocking)
- The `.epub` files in the library folder for context extraction

**Standalone `.epub` / `.kepub` folders.** Vocare scans for ebook files and looks for sibling KOReader `.sdr` directories.

In all three cases, the read is **local**. Nothing about your library, highlights, or notes is sent anywhere by Vocare itself. The rules in § 5.1 only apply when *you* deliberately trigger a card-generation action on a specific highlighted word.

## 8. Crash Logs

If Vocare crashes, a crash log is written to `~/.vocare/logs/crash_YYYYMMDD_HHMMSS.log`. The log contains:

- Python traceback
- Vocare version
- Timestamp

Crash logs are **not** automatically uploaded. If you choose to attach one to a GitHub bug report (at `github.com/MestreShao-Studios/vocare-issues`, created at public beta release), you are doing so voluntarily, and you can read the log first to confirm it contains nothing you would rather not share. Crash logs older than 30 days are deleted automatically on next launch.

## 9. API Keys

Your API keys for each provider are stored as plain JSON in `config.json`. This is a deliberate choice: the macOS Keychain integration adds installation complexity on first run, and the file is already on your own machine protected by your macOS user account and FileVault (if enabled). The trade-off: if your macOS account is compromised, your API keys in `config.json` are readable; the same is true of any Keychain password once the account is unlocked.

If you share your Mac with others, create separate macOS user accounts — `~/.vocare/` is per-user.

**To revoke access** for any provider: delete the key from Settings (or regenerate the key in your provider's dashboard, which invalidates the old one). Vocare cannot call a provider for which it holds no key.

## 10. Children's Privacy

Vocare is not designed for and not directed at children under 13 (US COPPA threshold) or under 16 (certain EU member-state thresholds under GDPR Art. 8). Vocare does not knowingly collect data about anyone. Because there is no account and no tracking, we cannot know the age of any user. If a parent believes their child has installed Vocare and wishes to confirm no data was collected, the answer is: **Vocare collects nothing centrally**. All data stays on the child's Mac under their macOS account.

Parents who want to restrict Vocare usage should use macOS Screen Time / parental controls at the operating-system level.

## 11. Your Rights Under GDPR and Swiss FADP

Because MestreShao Studios does not hold any of your personal data, you exercise these rights directly on your own Mac:

| Right | How to exercise it |
|---|---|
| **Access (Art. 15 GDPR)** | Open `~/.vocare/` and read the JSON/log files |
| **Rectification (Art. 16)** | Edit the JSON files directly, or use in-app Settings |
| **Erasure / "Right to be forgotten" (Art. 17)** | Delete `~/.vocare/` |
| **Restriction of processing (Art. 18)** | Stop launching the app; remove the API keys from Settings |
| **Data portability (Art. 20)** | Copy `~/.vocare/` to wherever you like — it's already in open JSON/PNG/MP3/AIFF formats |
| **Objection (Art. 21)** | Quit the app; remove API keys |
| **Withdraw consent (Art. 7(3))** | Uninstall |
| **Lodge a complaint (Art. 77)** | Swiss FDPIC (https://www.edoeb.admin.ch/) or your EU/EEA local supervisory authority |

For data you have deliberately sent to a third-party AI provider (§ 5.1), those rights are exercised with that provider directly, using the privacy-contact channel in their own privacy policy.

## 12. Data Transfers Outside Switzerland / EEA

MestreShao Studios does not transfer your data anywhere — because MestreShao Studios does not hold your data.

When you trigger an AI call (§ 5.1), your request travels from your Mac directly to the provider you selected. Most of the providers listed are based in the United States. This is **your** international transfer, not ours. Your decision to use a US-based AI provider is made each time you enter that provider's API key into Settings and click the button that triggers a call to it.

## 13. Security

Security of your data is a function of:

- **macOS account security** (your password; FileVault full-disk encryption if enabled; File System Protection for `~/.vocare/`).
- **Each third-party AI provider's security** for data you send them (TLS in transit, their own storage security, their own retention and breach-notification obligations).
- **Vocare's code** — open architecture, no code obfuscation, auditable. The source will be available to security researchers on request; it is not public at launch to protect against pre-launch cloning, but the binary is macOS-notarized and its behaviour is documented in this policy.

## 14. Changes to This Policy

Material changes ship with the next Vocare release. The **Last updated** date at the top of this document changes. A summary of what changed is posted in the release notes on the GitHub release page at `github.com/MestreShao-Studios/vocare-issues/releases` (created at public beta release). Old versions of this policy are preserved in the Git history of the Vocare source repository.

You are encouraged to re-read this policy at each major version update.

## 15. Contact

- **General support:** support@mestreshao.studio
- **Privacy questions:** legal@mestreshao.studio
- **Bug reports:** https://github.com/MestreShao-Studios/vocare-issues (at public beta release)
- **Supervisory authority (Switzerland):** FDPIC — https://www.edoeb.admin.ch/

---

## 16. Plain-Language Summary (Required by GDPR Art. 12 — "Concise, transparent, intelligible")

Seven sentences:

1. Vocare is a Mac app. It runs only on your Mac.
2. Everything it stores stays on your Mac. Delete `~/.vocare/` and it's gone.
3. When you click a button to process a word, it sends that word to whichever AI service you configured — with your own API key. You are that AI service's customer, not us.
4. We (MestreShao Studios) have no servers and see none of your data.
5. There is no account, no login, no tracking, no analytics, no cookies, no ads, no telemetry.
6. When you send a card to Anki, it stays on your Mac — AnkiConnect runs locally.
7. If you have a question, email legal@mestreshao.studio.

---

## Policy Version History

| Version | Date | Notes |
|---|---|---|
| 3 | 2026-04-30 | Added Calibre annotation reading (§ 7) — Vocare gained Calibre integration in v4.36 (2026-04-28); the privacy section needed to reflect that Calibre is now a third local-only highlight source alongside Kobo USB and standalone EPUB folders. Privacy contact corrected from `privacy@mestreshao.studio` (not yet provisioned per the playbook's email-address map) to `legal@mestreshao.studio` (the existing studio address for legal/privacy concerns). If `privacy@` is later set up as an alias, the policy should swap back. |
| 2 | 2026-04-15 | Self-review against GDPR Art. 13/14, Swiss FADP, and Apple App Store requirements. Added: controller identification, right-to-lodge-complaint, lawful-basis section, retention-period table, data-transfer section, security section, plain-language summary (GDPR Art. 12 requirement), full data-category matrix for Apple App Privacy Details. Human-lawyer-review caveat added at top. |
| 1 (draft) | 2026-04-15 | Initial draft — factually accurate to the code but missing some GDPR structural requirements. Superseded. |
