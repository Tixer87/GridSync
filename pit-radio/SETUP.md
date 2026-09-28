# Pit Radio Setup

This guide explains exactly what must be changed before using the example workflow.

## 1. Copy the Example Workflow

Copy:

```text
pit-radio/examples/discord-release.example.yml
```

to:

```text
.github/workflows/discord-release.yml
```

GitHub only runs Actions workflows that are stored inside `.github/workflows/`.

## 2. Create Discord Webhooks

Create one webhook for every Discord destination you want to use.

In Discord:

```text
Channel Settings
→ Integrations
→ Webhooks
→ New Webhook
```

The example workflow expects up to three webhook destinations:

```text
main
changelog
external
```

You do not need to use all three.

## 3. Add GitHub Actions Secrets

Open:

```text
Repository
→ Settings
→ Secrets and variables
→ Actions
→ Secrets
```

Create the secrets required by the destinations you use.

The example workflow uses:

```text
DISCORD_WEBHOOK
CHANGELOG_WEBHOOK
EXTERNAL_DISCORD_WEBHOOK
```

Example mapping:

```text
DISCORD_WEBHOOK
→ webhook for your main announcement channel

CHANGELOG_WEBHOOK
→ webhook for your changelog or update channel

EXTERNAL_DISCORD_WEBHOOK
→ webhook for another server or community
```

Important:

```text
Never paste the actual webhook URL into the public YAML file.
```

## 4. Add GitHub Actions Variables

Open:

```text
Repository
→ Settings
→ Secrets and variables
→ Actions
→ Variables
```

The example workflow supports:

```text
COMMUNITY_NAME
WEBSITE_URL
MAIN_ROLE_ID
EXTERNAL_ROLE_ID
```

Suggested values:

```text
COMMUNITY_NAME
Your project or community name

WEBSITE_URL
https://example.com/

MAIN_ROLE_ID
Optional Discord role ID for the main server

EXTERNAL_ROLE_ID
Optional Discord role ID for the external server
```

Role IDs are optional.

If no role should be mentioned, leave the variable empty or remove the role configuration from your own workflow.

## 5. Optional Custom Emoji Variables

The example workflow supports optional custom emoji IDs.

Available variables include:

```text
EMOJI_MAIN
EMOJI_LOGO
EMOJI_DISCORD
EMOJI_DOWNLOAD
EMOJI_VOICE
EMOJI_STATS
EMOJI_TOOLS
EMOJI_RACING
EMOJI_CAR1
EMOJI_CAR2
EMOJI_CAR3
```

Only enter the numeric Discord emoji ID.

Example:

```text
123456789012345678
```

Do not enter:

```text
<:name:123456789012345678>
```

Pit Radio builds that syntax automatically.

If you leave an emoji variable empty, the workflow uses its fallback emoji.

## 6. Custom Emoji Names

The example workflow contains placeholder emoji names such as:

```python
("community", "EMOJI_MAIN", ...)
("download", "EMOJI_DOWNLOAD", ...)
("tools", "EMOJI_TOOLS", ...)
```

The first value must match the actual name of your Discord custom emoji.

Example:

If your emoji is:

```text
:my_download:
```

change:

```python
("download", "EMOJI_DOWNLOAD", ...)
```

to:

```python
("my_download", "EMOJI_DOWNLOAD", ...)
```

The ID still comes from the GitHub Variable.

## 7. Rename Targets If Needed

The example targets are:

```text
main
changelog
external
both
```

You may keep them as they are or rename them.

If you rename a target, update every matching place in the workflow:

```text
workflow_dispatch options
target validation
send routing
```

For example, if `main` becomes `announcements`, update all checks that currently use `main`.

## 8. Change the Display Text

Search the example workflow for these strings:

```text
PIT RADIO // NEW RELEASE
PIT RADIO // COMMUNITY BULLETIN
PIT RADIO // EMOJI CHECK
Previews · Details · Download
Open details
Pit Radio
```

You can change them to match your own project style.

## 9. Test the Workflow

Open:

```text
Repository
→ Actions
→ Pit Radio
→ Run workflow
```

Use:

```text
mode: test
target: main
```

Verify:

- the message arrives in the correct channel
- the correct webhook is used
- custom emojis appear correctly
- fallback emojis appear where expected
- no role is pinged
- the optional link is correct

Then test any additional targets you plan to use.

## 10. Manual Announcement Test

Use:

```text
mode: manual
target: main
```

Example values:

```text
manual_title:
Community Update

manual_intro:
A short introduction to the update.

manual_details:
First change | Second change | Third change

manual_url:
https://example.com/update
```

## 11. Automatic Release Broadcasts

If you want automatic release announcements, keep:

```yaml
on:
  release:
    types: [published]
```

If you do not want release broadcasts, remove the release trigger and the release specific logic from your own workflow.

## 12. Add Another Destination

To add another Discord destination:

1. Create another Discord webhook
2. Add it as a GitHub Actions Secret
3. Add the target to `workflow_dispatch`
4. Add the target to the validation set
5. Add a new send route
6. Decide whether the destination should use custom emojis or fallback emojis
7. Add an optional role variable if needed

Pit Radio is intentionally structured so more destinations can be added without rebuilding the whole workflow.
