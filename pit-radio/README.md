# Pit Radio

Pit Radio is the GridSync Discord broadcast system.

It uses GitHub Actions together with Discord webhooks to publish structured announcements without requiring a permanently running Discord bot or external server.

## What Pit Radio Can Do

- Publish automatic GitHub release announcements
- Publish manual bulletins
- Publish changelog entries
- Send to different Discord channels or servers
- Select the target before a manual workflow run
- Ping configured Discord roles
- Use GridSync custom emojis
- Fall back to standard Unicode emojis on servers without GridSync emojis
- Render reusable branded embeds
- Provide a dedicated test mode
- Link every broadcast back to GridSync

## Current Targets

The current GridSync workflow supports:

```text
gridsync
changelog
cannabeez
both
```

`both` is intended for broadcasts that should be sent to the main GridSync destination and the external community destination.

The changelog target uses its own webhook and can therefore publish directly into the GridSync changelog channel.

## Modes

### Test

Used to verify:

- webhook connection
- selected destination
- custom emoji rendering
- fallback emoji rendering
- embed formatting

### Manual

Used for:

- community announcements
- Discord server updates
- project news
- changelog entries
- special releases

### Automatic Release

Triggered by a published GitHub Release.

This requires no manual workflow run.

## Custom Emoji System

GridSync targets can use server specific emojis through Discord's custom emoji syntax:

```text
<:emoji_name:emoji_id>
```

Pit Radio stores the emoji IDs in the workflow environment and builds the Discord syntax automatically.

For destinations that do not have access to the GridSync emojis, Pit Radio uses Unicode fallback values instead.

This means the same announcement can be sent to multiple servers without breaking its layout.

## Link Block

Pit Radio uses a fixed link section:

```text
Previews · Details · Download
Open on GridSync
```

If a manual GridSync URL is supplied, that URL is used.

If no manual URL is supplied, Pit Radio falls back to:

https://gridsync.ch/

The embed title itself remains non clickable so it does not imply that a dedicated article exists for every announcement.

## Why GitHub Actions?

Pit Radio does not need:

- a VPS
- a hosted bot process
- a Discord bot token
- a permanently running service

GitHub starts the workflow only when needed.

This makes Pit Radio suitable for small community projects that want structured Discord automation without maintaining their own backend.

## Setup

See [`SETUP.md`](SETUP.md).

## Technical Overview

See [`../docs/pit-radio.md`](../docs/pit-radio.md).
