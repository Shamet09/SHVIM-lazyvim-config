# SHVIM - Custom Neovim Setup

A customized Neovim configuration based on LazyVim for C, Python, and Assembly development with cybersecurity tools support.

![SHVIM Dashboard](https://img.shields.io/badge/Editor-Neovim-green?style=for-the-badge&logo=neovim)

## 🚀 Features

- **Custom SHVIM dashboard** with fuzzy finder integration
- **C/C++ development** with clangd LSP and debugging (GDB)
- **Python development** with pyright LSP and debugging (debugpy)
- **Assembly (NASM)** support with syntax highlighting and LSP
- **Full debugging support** with DAP (Debug Adapter Protocol)
- **Transparent background** support
- **Custom keybindings** for quick compile/run
- **Fuzzy finding** with Telescope (optimized for WSL)
- **Git integration** with Fugitive and Gitsigns
- **Terminal integration** with ToggleTerm
- **Hex editor** for binary analysis
- **Database UI** for SQL work
- **REST client** for API testing
- **Diff viewer** for file/git comparisons

---

## 📋 Prerequisites

### System: Fedora (WSL2 or native)

**Windows WSL Setup** (if using WSL):
```bash
# Install Fedora WSL
wsl --install -d Fedora

# Or if another distro is already installed, remove it first:
wsl --unregister Ubuntu
wsl --install -d Fedora
```

---

## 🔧 Installation Steps

### 1. System Update & Essential Packages

```bash
# Update system
sudo dnf update -y

# Install development tools
sudo dnf groupinstall "Development Tools" "C Development Tools and Libraries" -y

# Install essential tools
sudo dnf install gcc gcc-c++ make cmake gdb git curl wget ripgrep fd-find fzf -y

# Install Python tools
sudo dnf install python3 python3-pip python3-devel python3-neovim -y

# Install Neovim
sudo dnf install neovim -y
```

### 2. Programming Language Support

#### C/C++ Development
```bash
# Install clang and clangd
sudo dnf install clang clang-tools-extra -y

# Install GDB for debugging
sudo dnf install gdb -y
```

#### Python Development
```bash
# Install Python LSP and tools
pip3 install --user python-lsp-server[all] debugpy pyright black isort ruff pylint

# Install pynvim (Neovim Python provider)
pip3 install --user pynvim
```

#### Assembly (NASM)
```bash
sudo dnf install nasm -y

# Optional: Assembly LSP (requires Rust/Cargo)
# cargo install asm-lsp
```

### 3. Additional Tools

#### Lua 5.1 (Required for some plugins)
```bash
sudo dnf install -y lua5.1 lua5.1-devel luarocks
```

#### Security/Pentesting Tools (Optional)
```bash
# Install security tools
sudo dnf install nmap wireshark -y
```

#### Multimedia & Utilities (Optional)
```bash
# For media playback
sudo dnf install mpv aria2 ffmpeg --allowerasing -y
```

### 4. RPM Fusion Repositories (for ffmpeg and extras)

```bash
sudo dnf install https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm -y
```

---

## 🎨 Neovim Setup

### 1. Install LazyVim Starter

```bash
# Backup existing config (if any)
mv ~/.config/nvim{,.bak}
mv ~/.local/share/nvim{,.bak}
mv ~/.local/state/nvim{,.bak}
mv ~/.cache/nvim{,.bak}

# Clone LazyVim starter
git clone https://github.com/LazyVim/starter ~/.config/nvim
rm -rf ~/.config/nvim/.git
```

### 2. Clone Your SHVIM Config

```bash
# Remove the default config
rm -rf ~/.config/nvim

# Clone your SHVIM config from GitHub
git clone https://github.com/Shamet09/nvim-config.git ~/.config/nvim
```

### 3. Install Plugins

```bash
# Start Neovim (plugins will auto-install)
nvim

# Inside nvim, plugins will automatically install via Lazy
# Wait for all plugins to finish installing

# Then run:
:Lazy sync
```

**Note:** The Python and C/C++ language extras are already configured in `cybersec.lua`, so you don't need to manually enable them via `:LazyExtras`.

---

## 🎯 Configuration Files Structure

```
~/.config/nvim/
├── lua/
│   ├── config/
│   │   ├── autocmds.lua       # Auto commands
│   │   ├── keymaps.lua        # Custom keybindings
│   │   ├── lazy.lua           # Lazy.nvim setup
│   │   └── options.lua        # Neovim options
│   └── plugins/
│       ├── asm.lua            # Assembly language support
│       ├── colorscheme.lua    # Theme configuration (transparent)
│       ├── cybersec.lua       # Python/C extras, security tools
│       ├── dashboard.lua      # SHVIM dashboard
│       ├── debugging.lua      # DAP debugging setup
│       ├── enhancements.lua   # UI enhancements, tools
│       ├── python-config.lua  # Python LSP configuration
│       └── user.lua           # User plugins (git, terminal, hex, db)
├── .gitignore
└── init.lua                   # Main entry point
```

---

## ⌨️ Keybindings

### General
| Key | Action |
|-----|--------|
| `jk` or `kj` | Exit insert/visual mode |
| `<leader>` | Space (leader key) |
| `<C-s>` | Save file |
| `<leader>w` | Save file |
| `<leader>q` | Quit |
| `<leader>h` | Clear search highlighting |

### Dashboard (SHVIM Start Screen)
| Key | Action |
|-----|--------|
| `f` | Find files (fuzzy) |
| `r` | Recent files |
| `g` | Find text (grep) |
| `n` | New file |
| `c` | Config files |
| `s` | Restore session |
| `x` | Lazy extras |
| `l` | Lazy plugin manager |
| `q` | Quit |

### File Navigation
| Key | Action |
|-----|--------|
| `<leader>ff` or `Space-f-f` | Find files (Telescope) |
| `<leader>fg` | Live grep (find text in files) |
| `<leader>fr` | Recent files |
| `<leader>fb` | File browser |
| `<leader>ft` | Find TODOs |
| `<leader>e` | Toggle file explorer (Neo-tree) |

### Code Running & Compilation
| Key | Action |
|-----|--------|
| `F5` or `<leader>rp` | Run Python file in terminal |
| `F6` or `<leader>rc` | Compile & run C file |
| `F7` | Compile & run C (safe with spaces in filename) |
| `<leader>cc` | Compile C file only |
| `<leader>cd` | Compile C with debug symbols (-g) |

### Debugging
| Key | Action |
|-----|--------|
| `F9` | Toggle breakpoint |
| `<leader>dc` | Start/Continue debugging |
| `F10` | Step over |
| `F11` | Step into |
| `F12` | Step out |
| `<leader>dt` | Terminate debug session |
| `<leader>du` | Toggle debug UI |

### Terminal
| Key | Action |
|-----|--------|
| `<leader>tt` | Toggle terminal |
| `Ctrl+/` | Toggle floating terminal |
| `Ctrl+\` | Toggle terminal (if configured) |

### Code Navigation
| Key | Action |
|-----|--------|
| `gd` | Go to definition |
| `gr` | Find references |
| `K` | Hover documentation |
| `<leader>ca` | Code actions |
| `<leader>rn` | Rename symbol |
| `]d` | Next diagnostic |
| `[d` | Previous diagnostic |
| `<leader>o` | Toggle code outline (Aerial) |
| `<leader>xx` | Show all diagnostics (Trouble) |
| `<leader>u` | Undo tree |

### Editing
| Key | Action |
|-----|--------|
| `gcc` | Comment/uncomment line |
| `gc` (visual) | Comment selection |
| `<C-n>` | Start multiple cursors |
| `<` (visual) | Indent left (stays in visual) |
| `>` (visual) | Indent right (stays in visual) |
| `<A-j>` | Move line down |
| `<A-k>` | Move line up |
| `p` (visual) | Paste without yanking replaced text |

### Git
| Key | Action |
|-----|--------|
| `<leader>gb` | Toggle git blame |
| `<leader>gd` | Open diff view |
| `<leader>gq` | Close diff view |
| `]c` | Next git change |
| `[c` | Previous git change |
| `:Git` | Git commands (Fugitive) |

### Cybersecurity Tools
| Key | Action |
|-----|--------|
| `<leader>hx` | Toggle hex view |
| `<leader>db` | Toggle database UI |
| `<leader>rr` | Run REST request (in .http files) |
| `<leader>rx` | Explain regex under cursor |

---

## 🎨 Customization

### Transparent Background

The config includes transparent background support. Make sure your terminal supports transparency:

**Windows Terminal:**
- Settings → Appearance → Acrylic opacity/transparency

Transparency is configured in `colorscheme.lua` with `transparent_background = true`.

### Nerd Fonts

Icons require a Nerd Font installed:

1. Download: [Nerd Fonts](https://www.nerdfonts.com/font-downloads)
2. Install the `.ttf` files
3. Set in Windows Terminal: Settings → Profile → Appearance → Font face

**Recommended fonts:**
- JetBrainsMono Nerd Font
- FiraCode Nerd Font
- Hack Nerd Font

---

## 📦 Installed Plugins

### Core
- **LazyVim** - Neovim distribution
- **lazy.nvim** - Plugin manager
- **telescope.nvim** - Fuzzy finder
- **telescope-fzf-native.nvim** - FZF algorithm for faster searches
- **telescope-file-browser.nvim** - File browser extension
- **nvim-treesitter** - Syntax highlighting

### Dashboard & UI
- **dashboard-nvim** - Custom SHVIM dashboard
- **nvim-web-devicons** - File icons
- **indent-blankline.nvim** - Indent guides
- **nvim-colorizer.lua** - Color highlighter

### Language Support & LSP
- **nvim-lspconfig** - LSP configurations
- **clangd** - C/C++ LSP
- **pyright** - Python LSP
- **asm-lsp** - Assembly LSP (optional)
- **black**, **isort**, **ruff** - Python formatters/linters
- **clang-format** - C/C++ formatter

### Debugging (DAP)
- **nvim-dap** - Debug Adapter Protocol client
- **nvim-dap-ui** - Debug UI
- **nvim-dap-virtual-text** - Shows variable values inline
- **nvim-dap-python** - Python debugging adapter
- GDB adapter for C/C++ debugging

### Development Tools
- **toggleterm.nvim** - Terminal integration
- **vim-fugitive** - Git integration
- **gitsigns.nvim** - Git signs in gutter + blame
- **nvim-autopairs** - Auto close brackets
- **nvim-surround** - Surround text operations
- **Comment.nvim** - Better commenting
- **vim-visual-multi** - Multiple cursors

### Navigation & Search
- **trouble.nvim** - Diagnostics/quickfix list
- **aerial.nvim** - Code outline/structure
- **todo-comments.nvim** - TODO highlighting and search
- **undotree** - Undo history visualizer

### Cybersecurity Tools
- **hex.nvim** - Hex editor for binary analysis
- **vim-dadbod-ui** - Database viewer/manager
- **rest-nvim** - REST API client
- **diffview.nvim** - Advanced diff viewer
- **nvim-regexplainer** - Regex pattern explainer
- **nvim-bqf** - Better quickfix window

---

## 🛠 Troubleshooting

### Icons not showing
```bash
# Make sure you have a Nerd Font installed and set in your terminal
# Verify in Neovim:
:checkhealth
```

### Python provider errors
```bash
pip3 install --user pynvim
```

### LSP not working
```bash
# Open Neovim and check LSP status
nvim test.py
:LspInfo

# Check Mason (language server installer)
:Mason
```

### Debugging not working
```bash
# Make sure debugpy is installed
pip3 install --user debugpy

# For C debugging, make sure gdb is installed
sudo dnf install gdb

# Check DAP status in Neovim
:checkhealth dap
```

### DNS issues in WSL (can't reach GitHub)
```bash
sudo bash -c 'echo "nameserver 8.8.8.8" > /etc/resolv.conf'
sudo bash -c 'echo "nameserver 8.8.4.4" >> /etc/resolv.conf'
```

### Git lock errors
```bash
rm -f ~/.local/share/nvim/lazy/*/.git/index.lock
```

### Plugin errors after update
```bash
# Clean reinstall
rm -rf ~/.local/share/nvim/lazy
nvim
:Lazy sync
```

### Slow file finding in WSL
```bash
# IMPORTANT: Work in Linux filesystem, not Windows
# Slow:
cd /mnt/c/Users/YourName/projects  # ❌ Windows filesystem

# Fast:
cd ~/projects                       # ✅ Linux filesystem
nvim
```

The config automatically ignores `/mnt/*` for better performance.

---

## 📁 Recommended Directory Structure

```bash
# Create organized workspace in Linux filesystem (fast)
mkdir -p ~/projects
mkdir -p ~/school
mkdir -p ~/.config

# Example project structure
~/projects/
├── password-project/
├── c-programs/
├── python-scripts/
└── ctf-challenges/
```

**WSL Performance Tip:** Keep your active projects in `~/` (Linux filesystem), not `/mnt/c/` (Windows). The speed difference is significant!

---

## 🔄 Updating

### Update Neovim plugins
```bash
nvim
:Lazy update
```

### Update your config from GitHub
```bash
cd ~/.config/nvim
git pull
nvim
:Lazy sync
```

### Push config changes to GitHub
```bash
cd ~/.config/nvim
git add .
git commit -m "Description of changes"
git push
```

### Update system packages
```bash
sudo dnf update -y
```

### Update Fedora version (when new release)
```bash
sudo dnf system-upgrade download --releasever=XX
sudo dnf system-upgrade reboot
```

---

## 📝 Notes

- **WSL Performance:** Always work in `~/` (Linux filesystem) not `/mnt/c/` for better performance
- **Memory:** WSL only uses memory when running. Use `wsl --shutdown` to free memory when done
- **Python Provider:** If you get Python errors, run `pip3 install --user pynvim`
- **Compilation:** 
  - C files: `gcc filename.c -o filename`
  - Assembly: `nasm -f elf64 filename.asm -o filename.o && ld filename.o -o filename`
- **Debugging:**
  - Python: Uses `debugpy` (installed via pip)
  - C/C++: Uses GDB
  - Set breakpoints with `F9`, start with `Space-d-c`

---

## 🎓 Learning Resources

### Vim Motions
```vim
# Built-in interactive tutorial
:Tutor
```

### Help System
```vim
:help <topic>
:help keymaps
:help lsp
```

### Recommended Learning Path
1. **Week 1:** Master basic motions (`hjkl`, `w`, `b`, `0`, `$`, `gg`, `G`)
2. **Week 2:** Learn editing (`d`, `y`, `p`, `c`, `i`, `a`, `o`)
3. **Week 3:** Practice on real projects (use it daily!)
4. **Week 4:** Explore advanced features (LSP, debugging, git)

---

## 🤝 Contributing

This is a personal config, but feel free to fork and customize for your needs!

To contribute improvements:
1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

---

## 📜 License

MIT License - Feel free to use and modify

---

## 🙏 Credits

- [LazyVim](https://github.com/LazyVim/LazyVim) - Base configuration
- [Neovim](https://neovim.io/) - The amazing editor
- All plugin authors for their incredible work

---

**Last Updated:** January 2026  
**Tested On:** Fedora (WSL2), Windows 11  
**Neovim Version:** 0.9+  
**Repository:** [github.com/Shamet09/nvim-config](https://github.com/Shamet09/nvim-config)
