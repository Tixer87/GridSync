# Pit Radio Setup

This guide describes the basic setup required to reuse Pit Radio.

## 1. Create Discord Webhooks

Create a webhook for every Discord destination you want Pit Radio to support.

Example destinations:

```text
Voice Packs
Changelog
External Community Server
```

In Discord:

```text
Channel Settings
→ Integrations
→ Webhooks
→ New Webhook
```

Copy each webhook URL.

## 2. Add GitHub Actions Secrets

In the GitHub repository open:

```text
Settings
→ Secrets and variables
→ Actions
→ New repository secret
```

The current GridSync workflow uses:

```text
DISCORD_WEBHOOK
CHANGELOG_WEBHOOK
CANNABEEZ_DISCORD_WEBHOOK
```

Never place actual webhook URLs directly in the public workflow file.

## 3. Configure Role IDs

Pit Radio can mention configured Discord roles.

Role IDs are stored in the workflow environment, for example:

```text
GRIDSYNC_ROLE_ID
CANNABEEZ_ROLE_ID
```

To copy a Discord role ID, enable Developer Mode in Discord and use Copy ID on the role.

## 4. Configure Custom Emojis

Custom Discord emojis require:

```text
emoji name
emoji ID
```

The workflow generates the final Discord format automatically:

```text
<:name:id>
```

If a destination cannot use the custom emoji, Pit Radio falls back to standard Unicode emojis.

## 5. Workflow Targets

The current workflow supports:

```text
gridsync
changelog
cannabeez
both
```

A manual run should therefore select both a mode and a target.

Example:

```text
mode: manual
target: changelog
```

## 6. Manual Fields

Pit Radio manual mode currently accepts:

```text
manual_title
manual_intro
manual_details
manual_url
```

### manual_title

Main embed title.

Example:

```text
GridSync Discord Server Update
```

### manual_intro

Short italic introduction above the details.

Example:

```text
The GridSync Discord server has received a major community update.
```

### manual_details

Separate entries using `|`.

Example:

```text
New onboarding system | Updated permissions | New changelog channel
```

Pit Radio converts each item into its own formatted line.

### manual_url

Optional GridSync destination page.

Example:

```text
https://gridsync.ch/ratix/
```

If left empty, Pit Radio links to:

```text
https://gridsync.ch/
```

## 7. Test Before Publishing

Run:

```text
mode: test
target: gridsync
```

The test should confirm:

- correct webhook
- correct channel
- custom emojis
- embed format
- GridSync link block

For an external server, run the test against that target and verify the fallback emojis.

## 8. Automatic Releases

The workflow also listens for:

```yaml
release:
  types: [published]
```

When a GitHub Release is published, Pit Radio can automatically broadcast the release without a manual workflow run.

## Adding Another Destination

To add another server or channel:

1. Create a new Discord webhook
2. Store it as a GitHub Actions secret
3. Add the target to the workflow input options
4. Allow the target in the Python validation set
5. Add a send route for the new webhook
6. Decide whether it should use GridSync custom emojis or fallback emojis

The existing architecture can therefore be extended without rebuilding Pit Radio from scratch.
