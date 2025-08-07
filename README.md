# Claude Settings

Personal configuration and settings for Claude Code CLI.

## Setup

```bash
./install.sh
```

## Usage

Run Claude with custom settings:
```bash
claude --dangerously-skip-permissions
```

## Structure

- `.claude/` - Configuration files and hooks
- `CLAUDE.md` - Project-specific instructions
- `install.sh` - Setup script

## Features

- Custom hooks for prompt processing `-u`, `-e`
- Development workflow automation
- Project-specific Claude behavior configuration
