# ts-playground

Vite + TypeScript (vanilla-ts template). Vitest for tests, Biome for lint/format, Husky gates commits and pushes.

## Non-negotiable: truth over claims

Nothing is "done," "fixed," or "working" until it has been empirically verified in this session. Never say "should work," "this should fix it," or "that looks right" as a substitute for actually running it. If you have not run the proof, say what you have not run.

Every completion claim must be backed by one of:

- **Command output** actually run this session (test results, build output, tsc output) — quote it or summarize what it showed, not what you expect it to show.
- **A test** that exercises the behavior and passes (show the run, not just that a test file exists).
- **An external reference** (official docs, changelog, spec) when the claim is about how a library/API behaves — link or quote the source, don't recall from training.
- **Direct observation** of the running app (dev server output, browser behavior) for UI/runtime changes.

If none of these are possible (e.g. you lack a way to run something), say so explicitly instead of asserting success.

## Required verification before marking work complete

Husky enforces `typecheck` + `lint` + `test:run` on `pre-commit` and `pre-push` (see `.husky/`). A successful `git commit`/`git push` output is the accepted proof for those three — don't re-run them by hand first just to narrate the same result twice. If the hook fails, that failure output is itself the evidence something isn't done yet.

Hooks only run at commit/push time and can't see runtime behavior. So for any change with a runtime surface, still run `npm run dev` and exercise the actual change in the browser before claiming it works — golden path plus at least one edge case. A passing hook proves the code compiles, lints, and passes tests; it does not prove the feature works.

For docs-only or no-runtime-surface changes, explicitly say so instead of claiming verification that doesn't apply.

## Scope discipline

When a fix's easiest path is broader than the problem (e.g. excluding a whole directory from a linter instead of the one offending file, disabling a rule globally instead of overriding it narrowly), prefer the narrowest fix. If a broader change genuinely seems right, ask before applying it — don't apply it and mention it afterward as a footnote.

## Commands reference

| Command | Purpose |
|---|---|
| `npm run dev` | Start dev server |
| `npm run build` | Type-check + production build |
| `npm run preview` | Preview production build |
| `npm run typecheck` | `tsc --noEmit` |
| `npm run lint` | `biome check .` |
| `npm run test` | Vitest, watch mode |
| `npm run test:run` | Vitest, single run (used in hooks/CI) |
