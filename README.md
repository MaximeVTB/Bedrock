# Bedrock
Hey Obsidian, meet your older brother :)

## Web app

`index.html` is a single-file, backend-less Single-Page Application that turns this
repository into a private Obsidian-style Vault, hosted directly on GitHub Pages.

- No server, no build step: everything runs in the browser and talks to the GitHub API
  (via `@octokit/rest`) to read/write Markdown notes and attachments in this repo.
- Gated by a login overlay (username/password + a GitHub Personal Access Token), with
  the session optionally persisted in `localStorage`/`sessionStorage`.
- Obsidian-flavored live-preview Markdown engine: wikilinks, embeds, callouts, YAML
  frontmatter, highlights, tags, hidden `%% comments %%`, task checkboxes, Mermaid
  diagrams and KaTeX math.
- Drag & drop upload of images/PDF/Markdown straight to the repo, with automatic
  `![[file]]` embed insertion, and a 2s-debounced auto-sync (commit + push) indicator.
- Optional "Bedrock AI" side panel to analyze, summarize, rephrase, or extend notes,
  and to suggest `[[wikilinks]]` between existing notes (OpenAI / Anthropic / local
  endpoint, bring your own API key).

⚠️ Because this is a pure client-side app, the login gate and any stored API keys are
only a convenience/deterrent, not a real security boundary — anyone with the page
source and enough patience can bypass them. Only use this for personal/low-sensitivity
Vaults, and treat your GitHub PAT and AI API keys as visible to anyone able to inspect
the browser session.

To deploy: enable GitHub Pages on this repository (serving from the root of the
default branch) — `index.html` will be served as-is, no build required.
