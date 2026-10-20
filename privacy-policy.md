# Aside — Privacy Policy

**Effective date:** 2026-10-20
**Last updated:** 2026-10-20
**Status:** Published. This document was prepared without independent legal review; it is updated in place when anything changes.

---

## 1. About this policy

This is the privacy policy for **Aside**, a macOS application that listens through the microphone (and, when enabled, the meeting audio on your Mac) during interview practice or live interviews, transcribes the audio on your Mac or through a speech-to-text service you select, and surfaces tailored answer suggestions grounded in the user's CV. Aside is published by **Naresh Kumar Singh** ("we", "us"), based in Oakville, Ontario, Canada.

If you have questions about this policy or want to exercise any of the rights described below, contact us at **nareshkumar.singh@gmail.com**. We aim to respond within thirty (30) days.

---

## 2. What data we collect

We collect only the data needed to deliver the product. Concretely:

| Data | Source | Purpose | Where it lives |
|---|---|---|---|
| **Apple user identifier (`sub`)** | Sign in with Apple | account identity | Cloudflare D1 (our backend) |
| **Email address** (only if you elect to share it via Sign in with Apple) | Sign in with Apple | account communication | Cloudflare D1 |
| **CV file content** (PDF, DOCX, or text you upload) | You, during onboarding | extracting persona, skills, achievements to ground answer generation | OpenAI Files (transient processing) + Cloudflare D1 (extracted persona) |
| **Microphone audio** | Your Mac's microphone | local transcription via Apple Speech | **Audio is never sent to our servers.** Discarded after transcription. |
| **Live audio** (your microphone and, when you enable it, the meeting audio playing on your Mac) | You, during a live session | speech-to-text | Transcribed on your Mac by Apple Speech, or streamed to AssemblyAI for transcription when that engine is selected. Audio is not stored by Aside. |
| **Live transcript text** (the words detected from the audio above) | Apple Speech Recognition or AssemblyAI | feeding the answer generator | local SQLite buffer on your Mac (active session); sent to our backend only when you request an answer; Cloudflare D1 history (after end-of-session sync) |
| **Question / answer pairs** (the questions detected and the answers Aside generates) | Aside's answer engine | Live overlay display + History tab | local SQLite + Cloudflare D1 |
| **Generated resumes / cover letters** | Aside's document generator | display + download | Cloudflare D1; you can export to your Mac |
| **Subscription state** | Apple In-App Purchase (Phase 4) | enforcing plan limits (Starter Pack / Comfort Pack / Supernova Pack) | Cloudflare D1 |
| **Operational telemetry** (request counts, error codes, latency, model identifier) | our own backend | reliability and cost monitoring | Cloudflare Workers logs (24-hour retention) |

We do **not** collect:
- Your contacts, calendar, photos, or location
- Any data from other applications running on your Mac
- Browser history, passwords, or autofill data
- Device fingerprinting data (IP addresses are seen at the edge by Cloudflare for routing but are not joined to your account record)

---

## 3. How we use your data

We use the data above to:

1. **Sign you in** (Apple `sub` + email)
2. **Generate answers, resumes, and cover letters** (your CV content + live transcript)
3. **Show you your past sessions** (history)
4. **Enforce plan limits** (subscription state)
5. **Monitor service health** (operational telemetry, aggregated)

