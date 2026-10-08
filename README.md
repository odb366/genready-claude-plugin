# GenReady for Claude Code

Make your website readable and citable by AI search engines (ChatGPT, Perplexity, Google AI Overviews) and usable by AI agents, without leaving Claude Code.

The plugin adds two things:

- **The GenReady MCP server** (`https://genready.ai/mcp`): scan pages and sites, read findings, get ready-to-commit files, and verify fixes against the live site.
- **The `genready-fix-loop` skill**: tells Claude how to run scan → fix → deploy → verify, what it may change on its own, and what it must leave to you.

## Install

1. Create an API key at <https://genready.ai/api-keys>. For site-wide work, enable **Read site data** on the key.
2. Make the key available to Claude Code:

   ```bash
   export GENREADY_API_KEY=gr_live_...
   ```

   Put the line in your shell profile so it is set every time.
3. In Claude Code, add the marketplace and install the plugin:

   ```
   /plugin marketplace add odb366/genready-claude-plugin
   /plugin install genready@genready
   ```

4. Restart Claude Code. Run `/mcp` and check that `genready` is connected.

## Use

Open your site's repository and say what you want:

> Make my site AI-ready.

> Check why ChatGPT can't read our docs, and fix it.

Claude scans the live site once, fixes what has one right answer (robots.txt, llms.txt, structured data, meta directives, headings, alt text), asks you to deploy, and then verifies each fix against the live site. Writing changes and anything outside the repository are proposed, not applied.

## Cost

| Call | Cost |
| --- | --- |
| `analyze_website` | One API credit |
| `start_site_analysis` | API credits per page, Pro and Agency |
| `get_findings`, `get_artifact`, `get_fix_plan`, `list_domains`, `verify_findings` | Free |

Free accounts get 25 API credits a month. See <https://genready.ai/pricing>.

## Without the plugin

```bash
claude mcp add --transport http genready https://genready.ai/mcp \
  --header "Authorization: Bearer gr_live_your_key_here"
```

Docs: <https://genready.ai/docs/mcp>

## License

MIT
