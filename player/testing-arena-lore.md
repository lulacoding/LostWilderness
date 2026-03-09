# Testing: Arena Lore (Devoider / Diablo)

Full instructions to test kill tracking, spawn eligibility, server binding, drops, hordes, blue skull bedrock, and Diablo's Lair.

**Requirements:** Paper 1.21.x, Java 21, MySQL/MariaDB (same database for Survival and Amplified so kill counts are shared). You need **two server types** for full testing: **Survival** (Devoider only) and **Amplified** (Diablo only). You can run one server at a time and point it at the same DB.

---

## 1. Prerequisites

### 1.1 Database

- Use the same MySQL database for both Survival and Amplified (see [INSTALL_AND_RUN.md](INSTALL_AND_RUN.md) for setup).
- The plugin creates `boss_kills` and `clan_boss_kills` on first run. Ensure `config.yml` has the correct `mysql` section on both servers.

### 1.2 Permissions

- **`lw.admin.arena`** (default: op) — for `/arena-test` and `/diablo-lair`.
- Normal players do not need this for killing bosses; they only need it to generate arenas or run test commands.

### 1.3 Nether roof (Y=127)

- **Devoider** (Survival) and **Diablo** (Amplified) only trigger when a **Wither is spawned at Y=127 in the Nether** (the roof).
- Build the Wither spawn structure (soul sand T + 3 Wither Skeleton skulls) with the **center of the Wither** at **Y=127** (the block layer where the Wither appears).
- If you build at Y=126 or Y=128, the plugin will not transform the Wither.

---

## 2. Kill tracking (player and clan)

### 2.1 What gets recorded

- **Normal Wither** (no metadata): killer’s `wither_kills` +1; every clan that has **at least one member within 64 blocks** of the death gets `wither_kills` +1 (once per clan per death).
- **Devoider** (metadata `devoider`): killer’s `devoider_kills` +1; same “present” rule for clans (64 blocks, 1 per clan).
- **Diablo**: no kill count is recorded (plan: optional; current implementation does not increment).

### 2.2 Testing normal Wither kills (for Devoider eligibility)

1. **Survival server:** Go to the **Overworld** (or any dimension) and spawn a normal Wither (e.g. with soul sand + 3 skulls **not** at Nether Y=127, or use a spawn egg / command if allowed).
2. Kill it. The player who gets the killing blow gets `wither_kills` +1.
3. Have **another player from the same clan** stand within **64 blocks** of the Wither when it dies. That clan should get `clan_boss_kills.wither_kills` +1 (once, even if 5 clan members are present).
4. Repeat until you have **6 wither kills** (player or clan). You can check the DB (see **Section 8**).

### 2.3 Testing Devoider kills (for Diablo eligibility)

1. **Survival server:** After you have 6 wither kills, go to the **Nether roof** and build a Wither at **Y=127** (see Section 3). It should become **Devoider**.
2. Kill the Devoider. Killer gets `devoider_kills` +1; clans with ≥1 member within 64 blocks get `devoider_kills` +1.
3. Repeat until you have **6 devoider kills** (player or clan). These counts are shared with Amplified via the same DB.

---

## 3. Spawn eligibility and server binding

### 3.1 Survival: Devoider only

1. Start the **Survival** server with the shared MySQL config.
2. **Before 6 wither kills:** Go to Nether, build the Wither structure at **Y=127** (roof). The Wither spawn should be **cancelled** (no Devoider, no normal Wither from that structure).
3. **After 6 wither kills:** Build the same structure at Nether Y=127 again. The Wither should spawn and **immediately become Devoider** (name “§cDevoider”, 300 HP, 10 Wither Skeletons spawn around players).

### 3.2 Amplified: Diablo only

1. Start the **Amplified** server with the **same** MySQL config.
2. **Before 6 devoider kills:** Build a Wither at Nether Y=127 on Amplified. The spawn should be **cancelled** (no Diablo, no Devoider).
3. **After 6 devoider kills** (earned on Survival): Build a Wither at Nether Y=127 on Amplified. It should become **El Diablo, Destroyer of Worlds** (600 HP, 10 Wither Skeletons).
4. **One Diablo at a time:** While that Diablo is alive, building another Wither at Y=127 on Amplified should be **cancelled**. After the Diablo dies, the next Y=127 Wither on Amplified can become Diablo again (if you still have 6 devoider kills).

### 3.3 Building the Wither at Y=127 or Y=128 (Nether roof)

- In the Nether, go to the **roof** (Y=127 or Y=128). Place:
  - Soul sand in a T (3 blocks horizontal, 1 block center below).
  - 3 Wither Skeleton skulls on top of the three horizontal soul sand blocks.
- The plugin treats **both Y=127 and Y=128** as Nether roof: if the Wither’s spawn location block Y is 127 or 128, it will be transformed (when eligibility is met). If you are at Y=128, the Wither may spawn at 128 and will now be recognised.

---

## 4. Drops

- **Devoider (Survival):** On death, **2 Nether Stars** and **2× normal Wither XP**. No other drops from the plugin.
- **Diablo (Amplified):** On death, **6 Nether Stars** and **4× normal Wither XP**.
- Verify that **BossDropListener** does not double-apply: only one set of stars/XP (handled in RoofWitherListener).

