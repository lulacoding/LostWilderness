# Implementation status (codebase vs Bible)

This document lists what is **implemented** in the Plugin codebase versus what appears in the Bible (Discord design) but is **not yet implemented**. Use it to see the gap between design and code. Code paths are under `Plugin/` (e.g. `common/`, `portals/`, `servers/survival/`, `servers/amplified/`).

**Legend:** ✅ Implemented · ❌ Not implemented · ⚠️ Partial / stub

---

## 1. Overview & Vision

| Item | Status | Notes |
| --- | --- | --- |
| Storyline (7 chapters, El Diablo, Devoiders, etc.) | ❌ | Design only; no storyline quest flow in code |
| Brotherhood / Epochians | ❌ | Lore only |
| 200% completion, Main Theme disc reward | ❌ | No advancement/disc reward logic |
| New Year / century titles, firework display | ❌ | Not in DayChangeListener or events |
| Calendar as internal clock | ✅ | CalendarSyncManager, DayChangeListener |
| Equator / seasons (Z-based) | ✅ | SeasonCalculator, Z > 500 / Z < -500 / equator |
| Placeable calendar item (1×1 block, book UI) | ❌ | Not in code |

---

## 2. Server infrastructure

| Item | Status | Notes |
| --- | --- | --- |
| Paper, BungeeCord, Velocity, VPS | ⚠️ | Infrastructure; plugin code assumes proxy/backend setup |
| Ubuntu, hardware, RAID, backup | ⚠️ | Ops; not in repo |
| MySQL (calendar, portals, clans) | ✅ | CalendarSyncManager, DatabaseManager, ClanManager use DB |
| HuskSync | ❌ | External plugin; not in repo |
| Discord bot (/link, /approve, roles) | ⚠️ | **/approve**, **/deny**, **/linkrequest** implemented (LinkApprovalService); bot/roles are external |
| Domains, launch | ⚠️ | Ops |

---

## 3. Plugins & modules

### Calendar

| Item | Status | Notes |
| --- | --- | --- |
| /date | ✅ | DateCommand |
| /time | ✅ | TimeCommand |
| /datejoined | ✅ | DateJoinedCommand |
| /season | ✅ | SeasonCommand |
| /resetcalendar | ✅ | Survival only; ResetCalendarCommand |
| /nextday | ⚠️ | Via **/lwdebug nextday** (admin), not standalone /nextday |
| /eoc (days since Epoch) | ❌ | No EOC command |
| /calender stats | ❌ | Not in code |
| Date format "1st January 1MC", Epoch (Day 0) | ✅ | DateCalculator, configurable format |
| MySQL sync (leader + polling 30–60s) | ✅ | CalendarSyncManager, SyncDayChangeListener |
| Config persistence, single-server | ✅ | CalendarServiceImpl, config.yml |
| Config folder auto-creation bug | ⚠️ | Workaround in Bible; code may still have issue |
| /timeset bug (resets calendar) | ⚠️ | Bible TODO; not verified in code |
| New day title (rare missing 1/7) | ⚠️ | Bible TODO |

### Portals

| Item | Status | Notes |
| --- | --- | --- |
| Crying Obsidian frame, fire, 1:1 coords | ✅ | PortalListener, TeleportListener, portal logic |
| 5 pairs per player, minimum spacing | ✅ | Config-driven (portal limit) |
| Air pocket when frame encased | ✅ | Portal creation logic |
| SurvivalPortalPlugin / AmplifiedPortalPlugin | ⚠️ | Single `portals` module; Survival/Amplified backends use same common + portals |
| Bungee Messenger | ✅ | Used for cross-server teleport |
| MySQL tables (portals, pending_portals) | ✅ | DatabaseManager, portal storage |
| /portals, /deleteportals | ✅ | PortalsCommand, DeletePortalsCommand |
| Entity passthrough (horses, Happy Ghasts) | ❌ | Bible TODO |

### LWEvents (Eclipse, Fog, Frost, Blizzard, Heatwave, etc.)

| Item | Status | Notes |
| --- | --- | --- |
| EclipseEvent | ✅ | EclipseEvent, chance + interval; sleep blocked |
| FogEvent | ✅ | FogEvent (ProtocolLib view distance); sleep blocked |
| BlizzardEvent | ✅ | BlizzardEvent, BlizzardMoveListener, Strays, freeze |
| FrostEvent | ✅ | FrostEvent, FrostMoveListener, cold biomes, heat sources |
| SummerHeatwaveEvent | ✅ | Husks, drying crops/farmland |
| ThunderEvent | ✅ | Thunderstorm, zombie horses on eclipse day |
| EasterWeekEvent | ✅ | Easter week titles (Gregorian Easter) |
| JungleMonsoonEvent | ✅ | In events impl |
| SeasonalStormEvent | ✅ | In events impl |
| SpringBloomEvent, AutumnLeafFallEvent | ✅ | In events impl |
| NaturalHordeSpawnerTask | ✅ | Horde spawner |
| Sleep blocking (eclipse, thunder, fog) | ✅ | SleepBlocker |
| /lwdebug (eclipse, fog, blizzard, frost, heatwave, easter) | ✅ | LWDebugCommand |

### Clans

