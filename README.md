# tmux

## Installation

```bash
sudo apt install tmux
```

### Minimal ~/.tmux.conf

```bash
setw -g mouse on 
set-option -ga terminal-overrides ",xterm-256color:Tc"
set -g default-terminal "xterm-256color"
```

### Themes

```bash
# Ubuntu
mkdir -p ${XDG_DATA_HOME:-$HOME/.local/share}/warp-terminal
cd ${XDG_DATA_HOME:-$HOME/.local/share}/warp-terminal/
git clone https://github.com/warpdotdev/themes.git

# Windows
New-Item -Path "$env:APPDATA\warp\Warp\data\" -ItemType Directory
Set-Location -Path $env:APPDATA\warp\Warp\data\
git clone https://github.com/warpdotdev/themes.git
```

### Plugins

```bash
mkdir -p ~/.config/tmux/plugins/tmux-plugins
git clone https://github.com/tmux-plugins/tmux-cpu ~/.config/tmux/plugins/tmux-plugins/tmux-cpu
git clone https://github.com/tmux-plugins/tmux-battery ~/.config/tmux/plugins/tmux-plugins/tmux-battery
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


### nano tmux.sh

```bash
#!/bin/bash

# Name of the tmux session
SESSION_NAME="dpi"

# Check if the session already exists
tmux has-session -t $SESSION_NAME 2>/dev/null

# If the session doesn't exist, create it
if [ $? != 0 ]; then
    # Create the :0 window (tab)
    tmux new-session -d -s $SESSION_NAME -n "API"
    tmux send-keys -t $SESSION_NAME:0 "cd /root/DPI/pace2_api/" Enter

    # Create the :1 window (tab)
    tmux new-window -t $SESSION_NAME:1 -n "systemMonitoring"
    tmux send-keys -t $SESSION_NAME:1 "cd /root/DPI/pace2_go_system_monitoring/" Enter

    # Create the :2 window (tab)
    tmux new-window -t $SESSION_NAME:2 -n "snmp"
    tmux send-keys -t $SESSION_NAME:2 "cd /root/DPI/pace2_snmp/" Enter

    # Create the :3 window (tab)
    tmux new-window -t $SESSION_NAME:3 -n "netdisco"
    tmux send-keys -t $SESSION_NAME:3 "su netdisco" Enter
    tmux send-keys -t $SESSION_NAME:3 "cd /home/netdisco/environments/" Enter

    # Create the :4 window (tab)
    tmux new-window -t $SESSION_NAME:4 -n "dpdk"
    tmux send-keys -t $SESSION_NAME:4 "cd /root/DPI/guide/dpdk-stable-23.11.1" Enter
    tmux send-keys -t $SESSION_NAME:4 "./usertools/dpdk-devbind.py -s" Enter

    # Create the :5 window (tab)
    tmux new-window -t $SESSION_NAME:5 -n "git"
    tmux send-keys -t $SESSION_NAME:5 "cd /root/DPI/pace2_dpdk_dpi/" Enter

    # Create the :6 window (tab)
    tmux new-window -t $SESSION_NAME:6 -n "script"
    tmux send-keys -t $SESSION_NAME:6 "cd /root/DPI/pace2_dpdk_dpi/examples/l2fwd_dpi/scripts/" Enter

    # Create the :7 window (tab)
    tmux new-window -t $SESSION_NAME:7 -n "pace2"
    tmux send-keys -t $SESSION_NAME:7 "cd /root/DPI/pace2_dpdk_dpi/examples/l2fwd_dpi/scripts/" Enter

    # Create the :8 window (tab) - fixed numbering issue
    tmux new-window -t $SESSION_NAME:8 -n "monitor"
    tmux send-keys -t $SESSION_NAME:8 "cd /root/DPI/pace2_dpdk_dpi/examples/l2fwd_dpi/scripts/" Enter

    # Create the :9 window (tab)
    tmux new-window -t $SESSION_NAME:9 -n "htop"
    tmux send-keys -t $SESSION_NAME:9 "htop" Enter

    # Create the :10 window (tab)
    tmux new-window -t $SESSION_NAME:10 -n "bash"
    tmux send-keys -t $SESSION_NAME:10 "cd" Enter

    # Create the :11 window (tab)
    tmux new-window -t $SESSION_NAME:11 -n "primary"
    tmux send-keys -t $SESSION_NAME:11 "sshpass -p '*****' ssh -o StrictHostKeyChecking=accept-new user@X.X.X.X -p X" Enter

    # Select the 0 window
    tmux select-window -t $SESSION_NAME:0

    echo "New tmux session '$SESSION_NAME' created with 11 tabs running different scripts."
else
    echo "Session '$SESSION_NAME' already exists. Attaching to it..."
fi

# Attach to the session
tmux attach-session -t $SESSION_NAME
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
