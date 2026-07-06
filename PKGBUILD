# Maintainer: Cap
pkgname=hyprland-patched
pkgver=0.55.4
pkgrel=1
pkgdesc="Hyprland with idle cursor animation patch"
arch=(x86_64)
url="https://github.com/hyprwm/Hyprland"
license=(BSD)
depends=(
    cairo
    gcc-libs
    glibc
    glslang
    hyprcursor
    hyprgraphics
    hyprland-protocols
    hyprlang
    hyprutils
    hyprwayland-scanner
    libdisplay-info
    libdrm
    libglvnd
    libinput
    libliftoff
    libx11
    libxcb
    libxcomposite
    libxfixes
    libxkbcommon
    libxrender
    opengl-driver
    pango
    pixman
    re2
    seatd
    systemd-libs
    wayland
    wayland-protocols
    xcb-proto
    xcb-util
    xcb-util-errors
    xcb-util-keysyms
    xcb-util-renderutil
    xcb-util-wm
    xorg-xinput
    xorg-xwayland
)
makedepends=(
    aquamarine
    cmake
    gdb
    git
    hyprwayland-scanner
    jq
    ninja
    pkgconf
    python
    vulkan-headers
    xorgproto
)
provides=(hyprland)
conflicts=(hyprland)
source=(
    "hyprland::git+https://github.com/hyprwm/Hyprland.git#tag=v${pkgver}"
    "hyprland-idle-cursor.patch"
)
sha256sums=('381b84fd51e3b9447db405184b563aecbd3925b97e4c0880675ecfd136408abf'
            'cea744ee346cff5794cef9e8c1a4b6da2b879c4e96b84e247b9f1f7a1d3c5c88')

prepare() {
    cd hyprland
    git submodule update --init --recursive
    patch -p1 < "${srcdir}/hyprland-idle-cursor.patch"
}

build() {
    cd hyprland
    cmake -B build \
        -DCMAKE_BUILD_TYPE=Release \
        -DCMAKE_INSTALL_PREFIX=/usr
    cmake --build build -j$(nproc)
}

package() {
    cd hyprland
    DESTDIR="${pkgdir}" cmake --install build
}
