# Agent State

This file is the first place future agents should read for current repo state.
Keep it short: `## Now` holds only live entries; the `drift` operator's
hygiene pass rotates landed or superseded entries verbatim to
`docs/history/state-archive.md` (create it on first use) — never summarize
them away, never let them pile up here. Write-time rules: volatile facts
(CI state, counts) carry `as of <commit>`; push status is never recorded
here — git owns it, and unpushed work is mentioned in the moment it
matters, never written down; a count or enumeration another file owns is
pointed to, never copied; machine-specific
facts (local toolchains, host layout, per-clone posture) go to the tracked
`.agents/machines.md`, keyed by machine and dated — never here.

## Now

- Governance bootstrap approved and landing (legacy carve-out): brush-era
  agent rules live in `.agents/repo-guidance.md`; foreign `AGENTS.md`
  removed; toolkit constitution installed by the paired refresh commit.
  Decision recorded in `.agents/decisions.md` (2026-07-16).

## Next

- None recorded.

## Blockers

- None recorded.

## Verification

- See `.agents/repo-guidance.md` (Verification) — the canonical home for the
  verification command. Record here only a deviation active right now.

## Active Sources

- `AGENTS.md`
- `.agents/repo-guidance.md`
- `.agents/decisions.md`

## Unrecorded Repo Memory

- None known.
