# ⚡ Claude Settings

Personal configuration and settings for Claude Code CLI to enhance development workflow.

## Quick Setup

Clone or download → Add to root of project. Make sure other Claude files are not present.

## Features

- **Notification sounds** - Audio alerts when tasks complete
- **Code quality** - Automatic ESLint and Stylelint execution after file edits
- **Permission management** - Fine-grained allow/deny controls
- **Slash commands** - Custom workflow commands
- **Plugins** - Custom plugins used

## Slash Commands

### `/code-review`
Comprehensive code review of branch changes. Covers architecture, TypeScript safety, Vue conventions, i18n, security, 
performance, error handling, and more. Outputs structured report with severity-tiered issues and action items. It also
prints localhost link to affected UI changes to save time navigating through app.

### `/handover`
End-of-session handover workflow. Organizes uncommitted work, updates `CLAUDE.md`, creates `SESSION_SUMMARY.md`, 
and prepares clear next-session priorities.
