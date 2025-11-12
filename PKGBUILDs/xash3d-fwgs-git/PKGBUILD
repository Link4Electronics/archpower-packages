# Maintainer: r4v3n6101

pkgname=xash3d-fwgs-git
pkgver=r5782.8259525e
pkgrel=1
pkgdesc="A custom GoldSrc engine implementation"
arch=('powerpc' 'powerpc64' 'powerpc64le' 'espresso')
url="http://xash.su/"
license=('GPL3')
depends=('freetype2' 'fontconfig' 'libpulse' 'sdl2')
makedepends=('gcc' 'gcc-libs' 'make' 'binutils' 'python')
provides=('xash3d')
conflicts=('xash3d-hlsdk' 'xash3d-git')
options=('!debug' 'strip')
source=("$pkgname::git+https://github.com/IntriguingTiles/xash3d-fwgs#branch=big-endian"
        "xash3d"
        "xash3d.desktop")
sha256sums=('SKIP'
            'df3e4dc8a5bd0bf109d70f0ab16cc70068a405818cbbbcbf9194640ed24570c1'
            '9ab4c61fd344ecadd92663b0e9f24a79a08605ff335e4a3931a0f21f7026e96d')

pkgver() {
    cd $srcdir/$pkgname
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
    cd $srcdir/$pkgname
    git submodule update --init --recursive
    # Define base arguments
    local _waf_flags=(
        -T release
        --enable-lto
        --enable-poly-opt
        --enable-bundled-deps
    )

    # Add -8 only for 64-bit PowerPC
    if [[ "$CARCH" == "powerpc64" || "$CARCH" == "powerpc64le" ]]; then
    _waf_flags+=("-8")
    fi

    # Execute waf using the array
    ./waf configure "${_waf_flags[@]}"
}

build() {
    cd $srcdir/$pkgname
    ./waf build
}

package() {
    cd $srcdir
    install -Dm 755 "xash3d" "${pkgdir}/usr/bin/xash3d"
    cd $pkgname
    ./waf install --strip --destdir="${pkgdir}/opt/xash3d/"
    install -Dm 755 "3rdparty/vgui_support/vgui-dev/lib/vgui.so" "${pkgdir}/opt/xash3d/vgui.so"
    install -Dm644 "game_launch/icon-xash-material.png" "${pkgdir}/usr/share/pixmaps/xash-material.png"
    install -Dm644 "${srcdir}/xash3d.desktop" "$pkgdir/usr/share/applications/xash3d.desktop"
}
