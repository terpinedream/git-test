# Git TUI - Terminal Git Interface

A comprehensive terminal-based Git interface with GitHub integration, file tree navigation, and text editing capabilities.

## Features

### 🎮 **Vim-like Modal Interface**
- **Normal Mode**: Navigation and commands (default mode)
- **Insert Mode**: Text input for configuration fields
- **Mode indicators** in status bar (NORMAL/INSERT)
- **ESC key** to exit insert mode and return to normal mode
- **Consistent vim motions** throughout the interface
- **Modal keybindings** - different actions in different modes

### 🗂️ **File Tree Navigation**
- **Real-time directory browsing** using the `tree` command
- **Color-coded file types**: Directories (blue), files (green), tree structure (cyan)
- **Keyboard navigation**: `j`/`k` to move up/down, `Enter` to open files or enter directories
- **Scroll indicators** showing current position in large file lists
- **Path display** showing current working directory

### 📝 **External Text Editor Integration**
- **Seamless external editor launch** via `Enter` or `o` key
- **Configurable editor** - defaults to neovim, respects `$EDITOR` environment variable
- **Full editor functionality** - use your preferred editor (neovim, vim, nano, etc.)
- **Automatic file tree refresh** after editing
- **Terminal state preservation** - clean transition to and from external editor

### 🔗 **GitHub Integration**
- **Repository creation and connection** to existing repositories
- **Personal Access Token authentication**
- **Automatic git conflict resolution** for divergent branches
- **Smart repository handling**: Creates new repos or connects to existing ones
- **Enhanced error reporting** with detailed debug information

### 🎨 **User Interface**
- **Dual-panel layout**: File tree on left, GitHub config on right
- **Color-coded interface** with syntax highlighting
- **Status bar** showing current mode (NORMAL/INSERT) and messages
- **Dynamic help text** that changes based on current mode
- **Focus management** between different UI sections
- **Modal indicators** clearly showing current input mode

### ⚙️ **Configuration**
- **Persistent settings** stored in `config.ini`
- **GitHub credentials** management
- **Editor preferences** configuration

## Installation

### Prerequisites
```bash
# Arch Linux
sudo pacman -S ncurses libgit2 curl json-c tree

# Ubuntu/Debian
sudo apt-get install libncurses5-dev libgit2-dev libcurl4-openssl-dev libjson-c-dev tree
```

### Build
```bash
make clean && make
```

## Usage

### Navigation (Normal Mode)
- **`h`/`l`**: Move between file tree and GitHub panels
- **`j`/`k`**: Navigate up/down in file tree
- **`i`**: Enter insert mode for editing GitHub fields
- **`Enter`**: Open file in editor or enter directory
- **`o`**: Open selected file in editor
- **`s`**: Git status
- **`a`**: Git add
- **`c`**: Git commit
- **`p`**: Git push
- **`P`**: Git pull
- **`q`**: Quit application

### Text Input (Insert Mode)
- **`ESC`**: Exit insert mode and return to normal mode
- **`Enter`**: Confirm input and exit insert mode
- **Type normally**: Edit text in the current field
- **Arrow keys**: Move cursor within text (for repository field)
- **Backspace**: Delete characters

### File Tree
- **Directory navigation**: Use arrow keys or `j`/`k` to move
- **File opening**: Press `Enter` on a file to open it in the editor
- **Directory entry**: Press `Enter` on a directory to navigate into it
- **Visual indicators**: Selected items are highlighted in reverse video

### External Editor
- **`Enter`** or **`o`**: Open selected file in external editor
- **Editor selection**: Uses `$EDITOR` environment variable or defaults to neovim
- **Full editor features**: All features of your chosen editor (neovim, vim, etc.)
- **Automatic return**: Returns to file tree when editor is closed
- **File tree refresh**: Automatically refreshes to show any changes made

### GitHub Integration
1. **Enter GitHub username** in the username field
2. **Enter Personal Access Token** in the token field
3. **Enter repository name** in the repository field
4. **Press Enter** on the [Connect] button to connect

The application will:
- Try to create a new repository if it doesn't exist
- Connect to existing repository if it already exists
- Handle git conflicts automatically
- Push local changes or pull remote changes as needed

## File Structure

```
tui-git/
├── src/
│   ├── main.c          # Main application entry point
│   ├── ui.c            # User interface and input handling
│   ├── filetree.c      # File tree navigation and display
│   ├── editor.c        # Text editor functionality
│   ├── github.c        # GitHub API integration
│   ├── git.c           # Git operations using libgit2
│   ├── config.c        # Configuration management
│   └── keymap.c        # Key mapping and shortcuts
├── include/
│   ├── ui.h            # UI structures and declarations
│   ├── filetree.h      # File tree structures
│   ├── editor.h        # Editor structures
│   ├── github.h        # GitHub API structures
│   ├── git.h           # Git operation structures
│   ├── config.h        # Configuration structures
│   └── keymap.h        # Key mapping structures
├── config.ini          # Configuration file
├── Makefile            # Build configuration
└── README.md           # This file
```

## Configuration

The `config.ini` file stores application settings:

```ini
# Git TUI Configuration
github_username=your_github_username
github_token=your_personal_access_token
editor_command=nvim
```

## Key Features

### Enhanced Git Conflict Resolution
- **Automatic branch detection**: Tries `main` first, falls back to `master`
- **Smart merge strategies**: Configures git pull strategy to avoid conflicts
- **Force push for new repos**: Automatically handles initial push issues
- **Fetch and reset fallback**: If pull fails, fetches and resets to remote

### File Tree Integration
- **Real-time updates**: File tree refreshes after git operations
- **Path preservation**: Maintains current directory context
- **Error handling**: Graceful handling of permission issues and missing files

### External Editor Integration
- **Seamless file opening**: Files open directly in your preferred external editor
- **Full editor power**: Use all features of neovim, vim, or any other editor
- **Automatic file tree refresh**: Changes are reflected immediately after editing
- **Environment variable support**: Respects `$EDITOR` environment variable

## Troubleshooting

### Common Issues

1. **"tree command not found"**
   - Install the `tree` package for your distribution
   - The file tree will show an error message if tree is not available

2. **GitHub authentication fails**
   - Ensure your Personal Access Token has the correct permissions
   - Check that the token hasn't expired
   - Verify your GitHub username is correct

3. **Git conflicts**
   - The application automatically handles most git conflicts
   - Check the debug output in `debug_output.txt` for detailed information

4. **File permissions**
   - Ensure you have read/write permissions for the current directory
   - Check file permissions for files you're trying to edit

### Debug Information

The application creates several debug files:
- `debug_output.txt`: Detailed GitHub API and git operation logs
- `repo_name.txt`: Temporary storage for repository names
- `config.ini`: Application configuration

## Contributing

This is a work in progress. Key areas for enhancement:
- **Git status display**: Show current git status in the UI
- **Branch management**: Add branch switching and creation
- **Commit history**: Display commit history and details
- **Search functionality**: Add file and content search
- **Plugin system**: Allow custom extensions

## License

This project is open source. Feel free to contribute and improve it!
