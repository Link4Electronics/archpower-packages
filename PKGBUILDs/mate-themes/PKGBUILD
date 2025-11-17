# Maintainer:  Alexander Epaneshnikov <alex19ep@archlinux.org>
# Contributor: Brad Fanella <cesura@archlinux.org>
# Contributor: Martin Wimpress <code@flexion.org>

pkgname=mate-themes
pkgver=3.22.26
pkgrel=3
pkgdesc="Official themes for the MATE desktop"
url="http://mate-desktop.org"
arch=('any')
license=('LGPL-2.1-or-later')
makedepends=('autoconf-archive' 'mate-common' 'intltool')
optdepends=('mate-icon-theme: default icon theme')
options=('!emptydirs')
groups=('mate')
source=("${pkgname}-${pkgver}.tar.gz::https://github.com/mate-desktop/mate-themes/archive/refs/tags/v${pkgver}.tar.gz")
sha256sums=('7aa022a120b02ee14bcbb35c4e33f4f675c0eb6f33bb0ec7b9595b00bd9b14b7')

prepare() {
    	cd "${pkgname}-${pkgver}"

	# Remove check for gtk2
	sed -i '/Check GTK+ theme engines/,+3d' configure.ac

	./autogen.sh
}

build() {
    	cd "${pkgname}-${pkgver}"
    	./configure \
        	--prefix=/usr
    	make
}

package() {
    	cd "${pkgname}-${pkgver}"
    	make DESTDIR="${pkgdir}" install
}
