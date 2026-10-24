# johantor plugins

The `johantor` [Claude Code](https://code.claude.com/docs/en/overview) plugin marketplace. This
repository holds only the catalog (`.claude-plugin/marketplace.json`); each plugin lives in its
own repository.

```bash
claude plugin marketplace add johantor/plugins
claude plugin install crew@johantor
claude plugin install board@johantor
```

You can also install from the UI: run `/plugin` in Claude Code and browse to **Discover**.

Site: <https://johantor.github.io/plugins/>

| Plugin | What it does | Repository |
|---|---|---|
| `crew` | A `lead` agent plans the work and delegates each step to specialists, behind hook-enforced guardrails and one review gate. | [johantor/crew](https://github.com/johantor/crew) |
| `board` | A local kanban board of every Claude Code session: what needs you, what is running, what you closed today. | [johantor/board](https://github.com/johantor/board) |

## Updating and uninstalling

```bash
claude plugin marketplace update johantor    # refresh the catalog
claude plugin update crew@johantor           # update a plugin
claude plugin uninstall crew@johantor        # remove it
```

## Moving from `johantor/crew`

The marketplace used to live in `johantor/crew`. That source is gone. The marketplace name and
the install ids are the same, so only the source changes. Removing a marketplace uninstalls its
plugins, so install the ones you use again:

```bash
claude plugin marketplace remove johantor
claude plugin marketplace add johantor/plugins
claude plugin install crew@johantor   # and board@johantor
```

## Maintaining

Each plugin lives in the `plugin/` folder of its repository, and the entries install that folder
only (`git-subdir`), so a repo's site and tooling never reach users.

A plugin entry's `name` and `description` copy the plugin's own `plugin.json`, which is
canonical. CI (`validate.yml`) fetches each `plugin.json` from its repository and fails on a
mismatch, so update the entry here when a plugin changes its description.

The site is `docs/`, served by GitHub Pages from `main`. `docs/style.css` is a copy of the crew
site's stylesheet (`johantor/crew`, `docs/style.css`), so keep the two in step; marketplace-only
styles live in `docs/plugins.css`.

## License

[Apache-2.0](LICENSE). The plugins collect no data and send nothing to the maintainers. An
independent project, not affiliated with or endorsed by Optimizely or Anthropic.
