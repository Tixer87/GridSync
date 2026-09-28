# GridSync Voice Packs

This repository is primarily used as the release and download backend for GridSync iRaceDeck Voice Packs.

The actual GridSync project lives on:

https://gridsync.ch/

## Why This Repository Exists

GridSync Voice Packs can become too large for practical direct website hosting.

GitHub Releases therefore acts as the distribution platform.

The workflow is simple:

```text
Voice Pack
→ GitHub Release
→ GridSync Website
→ Direct Download
```

The GridSync website links directly to the release files stored here.

This repository is therefore mainly a reliable public download and release archive rather than a traditional source code repository.

## Voice Pack Releases

Published releases contain downloadable GridSync Voice Packs for iRaceDeck Race Engineer.

The website provides the presentation, previews and project information.

GitHub provides the actual release storage and download infrastructure.

### GridSync Website

https://gridsync.ch/

## Pit Radio

While setting up automated release announcements for the Voice Packs, a small GitHub Actions workflow was created to notify Discord when a new release was published.

As usually happens with GridSync projects, the small helper did not stay small for very long.

That workflow gradually became **Pit Radio**.

Pit Radio can now handle:

- Automatic GitHub Release broadcasts
- Manual Discord announcements
- Changelog posts
- Multiple Discord webhook destinations
- Selectable broadcast targets
- Discord role mentions
- Custom server emojis
- Automatic fallback emojis for other servers
- Test broadcasts
- Reusable branded Discord embeds

The production Pit Radio workflow used by GridSync lives in:

```text
.github/workflows/discord-release.yml
```

Sensitive webhook URLs are stored securely as GitHub Actions Secrets and are not included in the public workflow file.

## Pit Radio Community Template

Because Pit Radio became useful beyond the original Voice Pack release workflow, a reusable community version is being maintained separately.

Branch:

```text
pit-radio-community
```

The community branch removes project specific configuration and documents how other users can configure Pit Radio for their own Discord server, repository and webhooks.

It includes:

```text
README.md

pit-radio/
├─ README.md
├─ SETUP.md
├─ CHANGELOG.md
└─ examples/
   └─ discord-release.example.yml

docs/
└─ pit-radio.md
```

The community version uses placeholders and GitHub Actions Variables instead of GridSync specific role IDs, emoji IDs and destinations.

## Repository Structure

The `main` branch intentionally stays small.

```text
.github/
└─ workflows/
   └─ discord-release.yml

README.md
```

Voice Pack binaries are distributed through **GitHub Releases** rather than being committed directly into the repository.

## GridSync

GridSync is a community driven sim racing project covering Voice Packs, RaTiX, liveries, tools and other experiments that somehow have a habit of becoming full projects.

Website:

https://gridsync.ch/

Discord:

https://discord.gg/RSG338jb44

