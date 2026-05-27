# hyprland-patched

Hyprland with an idle cursor animation patch. Instead of hiding the cursor after inactive_timeout seconds, it shows the animated progress (AppStarting) cursor. Restores to default on movement.

## Install patched Hyprland

    git clone https://github.com/xCaptaiN09/hyprland-patched
    cd hyprland-patched
    makepkg -si

## hyprland.conf settings

    cursor:inactive_timeout = 10
    env = XCURSOR_THEME,VS-Cursors
    env = XCURSOR_SIZE,24
    env = HYPRCURSOR_THEME,VS-Cursors
    env = HYPRCURSOR_SIZE,24

## VS-Cursors setup

Install win2xcur:

    pipx install win2xcur
    sudo pacman -S imagemagick

Convert Windows cursors:

    mkdir -p ~/converted-cursors
    cd 'Cursors & Previews/Cursors'
    win2xcur *.cur *.ani -o ~/converted-cursors

Setup theme:

    mkdir -p ~/.local/share/icons/VS-Cursors/cursors
    cp ~/converted-cursors/* ~/.local/share/icons/VS-Cursors/cursors/

Create index.theme:

    [Icon Theme]
    Name=VS-Cursors

Symlinks (run from cursors directory):

    ln -s Arrow default
    ln -s Arrow top_left_arrow
    ln -s IBeam text
    ln -s IBeam xterm
    ln -s Hand pointer
    ln -s Hand pointing_hand
    ln -s SizeAll move
    ln -s SizeAll fleur
    ln -s SizeNS ns-resize
    ln -s SizeNS size_ver
    ln -s SizeNWSE nwse-resize
    ln -s SizeNWSE size_fdiag
    ln -s SizeNESW nesw-resize
    ln -s SizeNESW size_bdiag
    ln -s No not-allowed
    ln -s No forbidden
    ln -s Help help
    ln -s Wait watch
    ln -s Wait progress (then redo: rm progress && ln -s AppStarting progress)
    ln -s Crosshair crosshair
    ln -s UpArrow up_arrow

Or restore from backup:

    tar -xzf VS-Cursors-backup.tar.gz -C ~/.local/share/icons/
    sudo cp -r ~/.local/share/icons/VS-Cursors /usr/share/icons/

## Caelestia shell cursor fix

Edit ~/.local/share/caelestia/hypr/variables.conf:

    $cursorTheme = VS-Cursors

## GTK cursor fix

~/.config/gtk-3.0/settings.ini and ~/.config/gtk-4.0/settings.ini:

    [Settings]
    gtk-cursor-theme-name=VS-Cursors
    gtk-cursor-theme-size=24

## gsettings

    gsettings set org.gnome.desktop.interface cursor-theme 'VS-Cursors'
    gsettings set org.gnome.desktop.interface cursor-size 24

## Updating Hyprland

1. Bump pkgver in PKGBUILD to new version
2. Run makepkg -si
3. If patch fails, adjust hyprland-idle-cursor.patch to match new source

## Files

- PKGBUILD - build recipe
- hyprland-idle-cursor.patch - source patch for Renderer.cpp and Renderer.hpp
- VS-Cursors-backup.tar.gz - converted Xcursor theme
