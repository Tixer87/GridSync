# Pit Radio Changelog

## Current Development Version

### Added

- Multiple Discord webhook targets
- Dedicated GridSync changelog target
- Manual target selection
- Manual announcement mode
- Test mode
- Automatic GitHub release broadcasts
- Discord role mentions
- GridSync custom emoji support
- Unicode emoji fallbacks for external servers
- Reusable GridSync link block
- Branded Discord embeds

### Changed

- Pit Radio is no longer limited to a single Voice Packs webhook
- Manual broadcasts can be routed to individual destinations
- Embed titles remain non clickable
- GridSync navigation is handled through the fixed link block
- External servers use fallback emojis when GridSync custom emojis are unavailable

### Current Targets

```text
gridsync
changelog
cannabeez
both
```

### Current Modes

```text
test
manual
automatic release
```

## Project Direction

Pit Radio began as a small release notification workflow for GridSync voice packs.

It has since evolved into a reusable Discord publishing system for GridSync community projects and can be extended with additional channels, servers, templates and broadcast types.