We do **not**:
- Sell your data to third parties
- Use your CV content or transcripts to train any AI model (ours or anyone else's)
- Send marketing email or use the email for anything other than account-related communication
- Share your data with employers, recruiters, or anyone you might be interviewing with

---

## 4. Sub-processors (third parties that process data on our behalf)

| Sub-processor | Purpose | Data handled |
|---|---|---|
| **Apple Inc.** | Sign in with Apple, App Store distribution, Apple Speech Recognition, In-App Purchase | identity token, optional email, microphone audio (transcribed on-device by Apple Speech when that engine is selected), subscription receipt and server notifications |
| **AssemblyAI, Inc.** | Streaming speech-to-text when the AssemblyAI engine is selected (the default for signed-in users) | live audio streamed from your Mac over an encrypted WebSocket; the resulting transcript text. Our backend issues short-lived access tokens; it never receives the audio. AssemblyAI is based in the United States. |
| **Cloudflare, Inc.** | Workers (compute), D1 (database), KV (sessions, rate limits), Queues (background generation), Workers AI (inference for the live answer path) | all server-side data including extracted CV persona, history records, generated documents, and the transcript window and prompt sent for each answer |
| **OpenAI, L.P.** | Inference (answer generation, resume generation, cover letter generation, persona extraction) and File Storage / Vector Stores for retrieval-augmented prompting | CV content (uploaded as a file for persona extraction; deleted at end of pipeline), transcript-derived questions, generated answers. **Per OpenAI's API data-handling commitment, prompts and completions submitted via the API are not used to train OpenAI models.** |

If we add or change sub-processors materially, we will update this policy and (if your account is active) notify you in-app.

---

## 5. Where your data is stored, and where it travels

- **Cloudflare D1** (our database) is hosted on Cloudflare's globally distributed network. Your row may live in any of Cloudflare's data centers.
- **Cloudflare Workers** (our backend code) executes at the edge node closest to you when you make a request.
- **OpenAI's data centers** are in the United States. Calls to OpenAI from our backend therefore involve a transfer of your CV content and transcript-derived prompts to the United States.
- **AssemblyAI** processes streamed audio in the United States. When the AssemblyAI engine is selected, live audio travels directly from your Mac to AssemblyAI; our backend only issues the access token.
- **Cloudflare Workers AI** runs inference on Cloudflare's network for the live answer path; the transcript window and grounding context for each answer are processed there.

By using Aside you consent to these international transfers.

---

## 6. Retention

| Data | Retention |
|---|---|
| Microphone audio | Discarded immediately after local transcription. Never reaches our servers. |
| Live transcript (active session) | Retained on your Mac in the local SQLite buffer; you control when to clear it via Settings → Privacy & Overlay |
| Live transcript (after end-of-session sync) | Retained in Cloudflare D1 until you delete it |
| Generated resumes / cover letters | Retained in Cloudflare D1 until you delete them |
| Question/answer pairs (history) | Retained until you delete them |
| Operational logs | 24 hours on Cloudflare (request-level logs); aggregated counts kept longer |
| Account record | Until you delete your account, then erased within 30 days from our active stores. Backup copies may persist for an additional 30 days. |

You can delete individual sessions, profiles, and documents from inside Aside at any time. To delete your entire account, contact **nareshkumar.singh@gmail.com**; we will confirm receipt and complete the deletion within 30 days.

---

## 7. Your rights

Depending on where you live, you may have the right to:

- **Access** the personal data we hold about you
- **Correct** inaccurate data
- **Delete** your data ("right to erasure")
- **Port** your data (we provide history export from inside the app; for other data contact us)
- **Object to or restrict** certain processing
- **Withdraw consent** for any processing that relies on consent
- **Lodge a complaint** with your data protection authority

To exercise any of these, email **nareshkumar.singh@gmail.com** with the subject line `Data Subject Request`. We will verify your identity using the Apple `sub` associated with your account before acting on the request.

We respond within 30 days. Where local law gives you a longer timeframe (e.g. 45 days under CCPA), we may take that long but will keep you informed.

---

## 8. Children

Aside is not intended for users under 13 years of age. We do not knowingly collect personal data from children under 13. If you believe a child has provided personal data, contact us and we will delete it promptly.

---

## 9. Security

- Transport: TLS 1.2+ for every request between Aside and our backend (enforced by App Transport Security in Info.plist).
- At-rest on Cloudflare: D1 and KV are encrypted at rest by Cloudflare.
- At-rest on your Mac: the local transcript SQLite buffer is currently stored as plain SQLite with POSIX 0600 permissions (owner-only readable). We are working on full SQLCipher encryption; until then, anyone with your Mac account password and physical access to the device could read the buffer. For maximum security, sign out of Aside and purge data after sensitive sessions.
- Authentication: Sign in with Apple only. We never see your Apple password. Session tokens are short-lived (10 minutes) with rotating refresh.
- Sub-processor practices: see Section 4.

We do not promise security. No system is unbreakable. If we learn of a breach affecting your data, we will notify you without undue delay and in accordance with applicable law.

---

## 10. Changes to this policy

We will update this policy from time to time. The "Last updated" date at the top will reflect the most recent change. Material changes (e.g. a new sub-processor, a substantive change to data we collect) will be flagged in-app the next time you sign in. Continued use after a material change constitutes acceptance.

---

## 11. Contact

- **Email:** nareshkumar.singh@gmail.com

---

> **Drafting note:** this policy is a starting point. Before publishing, have a privacy lawyer in your operating jurisdiction (Canada — PIPEDA + provincial; plus GDPR if you market to Europe + CCPA if you market to California users) review and finalize. The structure here covers most common requirements but is not a substitute for legal advice.