| Item | Status | Notes |
| --- | --- | --- |
| /clan create, invite, accept, deny, leave | ✅ | ClanCommand |
| /clan color, promote, demote | ✅ | ClanCommand |
| /clan enemy, opposition | ✅ | ClanCommand |
| /clan info [name] | ✅ | ClanCommand |
| /clan list | ❌ | In help text but no handler; falls to "Unknown sub-command" |
| /clan reside | ❌ | Not in code |
| ClanManager, MySQL, BotApiClient (Discord) | ✅ | ClanManager, ClanDisplayListener |
| **Alliance** (create, invite, join, leave, info, list) | ❌ | AllianceCommand returns "not yet implemented" for all |
| /war declare, ceasefire, end | ❌ | No war commands |
| /nomad | ❌ | Not in code |
| Devoider/El Diablo kill counts (clan) | ⚠️ | BossKillRepository exists; clan integration TBD |

### RoofWither / boss

| Item | Status | Notes |
| --- | --- | --- |
| RoofWitherListener (Devoider / El Diablo) | ✅ | RoofWitherListener, 6 withers, 6 Devoiders, arena barriers |
| BossAbilityListener, BossDropListener | ✅ | In common |
| BossArena, ArenaManager, Boundary | ✅ | World/arena utils |
| ArenaBoundaryListener (restrict movement) | ✅ | Sandboxed arena |
| /arena-test, /diablo-lair | ✅ | ArenaTestCommand, DiabloLairCommand |

### Lobby / queue / resource pack

| Item | Status | Notes |
| --- | --- | --- |
| DefaultPackListener (force pack) | ✅ | DefaultPackListener |
| PackStatusListener | ✅ | PackStatusListener |
| VoidWorldGenerator, DeluxeMenus, queue plugin | ❌ | Not in Plugin repo (separate lobby server) |
| PackServer /packs/*.zip | ❌ | Not in code; config-driven pack URL |

### Other

| Item | Status | Notes |
| --- | --- | --- |
| LWHelpCommand, LWPluginsCommand, LWConfigCommand | ✅ | /lwhelp, /lwplugins, /lwconfig |
| Multichat, Clearlagg, Multiverse, Harbor | ❌ | External plugins |
| Geyser, Floodgate, BungeeGuard | ❌ | Infrastructure / external |
| Datapacks (build height, advancements) | ⚠️ | Not in Plugin repo; separate assets |
| Difficulty Hard | ⚠️ | Server config |

---

## 4. Resource packs & client assets

| Item | Status | Notes |
| --- | --- | --- |
| GeyserPackConverter, Bedrock manifest | ❌ | External tool / docs in Bible |
| Geyser config (resource-packs) | ❌ | Server config |
| Eclipse red moon pack (force during event) | ⚠️ | Events config; pack URL in config |
| Logo, 64×64 icon, Discord assets | ❌ | Art/design; not in repo |
| Vertical slabs | ❌ | Not in plugin code |

---

## 5. Worlds & gameplay design

| Item | Status | Notes |
| --- | --- | --- |
| Lobby (void, queue, chest GUI) | ❌ | Separate server; not in Plugin repo |
| Creative (plots, superflat) | ❌ | Not in Plugin repo |
| Survival (calendar, events, clans, portals) | ✅ | SurvivalMain registers all |
| Amplified (same, no /resetcalendar) | ✅ | AmplifiedMain |
| Devoid dimension, Galactic Journey, Leaving the Firmament | ❌ | Design only; no world/quest logic |
| War (declare, music, head drops, warzone radius) | ❌ | No /war or war system |
| Maps (updatable, transfer) | ❌ | Not in code |
| Hemisphere (Z), equator 500 | ✅ | SeasonCalculator |

---

## 6. Technical decisions

| Item | Status | Notes |
| --- | --- | --- |
| Calendar leader + polling | ✅ | CalendarSyncManager, SyncDayChangeListener |
| Portal 1:1 coords, no 8:1 | ✅ | Portal logic; Paper config separate |
| Plugin placement (backend only, Bungee messenger) | ✅ | Portals/calendar in Survival/Amplified |
| ROADMAP_MASTER.md, GitHub | ✅ | In Plugin/ |

---

## 7. Audio & visual

| Item | Status | Notes |
| --- | --- | --- |
| Lobby/warzone/eclipse music themes | ❌ | No in-game music triggers in plugin; resource pack / external |
| Custom discs (Get Lost, per dimension, 200%) | ❌ | No disc reward logic in code |
| Eclipse 5-act theme (audio) | ❌ | Design only |
| Logo, advertising assets | ❌ | Art/design |

---

## 8. Open questions / TODO (from Bible)

| Item | Status | Notes |
| --- | --- | --- |
| Calendar: config folder fix, /timeset fix, title fix | ⚠️ | Bible TODOs |
| Portal: entity passthrough | ❌ | Not implemented |
| Bedrock: /time /date namespace, lobby GUI fallback | ⚠️ | Geyser/Bedrock; not in plugin |
| Build height, lobby datapack 77 | ❌ | Datapack / other repo |
| Vulcan, Clearlagg verify | ❌ | External |
| Release, future ideas (wind, tides, Thirst) | ❌ | Design / future |

---

## Documentation (this Docs folder)

- **Player guide:** [player/README.md](player/README.md) — Home, Calendar & Time, Events, Survival, Amplified, Clans, Portals, Link Approval, Common, Calendar Plugin.
- **Development:** [development/dev-guide.md](development/dev-guide.md) — Command framework, BaseCommand, CommandService, EnhancedServiceRegistry, world/arena utilities, plugin-to-plugin communication, best practices.
- **Design (Bible):** [design/README.md](design/README.md) — Full architecture and design from Discord.
