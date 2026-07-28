# v5 Product & Software Requirements

## Primary user journey
1. User lands and sees an example finished asset plus one primary CTA: **Create my marketing asset**.
2. User chooses an outcome and market.
3. User enters property notes in a progressive, three-step builder.
4. User generates a finished asset in-page.
5. User edits, regenerates, creates channel variants, copies or exports.
6. Only after value delivery, the user may save locally, subscribe or view a relevant partner offer.

## Functional requirements

### FR-01 Guided builder
- Three steps: Outcome; Property & audience; Tone & details.
- Progress indicator, Back/Next, autosave draft in session storage.
- Required fields are validated inline.
- Quick mode accepts free-form notes; structured mode exposes optional detail fields.

### FR-02 Asset catalogue
Support at minimum: Listing Description, Instagram Caption, Reel Script, Open House Invite, Seller Follow-up Email, Buyer Consultation Script, Price Reduction Announcement, Just Sold Post, Farming Postcard and Listing Launch Bundle.

### FR-03 Market profiles
- Selector defaults from browser locale but never silently assumes legal jurisdiction.
- Profile controls spelling, units, currency formatting, terminology, disclaimer text and prompt instructions.
- v5 profiles: ZA, US/CA, UK/Europe, AU/NZ, Middle East/Other.

### FR-04 Generation
- Generate finished structured content through a secure server-side adapter.
- Return title, body, CTA, hashtags where relevant, compliance notes and channel variants.
- Display loading stages, retry and graceful fallback.
- Never expose provider API keys in browser code.

### FR-05 Output workspace
- Editable rich/plain text blocks.
- Copy individual sections or all content.
- Regenerate whole asset or a selected section.
- Switch channel tabs without losing edits.
- Export TXT and print-friendly HTML/PDF via browser.

### FR-06 Examples and trust
- Show 2–3 representative outputs before input.
- Clearly explain what is generated and what the agent must verify.
- Preserve compliance reminder and add market-specific review text.

### FR-07 History
- No account required.
- Store recent outputs locally with an explicit clear-history control.
- Do not store sensitive client data in analytics.

### FR-08 Email and partners
- Email capture appears after successful output and is optional.
- Sponsor placements are labelled “Partner” or “Sponsored”.
- No sponsor may obscure controls, alter generated content or be required for use.

### FR-09 Accessibility
- WCAG 2.2 AA target.
- Keyboard-complete flow, visible focus, semantic labels, live regions for generation status, reduced-motion support and minimum 44×44 CSS-pixel touch targets.

## Acceptance criteria
- A new user can generate a finished listing asset without login or payment.
- Median happy-path completion is ≤3 minutes in usability testing.
- Generated output remains editable after regeneration failure.
- Mobile widths from 320px upward have no horizontal overflow.
- All critical controls are keyboard accessible.
- API failures produce a useful message and a prompt-only fallback without losing form data.
- Market profile is visible in the output and can be changed before regeneration.
