# SF311 Blocked Driveway — Claude Code Skill

A [Claude Code](https://docs.anthropic.com/en/docs/claude-code) skill that automates filing SF311 complaints for vehicles blocking your driveway. Give it three photos of the offending car, and it handles the rest.

## What it does

1. **Reads your photos** using Claude's vision to extract the license plate, make, model, color, and vehicle type
2. **Opens the SF311 form** in your browser via [Claude in Chrome](https://chromewebstore.google.com/detail/claude-in-chrome/)
3. **Fills every field** — vehicle details, your address, contact info, and a description
4. **Uploads the photos** as evidence
5. **Asks you to confirm** before submitting (never auto-submits)

## Prerequisites

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) CLI
- [Claude in Chrome](https://chromewebstore.google.com/detail/claude-in-chrome/) browser extension (for form automation)

## Installation

```bash
# Clone into your personal skills directory
mkdir -p ~/.claude/skills
git clone https://github.com/sam-silv/sf311-blocked-driveway.git ~/.claude/skills/sf311-blocked-driveway
```

Then edit `~/.claude/skills/sf311-blocked-driveway/SKILL.md` and replace the placeholders:

```
- **Name**: YOUR_NAME          → your full name
- **Phone**: YOUR_PHONE        → your phone number
- **Driveway Address**: YOUR_ADDRESS  → your street address
```

## Usage

```
/sf311 photo1.jpg photo2.jpg photo3.jpg
```

Claude will analyze the photos, show you what it found, and ask for confirmation before proceeding to fill the form.

## Options

By default, the skill selects **"cite and tow"** as the request type. If you prefer citation only, just tell Claude when it asks for confirmation.

## License

MIT
