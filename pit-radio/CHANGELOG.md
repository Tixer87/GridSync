# Pit Radio Changelog

## Community Template

### Included

- Manual Discord announcements
- Automatic GitHub release announcements
- Multiple webhook destinations
- Main, changelog and external example targets
- Optional role mentions
- Optional custom Discord emojis
- Unicode emoji fallbacks
- Test mode
- Configurable community name
- Configurable website URL
- Reusable Discord embed formatting
- Safe GitHub Actions Secret usage
- GitHub Actions Variables for reusable configuration

### Template Goal

The community template is intentionally generic.

It does not contain:

- private webhook URLs
- passwords
- API keys
- bot tokens
- project specific server IDs
- project specific role IDs
- project specific emoji IDs
- project specific release content

Users are expected to configure their own values through GitHub Actions Secrets and Variables.

### Current Example Targets

```text
main
changelog
external
both
```

These names are placeholders and can be renamed.

### Current Example Modes

```text
test
manual
automatic release
```
