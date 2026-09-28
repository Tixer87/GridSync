# Pit Radio Technical Notes

## Architecture

Pit Radio currently consists of:

```text
GitHub Actions
      │
      ▼
discord-release.yml
      │
      ├─ Manual workflow dispatch
      └─ GitHub release event
      │
      ▼
Python broadcast logic
      │
      ├─ Build message
      ├─ Select emoji set
      ├─ Select destination
      ├─ Add role mention
      └─ Send JSON payload
      │
      ▼
Discord Webhook
```

## Workflow File

Pit Radio runs from:

```text
.github/workflows/discord-release.yml
```

GitHub Actions only executes workflow files stored below `.github/workflows/`.

## Events

### Release Event

A published GitHub Release triggers the workflow automatically.

### workflow_dispatch

Allows a user to manually start Pit Radio through the GitHub Actions interface.

Current inputs include:

```text
mode
target
manual_title
manual_intro
manual_details
manual_url
```

## Destination Routing

The current routing model is:

```text
gridsync   → main GridSync webhook
changelog  → GridSync changelog webhook
cannabeez  → external community webhook
both       → GridSync + external community
```

The target value is validated before sending.

This is important because an unknown target should never silently route to an unintended webhook.

## Webhook Secrets

Webhook URLs are stored as GitHub Actions secrets.

Current examples:

```text
DISCORD_WEBHOOK
CHANGELOG_WEBHOOK
CANNABEEZ_DISCORD_WEBHOOK
```

Secrets are injected into the workflow at runtime.

They should never be committed into the repository.

## Custom Emojis

GridSync emoji configuration consists of:

```text
logical key
Discord emoji name
environment variable containing the emoji ID
Unicode fallback
```

For a GridSync destination:

```text
custom emoji available
→ <:name:id>
```

For an external destination:

```text
custom emoji disabled
→ Unicode fallback
```

This allows one payload system to support both branded and generic Discord servers.

## Role Mentions

Pit Radio can prepend:

```text
<@&ROLE_ID>
```

to the message content.

`allowed_mentions` is restricted so Discord only parses the intended role mention.

This prevents uncontrolled mentions from text inside an announcement.

## Embed Layout

Current Pit Radio posts follow this structure:

```text
PIT RADIO header

Embed title
Introduction
Details

Previews · Details · Download
Open on GridSync

Pit Radio · GridSync Community
```

The title is intentionally not linked.

Navigation is kept in the dedicated GridSync link field.

## Manual Details

`manual_details` uses the pipe character as a separator:

```text
Item one | Item two | Item three
```

The workflow splits the value and assigns icons in order.

Additional entries can fall back to a neutral bullet after the configured icon list is exhausted.

## HTTP Result

Discord webhook success normally returns:

```text
HTTP 204
```

This means Discord accepted the webhook request.

It does not by itself verify that the selected webhook points to the intended channel, which is why Pit Radio includes explicit target routing and test mode.

## Extending Pit Radio

Possible future additions include:

```text
news
maintenance
voicepack
ratix
livery
tools
website updates
server status
additional Discord communities
```

The existing target and payload structure can be extended incrementally.
