# ⚡ Claude Settings

🛠️ Personal configuration and settings for Claude Code CLI to enhance development workflow.

## 🚀 Quick Setup

- Clone or download -> Add to the root of the project
- Make sure other claude files are not present

## 💻 Usage

Run Claude with custom settings:
```bash
claude --dangerously-skip-permissions
```

## ✨ Features

- 🔔 **Notification sounds** - Audio alerts when tasks complete
- 🔍 **Code quality** - Automatic ESLint and Stylelint execution after file edits
- 🎯 **Suffix hooks** - Use `-u` for ultrathink mode, `-e` for explanations after the prompt
- 📝 **Default prompt enhancement** - Automatic context addition
- 📋 **Coding rules & guidelines** - Personal Claude coding style preferences ([rules.md](.claude/rules.md))
- 🧰 **Curated tool selection** - Pre-defined favorite development tools ([tools.md](.claude/tools.md))
- 🎨 **Implementation templates** - Ready-to-use feature scaffolding ([implement.md](.claude/implement.md))
- 🔐 **Permission management** - Fine-grained allow/deny controls


## 📁 Project Structure

```
.claude/
├── hooks/                    # Custom prompt processing hooks
├── rules.md                  # Coding standards and best practices  
├── tools.md                  # Preferred development tools
├── implement.md              # Feature implementation templates
└── settings.json             # Core configuration
```

### 🔗 Quick Links
- [Settings](.claude/settings.json) - Core configuration file
- [Coding Rules](.claude/rules.md) - Development standards & best practices
- [Tools](.claude/tools.md) - Curated development tools
- [Implementation Guide](.claude/implement.md) - Feature templates

## 🎯 Custom Sufix Hooks

- **`-u` flag**: Activates ultrathink mode for complex problem-solving
- **`-e` flag**: Adds detailed explanation context to responses
- **Default enhancement**: Automatic prompt improvements

---

*Made with 🤖️ for enhanced Claude Code development experience*
