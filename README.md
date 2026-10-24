# johantor plugins

The `johantor` [Claude Code](https://code.claude.com/docs/en/overview) plugin marketplace. This
repository holds only the catalog (`.claude-plugin/marketplace.json`); each plugin lives in its
own repository.

```bash
claude plugin marketplace add johantor/plugins
claude plugin install crew@johantor
claude plugin install board@johantor
```

| Plugin | What it does | Repository |
|---|---|---|
| `crew` | A `lead` agent plans the work and delegates each step to specialists, behind hook-enforced guardrails and one review gate. | [johantor/crew](https://github.com/johantor/crew) |
| `board` | A local kanban board of every Claude Code session: what needs you, what is running, what you closed today. | [johantor/board](https://github.com/johantor/board) |

## Moving from `johantor/crew`

The marketplace used to live in `johantor/crew`. The marketplace name and the install ids are
the same, so only the source changes. Removing a marketplace uninstalls its plugins, so
install the ones you use again:

```bash
claude plugin marketplace remove johantor
claude plugin marketplace add johantor/plugins
claude plugin install crew@johantor   # and board@johantor
```

`johantor/crew` keeps a copy of the catalog for now, so the old source still works.

## Maintaining

Each plugin lives in the `plugin/` folder of its repository, and the entries install that folder
only (`git-subdir`), so a repo's site and tooling never reach users.

A plugin entry's `name` and `description` copy the plugin's own `plugin.json`, which is
canonical. CI (`validate.yml`) fetches each `plugin.json` from its repository and fails on a
mismatch, so update the entry here when a plugin changes its description.
