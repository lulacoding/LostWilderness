# Discord bot

## Linking and approval

- **/link** — link **Minecraft username** to Discord (e.g. `/link` in Discord with MC username, or in-game).
- **/approve** — staff approves a link (so only approved players get whitelist/roles).
- **Bedrock:** Bedrock players use a different link format; example given: **/link ".Lobsta2"** (the prefix is used to identify Bedrock accounts). *“Bedrock /link ".Lobsta2".”*
- After link and approve: **roles** and **nickname = MC name** are set so the Discord side matches the in-game identity.

## Whitelist and clan roles

- **Whitelistbot** (by **lulacoding**) is used for whitelist management.
- The bot **creates clan roles and channels** when clans are created in-game (via the clan plugin). So each clan gets a Discord role and optionally a channel; **ally chats** and **alliance** level are mirrored at Discord level.
- **Discord webhooks** are used for **server-wide in-game chat** and **logs** (e.g. to an admin channel).

## Skipping Bedrock in name checks

- For anticheat/name checks, **anyone with a name beginning with \*** (the Bedrock prefix) is **skipped** so Bedrock players are not falsely flagged. *“Also skipping anyone with a name beginning with * which is the symbol for bedrock players.”*

## Source

- Direct Messages (Grovyle187): /link, /approve, Bedrock .Lobsta2, whitelistbot (lulacoding).
- Bible section 2: roles, nickname = MC name, clan roles and channels, webhook logs.
