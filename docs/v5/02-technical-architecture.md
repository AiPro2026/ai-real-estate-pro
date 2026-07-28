# v5 Technical Architecture

## Architecture decision
Adopt **React + TypeScript + Vite** for the frontend. Keep GitHub Pages for static hosting. Add a provider-neutral serverless generation gateway. The frontend must remain deployable without the gateway; in that state it offers the current prompt-only fallback.

## System context
```text
Browser
  └─ React/Vite SPA
      ├─ UI components
      ├─ domain models and validation
      ├─ local history/session draft
      ├─ analytics adapter
      └─ GenerationClient
             │ HTTPS
             ▼
      Serverless API gateway
      ├─ rate limiting
      ├─ abuse controls
      ├─ request validation
      ├─ AI provider adapter
      └─ structured response validation
```

## Frontend structure
```text
src/
  app/                routing, providers, feature flags
  components/         reusable UI primitives
  features/
    builder/          steps, validation, draft state
    generation/       request lifecycle and output workspace
    playbooks/        daily workflows
    examples/         output previews
    partners/         labelled placements
    history/          local-only recent work
  domain/
    assets.ts         asset definitions
    markets.ts        locale and terminology profiles
    prompts.ts        provider-neutral prompt assembly
    schemas.ts        Zod request/response schemas
  services/
    generationClient.ts
    analytics.ts
    storage.ts
  styles/             tokens, base, utilities
  tests/
```

## Core contracts
```ts
export type MarketId = 'ZA' | 'US_CA' | 'UK_EU' | 'AU_NZ' | 'ME_OTHER';
export type AssetType =
  | 'listing_description' | 'instagram_caption' | 'reel_script'
  | 'open_house_invite' | 'seller_follow_up_email'
  | 'buyer_consultation_script' | 'price_reduction'
  | 'just_sold' | 'farming_postcard' | 'listing_launch_bundle';

export interface GenerationRequest {
  requestId: string;
  market: MarketId;
  assetType: AssetType;
  property: { type: string; location?: string; price?: string; bedrooms?: number; bathrooms?: number; features: string[]; notes: string };
  audience: string;
  tone: string;
  channels: string[];
}

export interface GeneratedSection { id: string; label: string; content: string; }
export interface GenerationResponse {
  requestId: string;
  title: string;
  sections: GeneratedSection[];
  variants: Record<string, GeneratedSection[]>;
  reviewNotes: string[];
  model?: string;
}
```

## API
`POST /v1/generate`
- Request body: `GenerationRequest`.
- Response: `GenerationResponse`.
- Validate both sides with the same versioned schema.
- Return `400` validation, `429` rate limit, `502` provider failure and `503` unavailable.
- Never return raw provider errors or secrets.

## Security
- API key only in serverless environment variables.
- CORS allowlist for production and preview origins.
- Per-IP and per-session rate limits; configurable quotas.
- Request size limit and content-length enforcement.
- Strip unnecessary personal information from logs.
- CSP, HTTPS, dependency scanning and locked package versions.
- Treat property addresses and client notes as potentially sensitive; do not persist server-side by default.

## Reliability
- Abortable requests with 30–45 second client timeout.
- One automatic retry only for transient failures.
- Preserve draft and prior output.
- Feature flag `directGeneration`; fallback builds a copy-ready prompt locally.

## Deployment
- GitHub Actions: install → lint → typecheck → unit tests → build → Playwright smoke tests → deploy Pages.
- Serverless gateway deployed separately with environment-specific secrets.
- Preview deployments for PRs where available.
- Rollback: revert deployment or disable `directGeneration` remotely.
