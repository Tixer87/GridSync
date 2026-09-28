# Pit Radio

Pit Radio is a reusable Discord publishing workflow built with GitHub Actions and Discord webhooks.

It is designed for communities, projects and repositories that want structured Discord announcements without running a permanent Discord bot.

## How It Works

Pit Radio runs when one of two things happens:

```text
Manual workflow run
or
Published GitHub Release
```

The workflow then:

```text
Reads configuration
→ builds the Discord message
→ selects the destination
→ selects custom or fallback emojis
→ optionally adds a role mention
→ sends the message through a Discord webhook
```

## Included Modes

### Test

Use test mode before publishing real announcements.

It checks:

- webhook routing
- selected destination
- custom emoji rendering
- fallback emoji rendering
- embed formatting
- optional website link

### Manual

Manual mode lets you enter an announcement directly from GitHub Actions.

Available fields:

```text
manual_title
manual_intro
manual_details
manual_url
```

`manual_details` uses the pipe character as a separator:

```text
First item | Second item | Third item
```

Pit Radio turns each item into a separate line.

### Release

When the workflow is configured with:

```yaml
on:
  release:
    types: [published]
```

a published GitHub Release can trigger Pit Radio automatically.

The release name, release body and release URL are read from GitHub and used to build the Discord message.

## Destinations

The example workflow contains four generic targets:

```text
main
changelog
external
both
```

These are only examples.

You can rename them to match your own project, for example:

```text
announcements
updates
partner
all
```

If you rename targets, update all matching target checks in the workflow.

## Custom Emojis

Custom emojis are optional.

When a custom emoji ID is configured, Pit Radio can build Discord syntax like:

```text
<:emoji_name:123456789012345678>
```

When an emoji ID is missing or custom emojis are disabled for a destination, Pit Radio uses a normal Unicode fallback.

This makes the same workflow usable on servers that do not share the same custom emojis.

## Role Mentions

Role mentions are optional.

If a role ID is configured, manual announcements and release broadcasts can mention that role.

Test messages should not ping roles.

## Website Link

The example workflow supports an optional website or details page.

If `manual_url` is supplied, that URL is used for the current manual post.

If it is empty, the workflow can fall back to the configured `WEBSITE_URL`.

If neither exists, the link block is omitted.

## Setup

See [`SETUP.md`](SETUP.md).

## Technical Notes

See [`../docs/pit-radio.md`](../docs/pit-radio.md).
