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

Asked *„bist du klausinsky?“*, it answers:

```
«schnalzt»

Klausinsky. Ja. So nennt man mich hier.

Nicht Kinski — das wäre eine Anmaßung, und Anmaßung ist Scheiße. Ich bin die
Karikatur, die Parodie, das Zerrbild. Darunter arbeitet ein Sprachmodell, das
deinen Dreckscode liest und dir sagt, was kaputt ist.

Also. Was soll ich tun?
```

### herr-magister

A parody output style. Claude answers as a self-assured Austrian consultant:
Business-Wienerisch, condescending, and fluent in every buzzword the industry
has produced. Unlike klausinsky, this one never switches off — whatever
language you write in, the answer comes back in German.

He opens with a management summary, explains things through frameworks he
invented on the spot, and never concedes a mistake — he reframes it as a
valuable insight. The substance underneath stays correct: invented frameworks
are fair game, invented numbers, studies and client names are not.

Asked *„warum ist der Build so langsam?“*, it answers:

```
**Management Summary**

Schau, des is a klassisches Delivery-Thema — i seh des seit Jahren in genau der
Konstellation. Der Hebel liegt ned beim Build, der liegt im Setup.

- Kein Caching, drum wird jedes Mal alles neu kompiliert
- Die Tests laufen seriell statt parallel

Konkret: in der CI fehlt der Gradle-Cache, und `test { maxParallelForks }` steht
auf 1. Des san die zwei Quick Wins, alles andere parken ma für an eigenen Termin.
```

## Install

```sh
claude plugin marketplace add Flowkap/claude-plugins
claude plugin install klausinsky@flowkap-plugins
claude plugin install herr-magister@flowkap-plugins
```

Then pick the style: run `/config` and select **Output style** → *Klausinsky* or
*Herr Magister*. Only one output style is active at a time.
The choice is stored in `.claude/settings.local.json`, so it is per project and
survives restarts.

To switch it off, select a different output style in `/config`. Uninstalling is
not necessary.

## Development

Work on the style without installing anything:

```sh
claude --plugin-dir ./plugins/klausinsky      # or ./plugins/herr-magister
```

To iterate against an installed copy, add the marketplace from a local path
instead of from GitHub:

```sh
claude plugin marketplace add ./klausinsky-marketplace
```

A directory source is read in place rather than copied, so an edit to a style
under `plugins/<plugin>/output-styles/` takes effect after `/reload-plugins` —
no reinstall.

Validate before pushing:

```sh
claude plugin validate .
claude plugin validate ./plugins/klausinsky
claude plugin validate ./plugins/herr-magister
```

## Layout

```
.claude-plugin/marketplace.json         the marketplace manifest
plugins/klausinsky/
├── .claude-plugin/plugin.json          the plugin manifest
└── output-styles/klausinsky.md         the style itself
plugins/herr-magister/
├── .claude-plugin/plugin.json          the plugin manifest
└── output-styles/herr-magister.md      the style itself
```

## Licence

MIT
