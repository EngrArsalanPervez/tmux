# tmux

## Installation

```bash
sudo apt install tmux
```

### Theme Installation

[catppuccin](https://github.com/catppuccin/tmux)

```bash
# Local Terminal theme should be : Gnome Dark
Theme Source: catppuccin (https://github.com/catppuccin/tmux)

mkdir -p ~/.config/tmux/plugins/catppuccin
git clone -b v2.1.2 https://github.com/catppuccin/tmux.git ~/.config/tmux/plugins/catppuccin/tmux
```

### ~/.tmux.conf

```bash
# ~/.tmux.conf

set -g @catppuccin_window_default_text "#W"
set -g @catppuccin_window_current_text "#W"
set -g @catppuccin_window_text "#W"


# Options to make tmux more pleasant
set -g mouse on
set -g default-terminal "tmux-256color"

# Configure the catppuccin plugin
set -g @catppuccin_flavor "mocha"
set -g @catppuccin_window_status_style "rounded"

# Load catppuccin
run ~/.config/tmux/plugins/catppuccin/tmux/catppuccin.tmux
# For TPM, instead use `run ~/.tmux/plugins/tmux/catppuccin.tmux`

# Make the status line pretty and add some modules
set -g status-right-length 100
set -g status-left-length 100
set -g status-left ""
set -g status-right "#{E:@catppuccin_status_application}"
set -agF status-right "#{E:@catppuccin_status_cpu}"
set -ag status-right "#{E:@catppuccin_status_session}"
set -ag status-right "#{E:@catppuccin_status_uptime}"
set -agF status-right "#{E:@catppuccin_status_battery}"

run ~/.config/tmux/plugins/tmux-plugins/tmux-cpu/cpu.tmux
run ~/.config/tmux/plugins/tmux-plugins/tmux-battery/battery.tmux
# Or, if using TPM, just run TPM
```

### Apply Theme

```bash
tmux source-file ~/.tmux.conf
tmux source ~/.tmux.conf
tmux
```

### Key Bindings

##### Tmux Sessions

```bash
# List Running sessions
tmux ls

# Start a new session
tmux

# Start a named session
tmux new -s mysession

# Re attach to a running session
tmux attach -t mysession

# kill a session
tmux kill-session -t mysession
```

##### Tmux Tabs/Windows

```bash
# New Window
Ctrl + b, then c

# Switch Windows
Ctrl + b, then n (next) or p (previous)

# List windows
Ctrl + b, then w

# Rename a window
Ctrl + b, then , (comma)
```

##### Tmux Panes

```bash
# Split horizontally
Ctrl + b, then %

# Split vertically
# Ctrl + b, then "

# Switch between panes
Ctrl + b, then arrow keys

# Resize panes
Ctrl + b, then Hold Ctrl + arrow keys

# Close a pane
Ctrl + d (or exit command in the pane)
```

##### Copy/Paste

```bash
Enter scroll mode: Ctrl + b, then [
Scroll with arrow keys
Select text: Press Ctrl + space for selecting text
Copy test: Press Ctrl + w
Paste text: Ctrl + b, then ]
```

##### Detach Tmux

```bash
Ctrl + Shift + b, then d
```

##### Kill TMUX Completely

```bash
tmux kill-server
```

##### Cheat Sheet

[Cheat Sheet](https://tmuxcheatsheet.com/)
