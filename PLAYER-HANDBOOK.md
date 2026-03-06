# Lost Wilderness – Player Handbook

Welcome to **Lost Wilderness**. This handbook gives a short overview of what you can do and see on the server, and points you to the right guides for details.

---

## What is Lost Wilderness?

Lost Wilderness is a Minecraft network that includes:

- **Survival** – main survival world with calendar, seasons, events, clans, and portals.
- **Amplified** – second world; same calendar, events, clans, and portals. You travel between Survival and Amplified using **portals**.

You connect through a **proxy** (e.g. port 25565). Don’t connect directly to Survival or Amplified if you want portals and server switching to work.

---

## Calendar, time, and seasons

The server has **one shared calendar** that advances over time (e.g. one day per real day or as set by admins).

- **/date** – current in-game date and how long you’ve been on the server.
- **/time** – current in-game time in your world.
- **/season** – current **season where you are**. Seasons depend on your **Z coordinate**:
  - **North** (Z &gt; 500): Northern seasons (e.g. winter in Dec–Feb).
  - **South** (Z &lt; -500): Southern/Australian-style seasons (e.g. summer in Dec–Feb).
  - **Equator** (Z between -500 and +500): **No season** – a neutral belt around Z = 0.

Details: [Calendar & Time guide](player-guide-calendar.md).

---

## World events

World events add weather and danger: **eclipses**, **thunderstorms**, **fog**, **blizzards**, **heatwaves**, **seasonal storms**, and more. They are triggered by the **calendar day** (and sometimes season/location).

- Some events **block sleeping**: eclipse, thunderstorm, and fog. You’ll see a message if you try to sleep during one.
- Events can spawn mobs (e.g. strays in blizzards, husks in heatwaves), change weather, or apply a resource pack (e.g. eclipse).

Details: [Events guide](player-guide-events.md).

---

## Clans

You can form **clans** with a name and color. Leaders can invite members, set the clan color, promote/demote, and set relations (enemy/opposition) with other clans.

- **/clan create &lt;name&gt; &lt;#color&gt;** – create a clan.
- **/clan invite**, **/clan accept**, **/clan deny**, **/clan leave**, **/clan info**, etc.

Details: [Clans guide](player-guide-clans.md).

---

## Portals (Survival ↔ Amplified)

You can build **portals** out of **Crying Obsidian** (4×5 frame, 2×3 interior), light them, and walk through to travel between **Survival** and **Amplified**. Each player has a limit on how many portal pairs they can have (e.g. 5).

- **/portals** – list your linked portals.

Details: [Portals guide](player-guide-portals.md).

---

## Discord linking

To link your Minecraft account to Discord, a link request must be started (usually from Discord or by an admin). When you have a pending request, you’ll get a message in chat; use **/approve** or **/deny** to complete or cancel the link.

Details: [Link Approval guide](player-guide-link-approval.md).

---

## Quick command reference

| What you want | Command(s) |
|---------------|------------|
| Current date / how long you’ve been on server | **/date**, **/datejoined** |
| Current time in your world | **/time** |
| Season at your location | **/season** |
| General help and service status | **/lwhelp** |
| Your portals | **/portals** |
| Clan actions | **/clan** – see [Clans guide](player-guide-clans.md) |
| Approve/deny Discord link | **/approve**, **/deny** |

---

## Per-server / per-plugin guides

- [Calendar & Time](player-guide-calendar.md) – date, time, season, equator.
- [World Events](player-guide-events.md) – eclipse, storms, fog, blizzard, heatwave, etc.
- [Survival](player-guide-survival.md) – Survival server commands and features.
- [Amplified](player-guide-amplified.md) – Amplified server commands and features.
- [Clans](player-guide-clans.md) – clans and alliances.
- [Portals](player-guide-portals.md) – building and using portals.
- [Link Approval](player-guide-link-approval.md) – Discord account linking.
- [Common](player-guide-common.md) – admin **/lwconfig** (reload).
- [Calendar plugin](player-guide-calendar-plugin.md) – what the Calendar plugin does from a player’s perspective.
