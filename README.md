# My tmux configuration files

I recommend using these settings on fresh tmux installations before any customization so that there are no conflicts with the current settings used by your system or your user.

By default tmux uses the `/etc/tmux.conf` configuration file to define its own global behavior. To define local behavior, only for the user, by default tmux uses the file `/home/<your user>/.tmux.conf` or just `~/.tmux.conf`.

The settings in this repository will be made to modify local behavior, only for your user. The tmux configuration file will be used in its default path at: `~/.tmux.conf` to point to the `~/.tmux/main.conf` file.

All tmux behavior in this repository will be defined within this file `~/.tmux/main.conf`.

## Features Included

- Plugin [Tmux Resurrect](https://github.com/tmux-plugins/tmux-resurrect) to allow sessions to persist after system shutdown.
- Plugin [Tmux Continuum](https://github.com/tmux-plugins/tmux-continuum) to start tmux automatically after the computer/server is turned on.

## How to Use

To create the default tmux configuration file, type in your terminal:

```bash
touch ~/.tmux.conf
```

Still in your terminal, set the path to the new tmux configuration file:

```bash
echo -n "source-file ~/.tmux/tmux.conf" >> ~/.tmux.conf
```

Now, for everything to work, you must clone this repository in your user configuration folder on Linux, according to the [XDG Base Directory Specification](https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html). Still in your terminal, type:

```bash
git clone https://github.com/itamcampos/tmuxfiles ~/.tmux
```

Then:

```bash
mkdir -p ~/.tmux/plugins
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
```

Ensure the tpm script has execute permissions. You can set this using `find` `+` `chmod`:

```bash
# Dar todas as permissões necessárias
find ~/.tmux/plugins/tpm -type f \( -name "*.sh" -o -path "*/bin/*" -o -path "*/bindings/*" \) -exec chmod +x {} \;
```

To test, open a new session with tmux

```bash
tmux new -s main
```

### Installing plugins

1. Add new plugin to `~/.tmux/tmux.conf` with `set -g @plugin '...'`

2. Press **prefix** + **I** (capital I) to install the plugins. The default prefix is **`​​Ctrl+b`**, so it would be **`Ctrl+b`** + **`I`**.

### Other operations

- Save tmux environment: `prefix + Ctrl-s`
- Restore tmux environment: `prefix + Ctrl-r`

To delete all saved sessions, remove the backup directories:

```bash
rm -vrf ~/.tmux/plugins/tmux-continuum/*
rm -vrf ~/.tmux/plugins/tmux-resurrect/*
```

Restart tmux:

```bash
tmux kill-server
```

To erase all tmux settings:

```bash
rm -vrf ~/.tmux/*
```

## Troubleshooting

This section provides several methods to resolve issues related to Tmux Plugin Manager (TPM) and plugin installation.

### 1. Automated Installation via a Temporary Session (Recommended)

This method simulates the standard installation process within a clean, temporary tmux session to resolve potential conflicts.

```sh
# Terminate any existing tmux server instances to ensure a clean state.
tmux kill-server

# Give execute permission to all TPM scripts
chmod +x ~/.tmux/plugins/tpm/tpm
chmod +x ~/.tmux/plugins/tpm/bin/*
chmod +x ~/.tmux/plugins/tpm/bindings/*
chmod +x ~/.tmux/plugins/tpm/scripts/*

# Or do it all at once:
find ~/.tmux/plugins/tpm -type f -name "*.sh" -exec chmod +x {} \;
find ~/.tmux/plugins/tpm -type f -path "*/bin/*" -exec chmod +x {} \;
find ~/.tmux/plugins/tpm -type f -path "*/bindings/*" -exec chmod +x {} \;

# Or take a more concise approach
find ~/.tmux/plugins/tpm -type f \( -name "*.sh" -o -path "*/bin/*" -o -path "*/bindings/*" \) -exec chmod +x {} \;

# Launch a new, detached session named 'temp'.
tmux new-session -d -s temp

# Source the configuration file and then send the key-binding (prefix + I) to trigger the installation.
tmux send-keys -t temp 'tmux source-file ~/.tmux.conf' Enter
sleep 10 # Allow time for the configuration to be sourced.
tmux send-keys -t temp C-b I

# Wait for the installation process to complete. This may take some time.
sleep 10

# Verify that the plugin directories have been created.
ls -la ~/.tmux/plugins/

# Clean up by terminating the temporary session.
tmux kill-session -t temp
```

### 2. Direct Script Execution

This is often the most reliable method as it directly invokes the TPM installation script, bypassing potential issues with session state or key-bindings.

```sh
# Set the environment variable required by the installation script.
export TMUX_PLUGIN_MANAGER_PATH="$HOME/.tmux/plugins/"

# Execute the installation script directly.
~/.tmux/plugins/tpm/scripts/install_plugins.sh
```

### 3. Complete Reinstallation of TPM

If the above methods fail, a complete reinstallation of the Tmux Plugin Manager can resolve corruption or deep-seated configuration issues.

```sh
# Remove the current TPM installation directory.
rm -rf ~/.tmux/plugins/tpm

# Clone a fresh copy of the TPM repository from GitHub.
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm

# Ensure all newly downloaded scripts and binaries are executable.
find ~/.tmux/plugins/tpm -type f \( -name "*.sh" -o -path "*/bin/*" -o -path "*/bindings/*" \) -exec chmod +x {} \;

# Test the new installation by starting a new tmux session.
tmux kill-server
tmux new -s main
```

## References

 - [ArchLinux Docs](https://wiki.archlinux.org/title/tmux)
 - [Igor Irianto](https://dev.to/iggredible/useful-tmux-configuration-examples-k3g)
 - [Serhat Teker](https://dev.to/serhatteker/restore-tmux-sessions-after-reboot-7g6)
 - [XDG Base Directory Specification](https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html)
 - [Tmux Resurrect](https://github.com/tmux-plugins/tmux-resurrect)
 - [Tmux Continuum](https://github.com/tmux-plugins/tmux-continuum)

