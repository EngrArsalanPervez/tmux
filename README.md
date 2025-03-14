# tmux

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

##### Kill TMUX Completely

```bash
tmux kill-server
```
