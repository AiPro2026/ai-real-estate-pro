# v5 SDLC, Test, Release & Codex Implementation Plan

## Delivery phases
### Phase 0 — Baseline
- Capture current Lighthouse, bundle size and funnel baseline.
- Add CI, formatting, linting, TypeScript and test harness.
- Create feature flag for direct generation.

### Phase 1 — P0 Core value
- Migrate to React/TypeScript/Vite without visual regression.
- Implement three-step builder, examples, loading states and output workspace.
- Implement secure generation gateway and prompt-only fallback.
- Add copy/export and responsive/mobile QA.

### Phase 2 — P1 Adoption
- Add market profiles, channel variants, local history and post-value email capture.
- Add accessibility remediation and analytics events.

### Phase 3 — P2 Revenue and optimisation
- Add configuration-driven partner placements.
- Add quality scoring only after observing real output usage.
- Run 8–12 agent usability sessions and iterate.

## Test strategy
### Unit
- Market profile mapping.
- Asset configuration.
- Zod validation.
- Prompt assembly.
- Output transformations.
- Local storage migration and clear-history.

### Component
- Step validation and navigation.
- Loading/error/success states.
- Copy and export controls.
- Sponsor labelling.
- Email capture timing.

### Integration
- Frontend request/response schema compatibility.
- Gateway rate limit and provider failure mapping.
- Feature-flag fallback.

### E2E
1. Generate listing on mobile.
2. Generate launch bundle and switch variants.
3. Change market and regenerate.
4. API failure preserves draft and offers prompt fallback.
5. Keyboard-only completion.
6. Clear local history.

### Quality gates
- Typecheck: zero errors.
- Lint: zero errors.
- Unit coverage: ≥80% for domain/services; ≥70% overall initially.
- Lighthouse target: Performance ≥90, Accessibility ≥95, Best Practices ≥95, SEO ≥95 on production-like build.
- No critical or high dependency vulnerabilities accepted without documented exception.

## Analytics taxonomy
Events: `landing_view`, `example_viewed`, `builder_started`, `step_completed`, `generation_requested`, `generation_succeeded`, `generation_failed`, `section_edited`, `variant_selected`, `content_copied`, `content_exported`, `history_saved`, `history_cleared`, `email_prompt_viewed`, `email_submitted`, `partner_viewed`, `partner_clicked`.

Required properties: anonymous session ID, market, asset type, channel, feature-flag state, duration bucket. Never send raw property notes, full addresses, client names, generated content or email address as analytics properties.

## Definition of Done
- Requirements and acceptance criteria met.
- Tests added and passing.
- Accessibility checks completed.
- Analytics events implemented and verified.
- Documentation updated.
- Security review completed for API changes.
- Mobile and desktop screenshots attached to PR.
- Rollback path tested.

## Codex execution instructions
1. Read all files under `docs/v5/` before changing code.
2. Inspect the existing repository and preserve current public URLs and GitHub Pages deployment.
3. Create a new implementation branch: `feat/v5-guided-asset-generation`.
4. Make small, reviewable commits in this order: tooling; design tokens/components; builder; generation client/gateway contract; output workspace; localisation/history; analytics/partners; tests/CI/docs.
5. Do not hard-code provider keys, sponsor URLs, market text or asset definitions in components; use configuration and environment variables.
6. Use TypeScript strict mode and schema validation at boundaries.
7. Keep a prompt-only fallback and do not remove the current working experience until direct generation is verified.
8. Run all quality gates and include results in the PR body.

## Suggested GitHub issues
- #1 Vite/React/TypeScript migration and CI.
- #2 Design system and accessible primitives.
- #3 Guided three-step asset builder.
- #4 Secure AI generation gateway and contracts.
- #5 Editable output workspace and exports.
- #6 Market profiles and localisation.
- #7 Local history and post-value email capture.
- #8 Analytics and privacy controls.
- #9 Configuration-driven sponsor placements.
- #10 E2E, accessibility, performance and release readiness.

## PR template
```md
## Summary

## Requirements covered

## Screenshots / recordings

## Test evidence
- [ ] lint
- [ ] typecheck
- [ ] unit
- [ ] E2E
- [ ] accessibility
- [ ] Lighthouse

## Security / privacy

## Analytics events

## Rollback

## Risks and follow-ups
```
