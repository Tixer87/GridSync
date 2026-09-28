# GridSync Community Projects

Community driven sim racing projects, tools and resources.

GridSync started around custom iRaceDeck Race Engineer voice packs and has grown into a broader community project covering voice packs, RaTiX, liveries, tools and Discord automation.

## Projects

### Pit Radio

Pit Radio is a lightweight Discord broadcast system powered by GitHub Actions and Discord webhooks.

It can currently handle:

- Automatic GitHub release broadcasts
- Manual community bulletins
- Changelog broadcasts
- Multiple Discord webhook targets
- Target selection per workflow run
- Role notifications
- GridSync custom emojis
- Automatic standard emoji fallbacks for other servers
- Reusable Discord embeds
- Test mode for webhook and emoji checks
- Fixed GridSync link blocks
- No external server or permanently running bot required

Documentation: [`pit-radio/README.md`](pit-radio/README.md)

### Voice Packs

Community voice packs for iRaceDeck Race Engineer.

Current GridSync packs and projects include:

- Ryan Race Engineer
- Snoop Voice Pack
- Family Guy multi voice pack
- Pit Wall Legends
- Additional community voice projects

Documentation: [`docs/voice-packs.md`](docs/voice-packs.md)

### RaTiX

RaTiX is a GridSync driver rating and race analysis project.

More information:

https://gridsync.ch/ratix/

### Liveries

GridSync liveries and community designs for sim racing.

### Tools

Small utilities, experiments and supporting tools created around the GridSync ecosystem.

## Website

https://gridsync.ch/

## Discord

https://discord.gg/RSG338jb44

## Repository Structure

```text
.github/
└─ workflows/
   └─ discord-release.yml

pit-radio/
├─ README.md
├─ SETUP.md
└─ CHANGELOG.md

docs/
├─ pit-radio.md
└─ voice-packs.md

README.md
```

## Community

GridSync is built around practical community projects. Features may begin as small internal tools and later become reusable resources when they prove useful beyond the original project.
