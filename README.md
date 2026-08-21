# claude-plugins

The plugin catalog for [pedro-angel](https://github.com/pedro-angel)'s Claude Code plugins.

A marketplace is a **catalog**, not a container: this repository holds no plugin code. It lists
where each plugin lives and pins the exact commit to install.

## Use it

```bash
claude plugin marketplace add pedro-angel/claude-plugins
claude plugin install claude-agent-methodology@pedro-angel
```

Or declare it in a repository's `.claude/settings.json`, so anyone who trusts that project gets
it without a separate prompt:

```json
{
  "extraKnownMarketplaces": {
    "pedro-angel": { "source": { "source": "github", "repo": "pedro-angel/claude-plugins" } }
  },
  "enabledPlugins": { "claude-agent-methodology@pedro-angel": true }
}
```

## What it lists

| Plugin | Source | Pin |
| :--- | :--- | :--- |
| `claude-agent-methodology` | [pedro-angel/claude-agent-methodology](https://github.com/pedro-angel/claude-agent-methodology) | `v0.2.0` → `f11a2ce` |

## How the pin works

Every entry names both a `ref` and a `sha`, and when both are present **the `sha` is the
effective pin** — Claude Code fetches and checks out that commit directly. The tag is what keeps
the commit reachable; the sha is what makes a moved tag detectable instead of followed. That is
the tag-addressed, SHA-asserted consumption ADR-0023 requires, expressed in the catalog rather
than in a bespoke installer.

Bumping a plugin is therefore a reviewed edit of its `ref` and `sha` together, in a pull request
here — never a silent retag upstream.

## Adding a plugin

Add an entry to `.claude-plugin/marketplace.json` and validate before opening the PR:

```bash
claude plugin validate .
```