---

## 5. Hordes

### 5.1 On Devoider / Diablo spawn

- When a Wither is transformed to Devoider or Diablo at Y=127, **10 Wither Skeletons** spawn around random players in the same world shortly after.

### 5.2 Diablo at 25% HP

- On **Amplified**, when **El Diablo** drops to **≤25% HP** (once per Diablo):
  - **1 normal Wither** spawns (at 1 block below the trigger location so it is not at Y=127 and does not become Devoider/Diablo).
  - **3–5 Wither Skeletons** (“Diablo Minion”) spawn.
- Trigger Diablo, damage it to 25% HP, and confirm one extra Wither plus several Wither Skeletons appear.

---

## 6. Blue skull (bedrock break)

- Only **Diablo’s charged (blue) skull** breaks bedrock.
- On Amplified, spawn Diablo, let it fire a **charged** Wither skull at **bedrock** (e.g. Nether roof or a bedrock wall). The block at impact should turn to air.
- Normal (black) skulls do not break bedrock in this implementation.

---

## 7. Diablo's Lair (floating platform)

1. Get permission **`lw.admin.arena`** (default op).
2. On **Survival** or **Amplified**, go to the location where you want the center of the platform (e.g. Nether roof or a void world).
3. Run:
   - **`/diablo-lair`** — generates a bedrock platform with default radius **15** (31×31 blocks) at your feet and registers the arena “Diablo's Lair” with movement restriction.
   - **`/diablo-lair 20`** — radius 20 (41×41). Radius is clamped between 5 and 64.
4. Confirm a **bedrock floor** appears and that the **ArenaBoundaryListener** keeps you inside the arena (you cannot walk off the platform if movement restriction is on).
5. **`/arena-test`** — creates a different test arena at your location and shows a particle outline for a few seconds; use it to verify boundary behavior without generating bedrock.

---

## 8. Checking kill counts in the database

Use the same MySQL user/database as in `config.yml`.

### 8.1 Player kills

```sql
SELECT * FROM boss_kills;
```

- `wither_kills` — normal Withers killed (for Devoider eligibility: need ≥6).
- `devoider_kills` — Devoiders killed (for Diablo eligibility: need ≥6).

### 8.2 Clan kills

```sql
SELECT * FROM clan_boss_kills;
```

- `wither_kills` — times a clan was “present” at a normal Wither death (≥6 → Devoider on Survival).
- `devoider_kills` — times a clan was “present” at a Devoider death (≥6 → Diablo on Amplified).

### 8.3 Resetting counts (for re-testing)

```sql
DELETE FROM boss_kills;
DELETE FROM clan_boss_kills;
```

Restart or continue; the next Wither/Devoider deaths will start from 0.

---

## 9. Quick test flow (minimal path)

1. **DB:** Ensure MySQL is running and both servers use the same `mysql` config.
2. **Survival:** Spawn and kill **6 normal Withers** (anywhere; not necessarily at Nether Y=127). Optionally have a clan member within 64 blocks to credit the clan.
3. **Survival:** Go to Nether roof, build Wither at **Y=127** → should become **Devoider**. Kill it; check drops (2 stars, 2× XP). Repeat until **6 devoider kills** (check DB or repeat 6 times).
4. **Amplified:** Same DB. Build Wither at Nether Y=127 → should become **Diablo**. Kill it; check drops (6 stars, 4× XP). Confirm only one Diablo can exist at a time.
5. **Amplified:** Spawn Diablo again, damage to 25% HP → confirm 1 Wither + 3–5 Wither Skeletons.
6. **Amplified:** Spawn Diablo, let a **charged (blue) skull** hit bedrock → block breaks.
7. **Admin:** Run `/diablo-lair` at desired location → bedrock platform + arena registered.

---

## 10. Troubleshooting

| Issue | Check |
|-------|--------|
| Wither at Nether Y=127 does not transform | Ensure the spawn event fires at block Y=127. Build the soul sand/skulls so the Wither spawns exactly at 127. |
| Devoider never spawns on Survival | Verify `boss_kills` or `clan_boss_kills` has `wither_kills >= 6` for at least one row. Same DB as Survival. |
| Diablo never spawns on Amplified | Verify `devoider_kills >= 6` (player or clan). Devoider kills are on Survival; DB must be shared. |
| Clan not getting credit | At least one clan member must be within **64 blocks** of the boss at death. Only one credit per clan per death. |
| Two Diablos | Only one Diablo at a time; the second spawn at Y=127 is cancelled until the first dies. |
| No bedrock break | Only **charged (blue)** Wither skulls break bedrock; normal skulls do not. |
| `/diablo-lair` or `/arena-test` unknown | Ensure you have `lw.admin.arena` (default op) and that the command is registered (Survival/Amplified/Common plugin loaded). |
| **`boss_kills` / `clan_boss_kills` table not in "minecraft"** | Tables are created when **Survival** or **Amplified** starts, in the DB given by **`config.yml` → `mysql.database`**. Default is `minecraft`. Ensure that config is the one used by the server (e.g. `plugins/LostWilderness-Survival/configs/.../config.yml` or Amplified) and that `mysql.database` is set to the database you expect. Restart the server so `BossKillRepository` runs and creates the tables if missing. |
