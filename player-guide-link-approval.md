# Lost Wilderness – Link Approval (Player Guide)

## Overview

**Link Approval** lets you link your **Minecraft** account to **Discord**. A link request is started from Discord (or by an admin); you then approve or deny it in-game with **/approve** or **/deny**.

---

## Commands (players)

| Command | Description |
|--------|-------------|
| **/approve** | Approve the pending link request for your Minecraft account. You must have a pending request. |
| **/deny** | Deny the pending link request. |

---

## How it works (player view)

1. Someone (usually a Discord bot or an admin) starts a link request that targets your Minecraft username.
2. If you’re **online**, you get a chat message like:  
   `Discord user <name> (<id>) wants to link. Type /approve or /deny.`
3. If you’re **offline**, the request is stored; when you next join, you may get the same message (depending on server setup).
4. You run:
   - **/approve** – Your MC account is linked to that Discord user (the server sends the approval to the bot).
   - **/deny** – The request is cancelled; no link is made.
5. If you have **no** pending request and use **/approve** or **/deny**, you’ll see: “You have no pending link requests.”

---

## Admin / console

- **/linkrequest &lt;discordId&gt; &lt;discordUsername&gt; &lt;mcUsername&gt;**  
  Only **console or RCON**. Creates a pending link for the given Minecraft user; they see the message and can **/approve** or **/deny**.

---

## Tips

- You must be in-game to approve or deny; the server needs to know it’s really you.
- Linking is used so the server (and Discord bot) can tie your Discord identity to your Minecraft account (e.g. for roles or verification).
