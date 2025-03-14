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

##### Tmux Panes

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
