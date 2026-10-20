# GenReady for Claude

Make your website readable and citable by AI search engines (ChatGPT, Perplexity, Google AI Overviews, Claude) and usable by AI agents. Scan it, fix what the scan finds in your repo, and check on the live site that the fixes worked.

GenReady looks at crawler access, `robots.txt`, `llms.txt`, structured data, content, and agent standards such as MCP. This plugin connects Claude to GenReady and teaches Claude the workflow.

## What is in it

| Piece                      | What it does                                                                                                                                              |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Skill `genready-fix-loop`  | Scans a URL, applies the safe fixes in your repo, asks you to deploy, then verifies each fix on the live site. Judgement calls are proposed, not applied. |
| Skill `audit-ai-readiness` | Reports scores and the top fixes. It never edits files.                                                                                                   |
| Skill `scan-whole-site`    | Scans a whole site and reads the ranked fix plan. It asks before it spends credits.                                                                       |
| Commands                   | `/genready:fix`, `/genready:scan`, `/genready:site`                                                                                                       |
| Connector                  | The GenReady MCP server at `https://genready.ai/mcp`                                                                                                      |

## Install

In the Claude app, add GenReady from the plugin directory. Then connect the GenReady connector and sign in to your GenReady account. A free account is enough to start.

In Claude Code:

```
/plugin marketplace add odb366/genready-claude-plugin
/plugin install genready@genready
```

Then run `/mcp`, choose `genready`, and select Authenticate. A browser window opens. Sign in to GenReady and approve the access. No API key is needed.

## Use

Open your site's repository and say what you want:

> Make my site AI-ready.

> Scan https://example.com and fix what you can in this repo.

Claude scans the live site once, fixes what has one right answer (robots.txt, llms.txt, structured data, meta directives, headings, alt text), asks you to deploy, then verifies each fix on the live site. Writing changes and anything outside the repository are proposed, not applied.

## Credits and plans

| Call                                                                              | Cost                                                                                           |
| --------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| `analyze_website`                                                                 | One credit per page scan                                                                       |
| `start_site_analysis`                                                             | One credit per page. A run started from Claude scans at most 25 pages unless you ask for more. |
| `get_findings`, `get_artifact`, `get_fix_plan`, `list_domains`, `verify_findings` | Free to call                                                                                   |

Re-checking fixes with `verify_findings` is part of the Pro and Agency plans. Free accounts get a monthly credit allowance. Plans and limits: https://genready.ai/pricing.

## Data

The plugin sends the URLs you ask Claude to scan, and your decisions about findings, to your GenReady account at genready.ai. GenReady fetches the public pages at those URLs. The plugin stores nothing itself and sends no repository files. Claude reads your files locally to apply fixes. The connector signs in through OAuth, and the plugin holds no API key. Privacy policy: https://genready.ai/privacy.

## Without the plugin

Any MCP client can connect to the same server with an API key from https://genready.ai/api-keys:

```bash
claude mcp add --transport http genready https://genready.ai/mcp \
  --header "Authorization: Bearer gr_live_your_key_here"
```

## Links

- Docs: https://genready.ai/docs/mcp
- Support: https://genready.ai/support
- Issues: https://github.com/odb366/genready-claude-plugin/issues
- MCP server for stdio clients: https://github.com/odb366/genready-mcp-server

## License

MIT
