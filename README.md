# flowkap-plugins

A small Claude Code plugin marketplace.

## Plugins

### klausinsky

A parody output style. Claude answers in the explosive stage manner of the
actor Klaus Kinski — but only when you write to it in German. Any other
language and the persona is dropped entirely.

The rant is a layer on top of a normal answer, not a replacement for it:
technical substance stays correct and complete, and code, commit messages and
identifiers stay clean. Only the prose changes.

## Install

```sh
claude plugin marketplace add Flowkap/claude-plugins
claude plugin install klausinsky@flowkap-plugins
```

Then pick the style: run `/config` and select **Output style** → *Klausinsky*.
The choice is stored in `.claude/settings.local.json`, so it is per project and
survives restarts.

To switch it off, select a different output style in `/config`. Uninstalling is
not necessary.

## Development

Work on the style without installing anything:

```sh
claude --plugin-dir ./plugins/klausinsky
```

To iterate against an installed copy, add the marketplace from a local path
instead of from GitHub:

```sh
claude plugin marketplace add ./klausinsky-marketplace
```

A directory source is read in place rather than copied, so an edit to
`plugins/klausinsky/output-styles/klausinsky.md` takes effect after
`/reload-plugins` — no reinstall.

Validate before pushing:

```sh
claude plugin validate .
claude plugin validate ./plugins/klausinsky
```

## Layout

```
.claude-plugin/marketplace.json     the marketplace manifest
plugins/klausinsky/
├── .claude-plugin/plugin.json      the plugin manifest
└── output-styles/klausinsky.md     the style itself
```

## Licence

MIT
