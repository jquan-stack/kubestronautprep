## 🐧 Essential Linux & Vim Commands for CKA

### 🔧 Linux CLI Essentials

```bash
# Navigate to directory
cd /etc/kubernetes/             # Go to kubeadm config dir

# View file content
cat config.yaml                 # Print file content
less config.yaml                # View with scroll support

# Edit YAML quickly
nano pod.yaml                   # Use nano editor (simpler than vim)

# View running processes
ps aux | grep kube              # Filter kube-related processes

# View disk and resource usage
free -m                         # Memory in MB
df -h                           # Disk usage in human-readable

# Network info
ip a                            # Show IP addresses
netstat -tulnp                  # View open ports (requires net-tools)
ss -tulwn                       # Alternative to netstat

# Logs
journalctl -u kubelet          # Systemd logs for kubelet

# Search in files
grep -i error config.yaml       # Case-insensitive search for "error"
```

### 🧠 Vim Quick Reference

```vim
# Enter insert mode
i             # Insert before cursor
I             # Insert at beginning of line

# Save & exit
:w            # Save file
:q            # Quit vim
:wq           # Save and quit
:q!           # Quit without saving

# Navigation
G             # Go to last line
gg            # Go to first line
:num          # Go to line number `num`

# Copy/Paste
yy            # Copy (yank) line
dd            # Delete line
p             # Paste below cursor

# Search
/word         # Search forward for 'word'
n             # Repeat search forward
N             # Repeat search backward

# Undo/Redo
u             # Undo
Ctrl + r      # Redo
```

> ✅ Tip: Use `vim -R file.yaml` for read-only mode to avoid accidental changes.

### 🧰 YAML Formatting Helpers

```bash
# Lint YAML
yamllint pod.yaml                # Validate YAML structure (install yamllint)

# Visualize structure
cat pod.yaml | yq .             # Pretty-print YAML (yq required)
```

These commands are designed to quickly troubleshoot, inspect, and edit Kubernetes cluster components efficiently under exam constraints.
