# Setup

The steps to take when setting up a new linux machine (for The Odin Project specifically, but many are also in general).

- ...
- install [Browsersync](https://browsersync.io/) (`npm install -g browser-sync`)
- [Set an alias to pull multiple git repos at once](https://dev.to/rmpato/git-pull-multiple-repositories-at-once-4l68) ("multipull")
- ...

## VSCodium

### Terminal Setup

Add the following to `settings.json` (probably in `/home/cobbland/.var/app/com.vscodium.codium/config/VSCodium/User/`):

```
  {
    "terminal.integrated.defaultProfile.linux": "bash",
    "terminal.integrated.profiles.linux": {
      "bash": {
        "path": "/app/bin/host-spawn",
        "args": ["bash"],
        "icon": "terminal-bash",
        "overrideName": true
      }
    },
  }
```

*Source: https://github.com/flathub/com.vscodium.codium#host-shell*

### Extensions

- Code Spell Checker
- ESLint
- Prettier - Code for...
- vscode-pdf

## Appimage Setup

*Instead of the following, you could also just use [Gear Lever](https://gearlever.mijorus.it) or [AppImageLauncher](https://github.com/TheAssassin/AppImageLauncher).*

- Make executable: `sudo chmod +x *.AppImage`.
- Run the file: `./"name of file (without quotation marks)"`
- Using the `mount` command, find where the appimage is mounted.
- Navigate to the mounted folder.
- Copy the icon file to `~/.local/share/icons/` and the .desktop file to `~/.local/share/applications/`.
- Edit the `.desktop` file to point to the appimage executable and the copied icon.

## Keyboard Remapping & Layers

Use [keyd](https://github.com/rvaiya/keyd) to remap keys and add layers.

Start with: `sudo systemctl enable --now keyd`

End by pressing `backspace+escape+enter`

My current config (which goes in `/etc/keyd/default.conf`):

```
[ids]

*

[main]

# Capslock as backspace
capslock = backspace

# Activate nav layers
a = overloadt(nav, a, 200)
; = overloadt(navleft, ;, 200)

# Shift bar
space = overloadt(shift, space, 200)

# Home row mods
s = overloadt(control, s, 200)
d = overloadt(meta, d, 200)
f = overloadt(alt, f, 200)
j = overloadt(alt, j, 200)
k = overloadt(meta, k, 200)
l = overloadt(control, l, 200)
# v = overloadt(altgr, v, 200)
# m = overloadt(altgr, m, 200)
# Both of the above were commented out because they've been causing me issues.

[nav]

g = capslock
h = backspace
j = left
i = up
k = down
l = right
; = home
' = end

[navleft]

e = up
s = left
d = down
f = right
g = backspace
h = capslock
```

*This is still a work in progress.*

*If I need cross-platform or more functionality, check out [kanata](https://github.com/jtroo/kanata) or [kmonad](https://github.com/kmonad/kmonad).*

## Aliases

Aliases added to `~/.bash_aliases`:

```bash
alias multipull="find . -mindepth 1 -maxdepth 1 -type d -print -exec git -C {} pull \;"
alias gg="git log --oneline --abbrev-commit --all --graph --decorate --color"
alias startkeyd="sudo systemctl enable --now keyd"
```

Make sure `~/.bashrc` contains:

```bash
if [ -f ~/.bash_aliases ]; then
    . ~/.bash_aliases
fi
```

## Shell

- Bash
- [Ghostty](https://ghostty.org)
    - [Fix SSH](https://ghostty.org/docs/help/terminfo#ssh)
- [Starship](https://starship.rs)
    - [Nerd Font Symbols Preset](https://starship.rs/presets/nerd-font): `starship preset nerd-font-symbols -o ~/.config/starship.toml` (after installing a [Nerd Font](https://www.nerdfonts.com/)

## To Try

- https://swaywm.org
- https://www.vicinae.com
