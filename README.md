# My tmux configuration files

I recommend using these settings on fresh tmux installations before any customization so that there are no conflicts with the current settings used by your system or your user.

By default tmux uses the `/etc/tmux.conf` configuration file to define its own global behavior. To define local behavior, only for the user, by default tmux uses the file `/home/<your user>/.tmux.conf` or just `~/.tmux.conf`.

The settings in this repository will be made to modify local behavior, only for your user. The tmux configuration file will be used in its default path at: `~/.tmux.conf` to point to the `~/.config/tmux/tmux_user.conf` file.

All tmux behavior in this repository will be defined within this file `~/.config/tmux/tmux_user.conf`.


## Features included in this repository

- Manual installation of [Tmux Resurrect](https://github.com/tmux-plugins/tmux-resurrect) to allow sessions to persist after system shutdown. This plugin was also installed using the official repository when it was still at this [commit](https://github.com/tmux-plugins/tmux-resurrect/commit/cff343cf9e81983d3da0c8562b01616f12e8d548). Click [here](https://github.com/tmux-plugins/tmux-resurrect/commit/cff343cf9e81983d3da0c8562b01616f12e8d548) to see the latest fix for this plugin, if it's still up, obviously.

- Manual installation of [Tmux Continuum](https://github.com/tmux-plugins/tmux-continuum) to start tmux automatically after the computer/server is turned on. This plugin was installed using the official repository when it was still at this [commit](https://github.com/tmux-plugins/tmux-continuum/commit/0698e8f4b17d6454c71bf5212895ec055c578da0). Click [here](https://github.com/tmux-plugins/tmux-continuum/commit/0698e8f4b17d6454c71bf5212895ec055c578da0) to see the latest fix for this plugin.


## How to use

To create the default tmux configuration file, type in your terminal:

```bash
touch ~/.tmux.conf
```

Still in your terminal, set the path to the new tmux configuration file:

```bash
echo -n "source-file ~/.config/tmux/tmux_user.conf" >> ~/.tmux.conf
```

Now, for everything to work, you must clone this repository in your user configuration folder on Linux, according to the [XDG Base Directory Specification](https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html). Still in your terminal, type:

```bash
git clone https://github.com/itamcampos/tmuxfiles ~/.config/tmux
```

To test, open a new session with tmux

```bash
tmux new -s test
```

## Important note

The tmux settings in this repository don't use plugin manager, but that could change, who knows.


## References

- [ArchLinux Docs](https://wiki.archlinux.org/title/tmux)
- [Igor Irianto](https://dev.to/iggredible/useful-tmux-configuration-examples-k3g)
- [Serhat Teker](https://dev.to/serhatteker/restore-tmux-sessions-after-reboot-7g6)
- [XDG Base Directory Specification](https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html)a
- [Tmux Resurrect](https://github.com/tmux-plugins/tmux-resurrect)
- [Tmux Continuum](https://github.com/tmux-plugins/tmux-continuum)
