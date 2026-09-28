# Pit Radio Community Template

Pit Radio is a reusable Discord broadcast workflow powered by GitHub Actions and Discord webhooks.

This branch is intended as a clean community template. It contains documentation and an example workflow that other users can copy into their own repository and adapt to their own Discord server.

No private webhook URLs, tokens, server specific IDs or project specific values should be stored in the public workflow file.

## What Pit Radio Can Do

Pit Radio can:

- Send manual Discord announcements
- Send changelog posts
- Send automatic GitHub release announcements
- Route messages to different Discord webhooks
- Mention optional Discord roles
- Use optional custom Discord emojis
- Fall back to standard Unicode emojis
- Run webhook and emoji tests
- Add a reusable website or details link
- Work without a permanently running bot or external server

## Files

```text
.github/
└─ workflows/
   └─ your-live-workflow.yml

pit-radio/
├─ README.md
├─ SETUP.md
├─ CHANGELOG.md
└─ examples/
   └─ discord-release.example.yml

docs/
└─ pit-radio.md
```

The example workflow belongs in:

```text
pit-radio/examples/discord-release.example.yml
```

A user who wants to activate Pit Radio should copy that file into:

```text
.github/workflows/
```

and rename it as desired.

## Start Here

1. Read [`pit-radio/SETUP.md`](pit-radio/SETUP.md)
2. Copy the example workflow into `.github/workflows/`
3. Create the required Discord webhooks
4. Add webhook URLs as GitHub Actions Secrets
5. Add optional IDs and branding as GitHub Actions Variables
6. Run Pit Radio in test mode
7. Enable manual or release broadcasts

## Security

Never place webhook URLs, bot tokens, API keys or passwords directly in a public workflow file.

Use GitHub Actions Secrets for sensitive values.

Server IDs, role IDs and emoji IDs are not secret credentials, but keeping them in GitHub Variables makes the template easier to reuse.
