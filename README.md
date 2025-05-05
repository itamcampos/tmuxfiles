# My tmux configuration files

I recommend using these settings on fresh tmux installations before any customization so that there are no conflicts with the current settings used by your system or your user.

By default tmux uses the `/etc/tmux.conf` configuration file to define its own global behavior. To define local behavior, only for the user, by default tmux uses the file `/home/<your user>/.tmux.conf` or just `~/.tmux.conf`.

The settings in this repository will be made to modify local behavior, only for your user. The tmux configuration file will be used in its default path at: `~/.tmux.conf` to point to the `~/.config/tmux/main.conf` file.

All tmux behavior in this repository will be defined within this file `~/.config/tmux/main.conf`.

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
echo -n "source-file ~/.config/tmux/config.conf" >> ~/.tmux.conf
```

Now, for everything to work, you must clone this repository in your user configuration folder on Linux, according to the [XDG Base Directory Specification](https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html). Still in your terminal, type:

```bash
git clone https://github.com/itamcampos/tmuxfiles ~/.config/tmux
```

Then:

```bash
git clone https://github.com/tmux-plugins/tpm ~/.config/tmux/plugins/tpm
```

To test, open a new session with tmux

```bash
tmux new -s main
```

Press **prefix** + **I** (capital I) to install the plugins. The default prefix is **`​​Ctrl+b`**, so it would be **`Ctrl+b`** + **`I`**.

- Save tmux environment: `prefix + Ctrl-s`
- Restore tmux environment: `prefix + Ctrl-r`

**To delete all saved sessions, remove the backup directories:**

```bash
rm -vrf ~/.tmux/plugins/tmux-continuum/*
rm -vrf ~/.tmux/plugins/tmux-resurrect/*
```

Restart tmux:

```bash
tmux kill-server 
```

**To erase all tmux settings:**

```bash
rm -vrf ~/.tmux/*
```

## References

 - [ArchLinux Docs](https://wiki.archlinux.org/title/tmux)
 - [Igor Irianto](https://dev.to/iggredible/useful-tmux-configuration-examples-k3g)
 - [Serhat Teker](https://dev.to/serhatteker/restore-tmux-sessions-after-reboot-7g6)
 - [XDG Base Directory Specification](https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html)
 - [Tmux Resurrect](https://github.com/tmux-plugins/tmux-resurrect)
 - [Tmux Continuum](https://github.com/tmux-plugins/tmux-continuum)
