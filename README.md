# Lost Wilderness — Centralised Documentation

All project documentation lives in **`Docs/`**: design, player guides, development, and implementation status.

---

## Quick Links

| Section | Description |
| --- | --- |
| **[Implementation status](implementation-status.md)** | What is implemented in code vs not (Bible vs Plugin codebase). |
| **[Design (Bible)](design/README.md)** | Server & plugin architecture from Discord: overview, infrastructure, plugins, resource packs, worlds, technical decisions, audio/visual, open questions. |
| **[Player guide](player/README.md)** | In-game handbook: Home, Calendar & Time, Events, Survival, Amplified, Clans, Portals, Link Approval, Common. |
| **[Development](development/dev-guide.md)** | Plugin development: command framework, services, world/arena utilities, best practices. |
| **[Style guide](style-guide.md)** | How all docs are formatted (headings, tables, links, sections). |

---

## Structure

```
Docs/
├── README.md                 ← You are here
├── implementation-status.md  ← Code vs design (what’s built, what’s not)
├── design/                  ← Bible: architecture & design (from Discord)
│   ├── 01-overview/
│   ├── 02-infrastructure/
│   ├── 03-plugins/
│   ├── 04-resource-packs/
│   ├── 05-worlds-gameplay/
│   ├── 06-technical-decisions/
│   ├── 07-audio-visual/
│   └── 08-open-questions/
├── player/                  ← Player-facing wiki (Plugin/docs)
│   ├── home.md
│   ├── calendar-and-time.md
│   ├── events.md
│   ├── survival.md
│   ├── amplified.md
│   ├── clans.md
│   ├── portals.md
│   └── ...
└── development/             ← Developer guide (Plugin/dev_guide)
    ├── dev-guide.md
    └── ...
```

---

## Source

- **Design:** Discord exports (channels + DMs), expanded into the Bible in `design/`.
- **Player:** Plugin wiki (how to play, commands, features).
- **Development:** Plugin dev guide (how to extend and maintain the codebase).

All docs in `Docs/` follow a single style. See [style-guide.md](style-guide.md) for formatting rules. When adding or editing pages, apply that guide so the docs stay consistent.

*Last consolidated: March 2026*
