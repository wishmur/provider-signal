# Deployment and secrets

## Facts established

- **Production runtime.** Lovable's `@lovable.dev/vite-tanstack-config` builds this template with the nitro preset `cloudflare-module` by default (`nodeCompat: true`, `deployConfig: true`), or `lovable-fetch-bundle` when `LOVABLE_NITRO_PRESET` selects it. Production is therefore a Cloudflare-Workers-style module worker hosted by Lovable at `<project>.lovable.app`. The project is currently unpublished; only the editor preview URL exists.
- **Server functions.** The worker serves SSR and `createServerFn` handlers from the same nitro bundle. The scaffold's `src/start.ts` already applies CSRF middleware to server-function requests.
- **Production secret path: unverified.** Lovable's public documentation describes a Secrets store for its Cloud edge functions. No documentation was found that those secrets are injected into a TanStack worker's environment, and no documented environment-variable setting exists for TanStack projects. On Cloudflare workers, secrets arrive on the `env` binding; `process.env` is populated only under `nodejs_compat` with process-env population, which the package's `nodeCompat: true` suggests but does not prove.
- **Key is server-only in code.** `ANTHROPIC_API_KEY` is read only inside `brief.server.ts`, never in a `VITE_`-prefixed variable, never in the client bundle.

## Accepted posture (current deployment constraint, not immutable product truth)

- **Lovable public URL:** `AI_MODE=cached`, no API key configured. Cached briefs are served with a clear "Cached output" label. The public endpoint has zero live-call exposure.
- **Local presentation:** `bun run dev` with a local `.env` (git-ignored). Genuine live Anthropic calls; the key never leaves the machine.
- **Key lifecycle:** the Console API key is deleted or rotated in the Anthropic Console on 2026-09-15, the day after the presentation.

## Phase 3 deployment gate

Before any public live endpoint exists, one of the following must hold:

1. A verified secure server-side secret path on the hosting platform **and** enforceable platform-level rate limiting (for example Cloudflare rate-limiting rules or a gateway quota) for the brief endpoint; or
2. The transparent split is retained: cached, clearly labeled output on the public URL and live calls only on the local presentation machine.

In-memory per-isolate throttling is a courtesy control for local runs and is never represented as sufficient protection for a public endpoint.

## Fallback if Lovable hosting cannot safely support the function

Self-deploy the `cloudflare-module` build to Cloudflare Workers with `wrangler secret put ANTHROPIC_API_KEY`, a scoped and rotated key, and a Cloudflare rate-limiting rule on the brief route. Phase 2 verifies `process.env` versus `env`-binding access in a local nitro preview build before relying on either.

## Phase 2 prerequisites

- Confirm `.env` is ignored by git (rules added in Phase 1).
- Run the isolated API smoke test described in `docs/AI_CONTRACT.md`; stop and report on failure.
