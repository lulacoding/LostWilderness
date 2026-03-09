# Lobby and queue

**Implementation:** VoidWorldGenerator, DeluxeMenus, custom queue plugin, and PackServer are **not** in the Plugin repo (separate lobby server). **DefaultPackListener** and **PackStatusListener** are implemented in the codebase.

## Lobby server

- **Void/empty** world (End-style void); **VoidWorldGenerator**.
- **Spectator** mode; **chest GUI menus** (e.g. **DeluxeMenus**); **port 25568**.
- **Link Discord**, **clan/ally list**, **queue** (custom queue plugin using **Discord + MySQL**).
- **Accept resource pack** before **Play**; **client check** (Vulcan/Negativity).
- **Play** = go to **Survival** or **“where you left off.”**
- **Bedrock:** If chest GUI fails, **CLI lobby** or tour fallback.
- **Staff priority** on queue (login doesn’t count toward cap).
- **Creative-while-queued** option.

## PackServer and DefaultPackListener

- **PackServer** serves packs from **/packs/*.zip** (or similar path).
- **DefaultPackListener** (in codebase) applies the default/Lost Wilderness pack; **Floodgate bypass** if Bedrock pack fails.

## Creative server

- **10 public plots** (monthly wipe), **private/clan/alliance** plots (yearly, max 2 years); **superflat**, **peaceful**, no day/night, **1M×1M**; must go via Lobby; **inventory swap + Vulcan check** on Survival load; **command blocks disabled**.
- **Hard border** between Lost Wilderness worlds and Creative.

## Lobby datapack (1.21.6)

- **Datapack ver 77** (1.21.6): **terms & conditions**, **cutscene box**, **custom menus**; lobby code waiting on 1.21.6.

## Source

- Bible sections 3 and 5: VoidWorldGenerator, DeluxeMenus, queue plugin, PackServer, DefaultPackListener, Creative rules, staff priority, datapack 77.
