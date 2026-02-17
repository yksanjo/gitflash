# 🎯 Project Navigator for Vibe Coders

A blazing-fast CLI project switcher for developers who work with many projects. Navigate between projects instantly with fuzzy search, check git status across all repos, and automate your workflow.

![Project Navigator Demo](https://via.placeholder.com/800x400?text=Project+Navigator+Demo)

## Features

- ⚡ **Instant Navigation** - Jump to any project with a short command
- 🔍 **Fuzzy Search** - Type partial names to match projects
- 🎨 **Interactive Picker** - Use fzf for visual project selection
- 📊 **Git Status** - Check all repos at once
- 🔄 **Multi-repo Operations** - Pull all repos with one command
- ⚙️ **Easy Configuration** - Simple alias-based setup

## Quick Start

### 1. Install Dependencies

```bash
# Install fzf (fuzzy finder)
brew install fzf
```

### 2. Download the Script

```bash
curl -fsSL https://raw.githubusercontent.com/yksanjo/project-navigator/main/.zsh-projects -o ~/.zsh-projects
```

### 3. Add to Your Shell

Add this to your `~/.zshrc`:

```bash
# Load fzf
[ -f /opt/homebrew/opt/fzf/shell/key-bindings.zsh ] && source /opt/homebrew/opt/fzf/shell/key-bindings.zsh

# Load project navigator
source ~/.zsh-projects
```

### 4. Configure Your Projects

Edit `~/.zsh-projects` and add your projects:

```zsh
WORKSPACE_PROJECTS=(
    "myproject"    "$HOME/projects/myproject"
    "api"          "$HOME/projects/api-service"
    "web"          "$HOME/projects/web-app"
)
```

### 5. Start Using It!

```bash
# Open a new terminal tab, then:

projects          # List all projects with git status
p myproject      # Jump to myproject
p api           # Fuzzy match - jumps to api-service
p               # Interactive fzf picker
gstatus         # Git status across all repos
gpull           # Pull all repos
```

## Commands

| Command | Description |
|---------|-------------|
| `p <project>` | Jump to project (supports fuzzy match) |
| `p` | Open interactive fzf picker |
| `projects` | List all projects with git status |
| `gstatus` | Show git status for all repos |
| `gpull` | Git pull on all repos |
| `pa <alias> <path>` | Add project at runtime |

## Configuration

### Adding Projects

Edit the `WORKSPACE_PROJECTS` associative array in `~/.zsh-projects`:

```zsh
declare -A WORKSPACE_PROJECTS
WORKSPACE_PROJECTS=(
    "alias1"    "/full/path/to/project1"
    "alias2"    "/full/path/to/project2"
    # Add more...
)
```

### Project Aliases

Use short, memorable aliases:
- `api` → `~/projects/api-service`
- `web` → `~/projects/web-app`
- `cli` → `~/projects/my-cli-tool`

## Git Status Indicators

When running `projects` or `gstatus`:

- `(git)` - Clean repo, no changes
- `(git ✦)` - Has uncommitted changes
- `→` - Currently in that directory

## Requirements

- **macOS** (tested on macOS Sequoia)
- **zsh** shell
- **fzf** - Fuzzy finder (`brew install fzf`)

## Troubleshooting

### Commands not found?

Make sure you've opened a **new terminal tab** after adding to `.zshrc`. Or run:

```bash
source ~/.zsh-projects
```

### fzf not working?

Ensure fzf is installed:
```bash
brew install fzf
```

And the shell integration is loaded in your `.zshrc`.

## Customization

### Change the Main Command

Rename `p` to something else by editing the function:

```zsh
# Change 'p()' to 'j()' or 'jump()'
j() {
    # ... same code
}
```

### Add More Automation

Extend `gpull()` or add new functions:

```zsh
# Run tests across all projects
gtest() {
    for proj in $(_projects_list); do
        path="${WORKSPACE_PROJECTS[$proj]}"
        if [[ -d "$path" && -f "$path/package.json" ]]; then
            echo "Testing $proj..."
            cd "$path" && npm test
        fi
    done
}
```

## License

MIT License - Feel free to use and modify!

## Contributing

Contributions welcome! Please open an issue or PR on [GitHub](https://github.com/yksanjo/project-navigator).

---

Made with 💜 for vibe coders
