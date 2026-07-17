# Agent Decisions

Record durable repo decisions here. Do not use this as a chat log. Each entry should make
sense without conversation history and should name superseded guidance when relevant.

Keep this file to what is currently in force or still open. When a decision is
closed - superseded, or settled and retained only as the rationale for a rule that
now lives in its canonical home elsewhere - move it verbatim, in that same change,
to an archive under `docs/history/` (for example `docs/history/decisions-archive.md`);
never summarize or drop wording, the exact text is the record. Keep a single
pointer to the archive at the top of this file, not a stub per entry. The archive
is the provenance log; this file is what is in force or still open.

## Decision lifecycle

A decision moves through these states:

- **Open** - a finding has been assessed but not yet acted on. It lives in the
  `## Open Decisions` queue below, with the verified evidence, the options, and a
  standing recommendation. The process is unchanged until it is adopted; an agent
  records it rather than implementing on the spot.
- **Active** - a decision that is in force now.
- **Adopted YYYY-MM-DD** - an Open finding that has been acted on: its rule now
  lives in its canonical home (a procedure, template, or invariant). Note where the
  rule landed; the finding is retained in place as the rationale that led to it,
  until it is archived.
- **Superseded** - replaced by a later decision; name the replacement.

When an entry becomes purely historical rationale - Adopted or Superseded, with the
live rule now owned elsewhere - archive it per the rule above: move it verbatim to
`docs/history/`, do not leave a stub.

## Decisions

### 2026-07-16 - Adopt AgentGovernanceBootstrap; retire foreign AGENTS.md

Status: Active

Decision:
This repository uses the AgentGovernanceBootstrap toolkit as agent governance.
Toolkit-owned files (`AGENTS.md`, harness shims, skills, playbooks, Claude
wrappers/hooks) are installed only via the toolkit refresh script (never
hand-edited). Brush-specific agent rules live in `.agents/repo-guidance.md`.
The former project `AGENTS.md` ("Agent Development Guide for brush") is
removed as part of the bootstrap legacy carve-out; its verified content is
migrated into repo-guidance. GitHub Copilot instructions at
`.github/copilot-instructions.md` keep their path (provider expects it) but
are banner-superseded so agents read `AGENTS.md` and
`.agents/repo-guidance.md` as authority.

Reason:
Refresh refused to replace a foreign `AGENTS.md` that never matched a
shipped toolkit hash. Partial refresh had already installed skills/playbooks
while the core constitution could not land. Bootstrap owns recovery,
including the two-commit carve-out.

Supersedes:
- Root `AGENTS.md` content role as brush agent development guide (file
  replaced by toolkit constitution after carve-out).
- Unbannered authority of `.github/copilot-instructions.md` for agent rules
  (retained as history with supersession banner).

## Open Decisions (deferred - not yet adopted)

Assessed findings the owner chose to record as a future decision rather than
implement now. The process is unchanged until one is adopted. Each states its
verified evidence, the options, and a standing recommendation. When one is adopted,
flip its status to `Adopted YYYY-MM-DD`, note where the rule now lives, and keep the
finding here as the rationale until it is archived.
