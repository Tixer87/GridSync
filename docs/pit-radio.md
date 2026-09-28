# Pit Radio Technical Reference

This document explains the example workflow structure and shows which parts users normally customize.

## Architecture

```text
GitHub event
or
manual workflow run
        │
        ▼
GitHub Actions workflow
        │
        ▼
Configuration from Secrets and Variables
        │
        ▼
Python message builder
        │
        ├─ selects target
        ├─ selects emoji set
        ├─ builds embed
        ├─ adds optional role mention
        └─ selects webhook
        │
        ▼
Discord webhook
```

## Public Configuration vs Secret Configuration

### Public Workflow File

The YAML workflow can safely contain:

```text
secret names
variable names
target names
fallback emoji codes
message templates
routing logic
```

### GitHub Actions Secrets

Use Secrets for sensitive values:

```text
webhook URLs
tokens
API keys
passwords
```

Example:

```yaml
MAIN_WEBHOOK: ${{ secrets.DISCORD_WEBHOOK }}
```

Anyone can see the name `DISCORD_WEBHOOK` in a public repository.

They cannot see the secret value stored behind it.

## GitHub Actions Variables

Use Variables for reusable non secret configuration:

```text
community name
website URL
role IDs
emoji IDs
```

Example:

```yaml
COMMUNITY_NAME: ${{ vars.COMMUNITY_NAME }}
MAIN_ROLE_ID: ${{ vars.MAIN_ROLE_ID }}
```

## Example Webhook Mapping

The example workflow uses:

```text
MAIN_WEBHOOK
CHANGELOG_WEBHOOK
EXTERNAL_WEBHOOK
```

The corresponding GitHub Secrets are:

```text
DISCORD_WEBHOOK
CHANGELOG_WEBHOOK
EXTERNAL_DISCORD_WEBHOOK
```

You may rename these in your own version.

If you rename them, update both the workflow environment variables and the Secret names they reference.

## Target Routing

The example targets are:

```text
main
changelog
external
both
```

Their example behavior is:

```text
main
→ main webhook
→ custom emojis enabled
→ optional main role mention

changelog
→ changelog webhook
→ custom emojis enabled
→ optional main role mention

external
→ external webhook
→ fallback emojis
→ optional external role mention

both
→ main webhook
→ external webhook
```

This routing is only an example.

You can add, remove or rename destinations.

## Why External Uses Fallback Emojis

Discord custom emojis may not be usable on another server.

For that reason the example workflow calls:

```python
build(False)
```

for the external target.

That forces fallback emojis.

If your external destination can use the same custom emojis, change it to:

```python
build(True)
```

## Emoji Configuration

Each emoji entry follows this structure:

```python
"logical_key": (
    "discord_emoji_name",
    "GITHUB_VARIABLE_NAME",
    "unicode_fallback"
)
```

Example:

```python
"tools": (
    "tools",
    "EMOJI_TOOLS",
    "\U0001F6E0\uFE0F"
)
```

To configure a custom emoji:

1. Change `tools` to the exact Discord emoji name if necessary
2. Create the GitHub Variable `EMOJI_TOOLS`
3. Set its value to the numeric Discord emoji ID

If the variable is empty, the fallback is used.

## Manual Input Fields

### mode

```text
test
manual
```

### target

```text
main
changelog
external
both
```

### manual_title

The embed title.

### manual_intro

Optional introductory text.

### manual_details

Multiple items separated with:

```text
|
```

Example:

```text
Item one | Item two | Item three
```

### manual_url

Optional link used in the details field.

If empty, `WEBSITE_URL` can be used as fallback.

## Role Mentions

The workflow may prepend:

```text
<@&ROLE_ID>
```

to the Discord message.

The payload restricts `allowed_mentions` to the configured role.

This prevents arbitrary mentions inside announcement text from being parsed by Discord.

## Test Mode

Test mode exists to confirm configuration before sending a real announcement.

A good test should verify:

```text
correct channel
correct webhook
correct target
correct emoji behavior
correct website link
no unwanted role mention
```

A successful Discord webhook request normally returns:

```text
HTTP 204
```

That only confirms that Discord accepted the webhook request.

It does not prove that the webhook points to the intended channel.

## Release Mode

A published GitHub Release provides:

```text
release name
release body
release URL
```

The workflow can use those values automatically.

Users who do not publish GitHub Releases can remove release mode entirely and keep only manual mode.

## What Most Users Need To Change

For a basic installation, change or configure these items:

```text
DISCORD_WEBHOOK
CHANGELOG_WEBHOOK
EXTERNAL_DISCORD_WEBHOOK

COMMUNITY_NAME
WEBSITE_URL

MAIN_ROLE_ID
EXTERNAL_ROLE_ID

optional EMOJI variables
optional emoji names
optional target names
optional display text
```

Everything else can usually remain unchanged for the first test.

## Extending the Workflow

Common extensions include:

```text
more Discord channels
more servers
different role mentions
different embed templates
different colors
different link labels
different automatic triggers
different announcement categories
```

Add one change at a time and use test mode before sending production announcements.
