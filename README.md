# Beginner-Friendly Helix Editor Configuration

![Helix Editor Logo](https://img.shields.io/badge/Helix-Editor-blueviolet?style=flat-square&logo=helix) 
![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)
![GitHub Stars](https://img.shields.io/github/stars/KrishnanKamatchi/Helix_Config?style=social)](https://github.com//KrishnanKamatchi/Helix_Config)  

## Overview

Helix is a modern, modal text editor inspired by Vim and Kakoune, built in Rust for speed and efficiency. This repository provides a **beginner-friendly configuration** for Helix that balances simplicity with powerful features, making it ideal for newcomers and advanced users alike.

This configuration includes:
- A clean, dark theme ("ao") for comfortable editing.
- Relative line numbers, cursor line highlighting, and true-color support.
- Auto-formatting, auto-saving, and smart completion.
- Custom keybindings for intuitive navigation and editing.
- Soft wrapping, indent guides, LSP inlay hints, and inline diagnostics.
- Optimized file and buffer pickers for efficient project navigation.

This open-source config is easy to set up and customize for your workflow.

## Features

### General Editor Settings
- **Theme**: "ao" (dark theme for reduced eye strain).
- **Line Numbers**: Relative for easy navigation (e.g., `5j` to jump 5 lines down).
- **Cursor Line**: Highlighted for better focus.
- **True Color**: Enabled for vibrant syntax highlighting.
- **Scroll Behavior**: 8 lines of scrolloff (context around cursor), 3 lines per scroll.
- **Mouse**: Disabled to encourage keyboard-driven workflow (toggle with `Space t`).
- **Auto-Format & Auto-Save**: Formats and saves files on focus loss or exit.
- **Completion**: Triggers after 2 characters, replaces on select, 500ms timeout.
- **Rulers**: Vertical lines at 80 and 120 characters for code style guides.
- **Gutters**: Displays diagnostics, line numbers, and spacing.
- **Bufferline**: Always visible for quick buffer switching.
- **Color Modes**: Enabled for language-specific highlighting.
- **Idle Timeout**: 1ms for responsive LSP/completion.
- **Popup Borders**: Around all popups for clarity.

### Cursor Shapes
- **Normal Mode**: Block cursor.
- **Insert Mode**: Bar cursor.
- **Select Mode**: Underline cursor.

### Soft Wrapping
- Enabled with a max wrap of 20 characters, retaining up to 40 characters of indent.

### Indent Guides
- Rendered as "┆" characters, visible at all indent levels.

### LSP (Language Server Protocol)
- Inlay hints displayed for better code understanding (e.g., type inferences).

### Inline Diagnostics
- Errors shown on cursor line; warnings on other lines.

### File Picker
- Hides hidden files, follows symlinks, deduplicates links.
- Respects `.gitignore`, includes parent directories, max depth of 4, and global Git ignore.

### Keybindings
#### Normal Mode
- **Space Key Prefix**:
  - `Space s`: Toggle soft-wrap.
  - `Space t`: Toggle true-color.
  - `Space f`: Open file picker.
  - `Space b`: Open buffer picker.
  - `Space q`: Quit.
  - `Space g`: Open lazygit (Git integration).
  - `Space w`: Save file.
  - `Space n`: New file.
  - `Space p`: Paste after cursor.
  - `Space d`: Delete selection.
  - `Space y`: Yank (copy).
  - `Space h`: Half page up.
  - `Space l`: Half page down.
- `C-s`: Save file.
- `C-q`: Quit.
- `C-o`: Open `~/.config/helix/config.toml`.
- `g a`: Code actions (LSP).
- `H`: Go to line start.
- `L`: Go to line end.
- `J`: Go to file end.
- `K`: Go to file start.
- `C c`: Toggle comments.

#### Insert Mode
- `C-Space`: Trigger completion.
- `C-s`: Save file.
- `C-z`: Undo.
- `C-y`: Redo.
- `C-c`: Switch to normal mode.

#### Select Mode
- `C-c`: Yank (copy).
- `C-x`: Delete selection.
- `C-v`: Paste after cursor.
- `C-a`: Select all.
- `C-d`: Delete selection.

## Installation and Setup

Follow these steps to install Helix and apply this configuration:

### Step 1: Install Helix
1. **Install Helix**:
   - On **Linux/macOS**:
     ```bash
     sudo snap install helix --classic
     ```
     Or use your package manager (e.g., `apt`, `brew`, `pacman`).
   - On **Windows**:
     Download the installer from the [Helix GitHub releases](https://github.com/helix-editor/helix/releases) or use a package manager like `winget` or `scoop`.
   - Verify installation:
     ```bash
     hx --version
     ```

2. **Optional**: Install `lazygit` for Git integration (`Space g`):
   ```bash
   brew install lazygit  # macOS
   sudo apt install lazygit  # Ubuntu/Debian
   ```

### Step 2: Set Up the Configuration
1. **Open Helix**:
   In your terminal, navigate to your project directory and launch Helix:
   ```bash
   helix .
   ```

2. **Open the Config File**:
   In Helix, open the configuration file:
   ```bash
   :config-open
   ```
   This opens `~/.config/helix/config.toml` in Helix.

3. **Paste the Configuration**:
   Copy the following configuration and paste it into the open `config.toml` file:

   ```toml
   theme = "ao"

   [editor]
   line-number = "relative"
   cursorline = true
   true-color = true
   scrolloff = 8
   scroll-lines = 3
   mouse = false
   auto-format = true
   auto-save = true
   completion-trigger-len = 2
   completion-replace = true
   completion-timeout = 500
   rulers = [80, 120]
   gutters = ["diagnostics", "line-numbers", "spacer"]
   bufferline = "always"
   color-modes = true
   idle-timeout = 1
   popup-border = "all"

   [editor.cursor-shape]
   normal = "block"
   insert = "bar"
   select = "underline"

   [editor.soft-wrap]
   enable = true
   max-wrap = 20
   max-indent-retain = 40

   [editor.indent-guides]
   render = true
   character = "┆"
   skip-levels = 0

   [editor.lsp]
   display-inlay-hints = true

   [editor.inline-diagnostics]
   cursor-line = "error"
   other-lines = "warning"

   [editor.file-picker]
   hidden = true
   follow-symlinks = true
   deduplicate-links = true
   git-ignore = true
   parents = true
   max-depth = 4
   git-global = true

   [keys.normal]
   space = { s = ":toggle soft-wrap.enable", t = ":toggle true-color", f = "file_picker", b = "buffer_picker", q = ":quit", g = ":sh lazygit", w = ":write", n = ":new", p = "paste_after", d = "delete_selection", y = "yank", "C-s" = ":write", "C-q" = ":quit", "C-o" = ":open ~/.config/helix/config.toml", h = "half_page_up", l = "half_page_down" }
   C-s = ":w"
   C-q = ":q"
   C-o = ":open ~/.config/helix/config.toml"
   g = { a = "code_action" }
   H = "goto_line_start"
   L = "goto_line_end"
   J = "goto_file_end"
   K = "goto_file_start"
   C = { c = "toggle_comments" }

   [keys.insert]
   "C-space" = "completion"
   "C-s" = ":w"
   "C-z" = "undo"
   "C-y" = "redo"
   "C-c" = "normal_mode"

   [keys.select]
   "C-c" = "yank"
   "C-x" = "delete_selection"
   "C-v" = "paste_after"
   "C-a" = "select_all"
   "C-d" = "delete_selection"
   ```

4. **Save and Apply**:
   - Save and close the file:
     ```bash
     :wq
     ```
   - Alternatively, reload the configuration without closing:
     ```bash
     :config-reload
     ```

5. **Verify**:
   Restart Helix (`helix .`) to ensure the settings are applied. Test keybindings like `Space f` (file picker) or `C-s` (save).

### Step 3: Customize (Optional)
- Edit `~/.config/helix/config.toml` to tweak settings (e.g., change `theme` or add new keybindings).
- Explore Helix documentation: `:help` in Helix or visit [helix-editor.com](https://helix-editor.com).

## Usage Tips
- **Navigation**: Use `hjkl` for arrow key movement in normal mode.
- **File Picker**: `Space f` to browse files; respects `.gitignore`.
- **Buffer Picker**: `Space b` to switch between open files.
- **LSP Support**: Install language servers (e.g., `rust-analyzer`, `typescript-language-server`) for enhanced autocompletion and diagnostics.
- **Git Integration**: `Space g` opens lazygit for Git operations.
- **Editing Config**: `C-o` quickly opens `config.toml` for changes.

## Contributing
This is an open-source project! To contribute:
1. Fork the repository.
2. Create a feature branch (`git checkout -b feature/awesome-change`).
3. Commit your changes (`git commit -m "Add awesome change"`).
4. Push to the branch (`git push origin feature/awesome-change`).
5. Open a pull request.

## License
This configuration is licensed under the [MIT License](LICENSE).

## Acknowledgments
- [Helix Editor](https://helix-editor.com) for an amazing text editor.
- The open-source community for inspiration and support.

Happy coding with Helix! 🚀
