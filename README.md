# hyprland-patched

Hyprland with an idle cursor animation patch. When the cursor is idle for `inactive_timeout` seconds, it switches to the animated progress cursor instead of hiding. Restores to default on movement.

## What it does

Hyprland normally hides the cursor after `cursor:inactive_timeout` seconds. This patch intercepts that and shows the AppStarting animation instead, then restores default when you move.

## Install

    git clone https://github.com/xCaptaiN09/hyprland-patched
    cd hyprland-patched
    makepkg -si

## hyprland.conf

    cursor:inactive_timeout = 10
    env = XCURSOR_THEME,VS-Cursors
    env = XCURSOR_SIZE,24
    env = HYPRCURSOR_THEME,VS-Cursors
    env = HYPRCURSOR_SIZE,24

## Restore cursor theme

    tar -xzf VS-Cursors-backup.tar.gz -C ~/.local/share/icons/
    hyprctl setcursor VS-Cursors 24

## Updating Hyprland

1. Bump pkgver in PKGBUILD to new version
2. Run makepkg -si
3. If patch fails, adjust hyprland-idle-cursor.patch to match new source

## Files

- PKGBUILD - build recipe
- hyprland-idle-cursor.patch - source patch for Renderer.cpp and Renderer.hpp
- VS-Cursors-backup.tar.gz - converted Xcursor theme
