# Lost Wilderness — Server and Plugin Architecture Bible

Full documentation set for the Lost Wilderness Minecraft server: design and architecture from Discord (channels and DMs), expanded with config, SQL, and reasoning. Use the links below to reach each section.

---

## Implementation Status (Code vs Design)

**[→ Implementation status](../implementation-status.md)** — Lists what is **implemented** in the Plugin codebase versus **not yet implemented** (or partial). Use it to see the gap between Bible design and actual code.

---

## Other Docs (This Folder)

- **Player guide:** [../player/README.md](../player/README.md) — Home, Calendar & Time, Events, Survival, Amplified, Clans, Portals, Link Approval, Common, Calendar Plugin.
- **Development:** [../development/dev-guide.md](../development/dev-guide.md) — Command framework, BaseCommand, CommandService, EnhancedServiceRegistry, world/arena utilities, best practices.

This **design** section is the architecture source (from Discord). The **player** and **development** sections are the in-game and developer reference.

---

## How to Use This Bible

- **Main index:** You are here. Each section links to a folder with an `README.md` index and subpages.
- **Source data:** The content comes from `Notes/extracted/` (plain-text Discord exports) and the original HTML in `Notes/`. Quotes in the pages are from those sources.
- **Detail level:** Pages go into more detail than the original messages: config snippets, SQL, commands, reasoning, and external links are included where discussed.
- **Implemented vs not:** Items marked **[Not implemented]** or **[Partial]** in the Bible pages are summarised in [../implementation-status.md](../implementation-status.md).

---

## 1. [Overview & Vision](01-overview/README.md)

High-level concept, storyline, Brotherhood, goals, and completion targets.

- [Vision and concept](01-overview/vision-and-concept.md)
- [Storyline (7 chapters, Lord / Redeemer / El Diablo)](01-overview/storyline.md)
- [Brotherhood and Epochians](01-overview/brotherhood.md)
- [Goals and 200% completion](01-overview/goals-and-completion.md)

---

## 2. [Server infrastructure](02-infrastructure/README.md)

Platform, proxy, hardware, worlds, sync, Discord bot, domains.

- [Platform and versions (Paper, 1.21.x)](02-infrastructure/platform-and-versions.md)
- [Proxy and VPS (BungeeCord, Velocity, TCPShield)](02-infrastructure/proxy-and-vps.md)
- [Hardware and storage (Ubuntu, RAID, backup)](02-infrastructure/hardware-and-storage.md)
- [Worlds and seeds (Multiverse, build height)](02-infrastructure/worlds-and-seeds.md)
- [Sync and data (MySQL, HuskSync, Vulcan)](02-infrastructure/sync-and-data.md)
- [Discord bot (link, approve, roles, whitelist)](02-infrastructure/discord-bot.md)
- [Domains and launch](02-infrastructure/domains-and-launch.md)

---

## 3. [Plugins & modules](03-plugins/README.md)

Calendar, portals, LWEvents, Eclipse, clans, lobby, anticheat, and other plugins.

- [Calendar (commands, MySQL sync, date format)](03-plugins/calendar.md)
- [Portals (Custom Portal API, Survival/Amplified plugins)](03-plugins/portals.md)
- [LWEvents and Eclipse (Fog, Frost, Blizzard, Blood Moon)](03-plugins/lwevents-and-eclipse.md)
- [Clans and war (commands, alliances, nomad)](03-plugins/clans-and-war.md)
- [Lobby and queue (VoidWorldGenerator, DeluxeMenus)](03-plugins/lobby-and-queue.md)
- [Anticheat (Vulcan, Negativity, BungeeGuard)](03-plugins/anticheat.md)
- [Other plugins (Multichat, Clearlagg, datapacks)](03-plugins/other-plugins.md)

---

## 4. [Resource packs & client assets](04-resource-packs/README.md)

Java → Bedrock conversion, serving packs, seasonal/eclipse packs, logo and assets.

- [Java to Bedrock (GeyserPackConverter, formats)](04-resource-packs/java-to-bedrock.md)
- [Serving packs (Geyser config, Floodgate)](04-resource-packs/serving-packs.md)
- [Seasonal and eclipse packs](04-resource-packs/seasonal-and-eclipse-packs.md)
- [Logo and advertising assets](04-resource-packs/logo-and-assets.md)

---

## 5. [Worlds & gameplay design](05-worlds-gameplay/README.md)

Lobby, Creative, Survival, Amplified, Devoid, Galactic Journey, storyline, seasons, war.

- [Lobby and Creative](05-worlds-gameplay/lobby-and-creative.md)
- [Survival (main overworld)](05-worlds-gameplay/survival.md)
- [Amplified (portal, Brotherhood, southern hemisphere)](05-worlds-gameplay/amplified.md)
- [Devoid and El Diablo’s Lair](05-worlds-gameplay/devoid-and-diablo.md)
- [Galactic Journey (Starport, planets)](05-worlds-gameplay/galactic-journey.md)
- [Storyline progression (Devoiders, El Diablo, Leaving the Firmament)](05-worlds-gameplay/storyline-progression.md)
- [Seasons and hemisphere](05-worlds-gameplay/seasons-and-hemisphere.md)
- [War and PvP (declared war vs raids, head drops)](05-worlds-gameplay/war-and-pvp.md)

---

## 6. [Technical decisions & conventions](06-technical-decisions/README.md)

Calendar sync, portal design, plugin placement, roadmap.

- [Calendar sync (leader, polling, MySQL)](06-technical-decisions/calendar-sync.md)
- [Portal design (1:1 coords, no 8:1 linking)](06-technical-decisions/portal-design.md)
- [Plugin placement (backend vs BungeeCord)](06-technical-decisions/plugin-placement.md)
- [Roadmap and codebase (GitHub, ROADMAP_MASTER)](06-technical-decisions/roadmap.md)

---

## 7. [Audio & visual design](07-audio-visual/README.md)

Music themes, custom discs, eclipse theme, logo, advertising.

- [Lobby and warzone music](07-audio-visual/lobby-and-warzone-music.md)
- [Eclipse theme (5 acts)](07-audio-visual/eclipse-theme.md)
- [Custom discs (per dimension, advancements)](07-audio-visual/custom-discs.md)
- [Biome and event music (Frost, Blizzard, Heatwave, Diablo)](07-audio-visual/biome-and-event-music.md)
- [Logo and advertising](07-audio-visual/logo-and-advertising.md)

---

## 8. [Open questions & TODO](08-open-questions/README.md)

Unresolved items from chat: calendar bugs, portal entities, Bedrock testing, build height, release timing, future ideas.

- [Calendar and portal TODOs](08-open-questions/calendar-and-portal-todos.md)
- [Cross-platform and Bedrock](08-open-questions/cross-platform-and-bedrock.md)
- [Build height, lobby, cosmetics](08-open-questions/build-height-lobby-cosmetics.md)
- [Release and future ideas](08-open-questions/release-and-future-ideas.md)

---

*Generated from Discord exports. Source: Direct Messages (Grovyle187), Lost Wilderness server channels (Audio Design, Graphical Design, Storyline, Custom Discs, Development).*
