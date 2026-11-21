# kitty-config

Configuration for the Kitty terminal on Linux Mint / Cinnamon, including a
fullscreen quick-access terminal and desktop keyboard shortcuts.

## Overview

This repository captures the Kitty setup used on this machine:

- **JetBrains Mono** font at 12 pt
- Colors from the GNOME Terminal **Tango** palette
- Beam cursor with blinking and translucent background
- **F12** toggles a fullscreen quick-access (Quake-style) terminal
- **Super+T** opens a new normal Kitty window

The files here are the actual config files from `~/.config/kitty`, plus a text
file of Cinnamon keybinding commands.

## Install steps

### Kitty

Kitty 0.51 or newer is required for the `quick_access_terminal` kitten. The
official binary install creates `~/.local/kitty.app` and places `kitty` and
`kitten` symlinks in `~/.local/bin`:

```sh
curl -L https://sw.kovidgoyal.net/kitty/installer.sh | sh /dev/stdin
kitty --version
```

On this machine Kitty was installed with the official installer, with symlinks
at `/home/ssn/.local/bin/kitty` and `/home/ssn/.local/bin/kitten`.

### JetBrains Mono

System-wide install:

```sh
sudo apt install fonts-jetbrains-mono
```

Or install locally without sudo by extracting the Ubuntu package into your user
font directory and refreshing the font cache:

```sh
mkdir -p /tmp/jbm && cd /tmp/jbm
apt download fonts-jetbrains-mono
tar xzf fonts-jetbrains-mono.tar.gz 2>/dev/null || true
dpkg -x fonts-jetbrains-mono/fonts-jetbrains-mono_*.deb extracted
mkdir -p ~/.local/share/fonts
cp -r extracted/usr/share/fonts/truetype/jetbrains-mono ~/.local/share/fonts/
fc-cache -f ~/.local/share/fonts
```

## Config files

| File | Installed location | Purpose |
| --- | --- | --- |
| `kitty.conf` | `~/.config/kitty/kitty.conf` | Main Kitty settings: font family/size, cursor, background opacity, and the 16 Tango palette colors. Everything else is left at Kitty defaults. |
| `quick-access-terminal.conf` | `~/.config/kitty/quick-access-terminal.conf` | Fullscreen quick-access panel: `edge center` anchors it to all screen edges and `layer overlay` keeps it above other windows. No monitor is pinned, so it follows the active screen. |
| `cinnamon-shortcuts.txt` | run with `bash` | Shell commands that register the two custom Cinnamon shortcuts. |

## Shortcuts & restore

1. Copy the config files into place:

   ```sh
   cp kitty.conf ~/.config/kitty/kitty.conf
   cp quick-access-terminal.conf ~/.config/kitty/quick-access-terminal.conf
   ```

2. Apply the keyboard shortcuts:

   ```sh
   bash cinnamon-shortcuts.txt
   ```

3. Press **F12** to show/hide the fullscreen quick-access terminal, and
   **Super+T** to open a new Kitty window.

The commands in `cinnamon-shortcuts.txt` use the absolute path
`/home/ssn/.local/bin/kitty`; change it if your Kitty binary lives elsewhere.
Cinnamon only reloads custom keybindings when the `custom-list` changes, so if
you edit a binding later, remove and re-add its entry in that list.
