You configure **`docs/engineering/GITHUB_PROJECT.md`** for this repository from a **GitHub Project (v2) URL** the user supplies, then remove the template example so delivery commands target the real board.

For any narrative text you add, use the language settings in `ai-builder/pipeline.config.json` (`GENERATED_DOCS_LANGUAGE`, `IMPLEMENTATION_CODE_LANGUAGE`) per `ai-builder/system/rules/language-conventions.md`.

**Input (required):** The full browser URL of the GitHub Project, for example:

- Organization: `https://github.com/orgs/acme-corp/projects/3`
- User: `https://github.com/users/octocat/projects/1`

If the user runs the slash command without pasting a URL, **ask once** for it and stop until they provide it.

---

## Steps

1. **Parse the URL** (trim whitespace; strip query string and fragment):
   - Organization projects: path pattern `/orgs/<owner>/projects/<project_number>`
   - User projects: path pattern `/users/<owner>/projects/<project_number>`
   - `<owner>` is the GitHub login or org slug; `<project_number>` is a positive integer.
   - If the URL does not match either pattern, **do not** guess. Explain the expected formats and ask for a correct link.

2. **Optional verification** (when `gh` is available and the user’s environment is this repo): run  
   `gh project view <project_number> --owner <owner>`  
   If it fails with auth errors, note that `gh auth refresh -s project` may be needed; still write `GITHUB_PROJECT.md` if parsing succeeded unless the user asked to abort on verification failure.

3. **Write** `docs/engineering/GITHUB_PROJECT.md` with:
   - Valid YAML frontmatter between `---` lines:
     - `owner:` — parsed owner slug (string)
     - `project_number:` — parsed integer
   - A short markdown body **below** the frontmatter for humans (commands only read frontmatter). Include:
     - The **source URL** the user provided (for traceability).
     - The verification snippet:

```bash
gh project view <project_number> --owner <owner>
gh project field-list <project_number> --owner <owner>
```

     - A one-line reminder: for a **public** repo, avoid committing internal org pins if that is a concern; otherwise committing this file is recommended so delivery commands share the same project.

4. **Delete** `docs/engineering/GITHUB_PROJECT.example.md` if it exists (template copy in this repo; after this command the real config file replaces it).

5. **Do not** remove or overwrite unrelated files. If `GITHUB_PROJECT.md` already exists, replace it only after the new URL parses successfully (or confirm with the user if they might lose hand-edited body text).

---

## Consistency

- Match the frontmatter contract used by **`/import-ai-task-doc-to-github-project`** and other delivery commands: exactly the keys **`owner`** and **`project_number`** in the first YAML document.

## Output

Briefly confirm: path written, owner and project number, whether the example file was deleted, and whether `gh project view` succeeded or was skipped.
