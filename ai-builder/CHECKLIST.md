# Flow Consistency Checklist

Use this checklist after any process update to ensure all pipeline artifacts stay aligned.

## 1) Stage and command parity

- [ ] Every active stage prompt in `ai-builder/system/prompts/` has a matching command in `.cursor/commands/`.
- [ ] Every command references the correct prompt file path.
- [ ] No command references deleted or renamed stages.

## 2) README alignment

- [ ] High-level flow matches active stages.
- [ ] Stage sections in README match current stage names and responsibilities.
- [ ] Source mapping in README matches current outputs.
- [ ] Daily execution runbook uses current command names.

## 3) Rules alignment

- [ ] `ai-builder/system/rules/kanban-workflow.md` uses current command contract.
- [ ] Status transitions match actual command behavior.
- [ ] `ai-builder/system/rules/spec-manifest.md` lists current source-of-truth artifacts only.
- [ ] No references to deprecated stages or outputs.

## 4) File and output contracts

- [ ] Each stage prompt declares required inputs and output paths.
- [ ] Output file names are consistent across prompt, command, and README.
- [ ] Runtime inputs are explicitly documented where required.

## 5) Deprecated references sweep

- [ ] No mentions of removed stage files.
- [ ] No mentions of old command names.
- [ ] No mentions of obsolete outputs.

Recommended search patterns:

- `Stage 9`, `9B`
- `task ship`
- old prompt/command names
- removed output file names

## 6) Templates and GitHub workflow

- [ ] Issue and PR templates reflect current lifecycle and validation expectations.
- [ ] Required fields in tickets match Stage 7/7B exports.
- [ ] Manual validation sections are present and usable.

## 7) Dry-run and safety

- [ ] Publish/readiness/execution stages support dry-run behavior.
- [ ] Write mode conditions are clearly documented.
- [ ] Single-ticket vs multi-ticket behavior is explicit.

## 8) Final quality check

- [ ] Run a final grep/ripgrep sweep for stale terms.
- [ ] Check lints/formatting for edited files.
- [ ] Validate one dry-run end-to-end sequence:
  - `7b-planning-export`
  - `7c-publish-milestone-to-github-project` (dry-run)
  - `7d-plan-ready` (dry-run)
  - `8-ai-execution` (dry-run with one `ticket_id`)
