# Contributor and POWER Maintainer: Link <link4electronics@gmail.com>

pkgname=taradino-git
_pkgname=taradino
pkgdesc='SDL2 port of Rise of the Triad'
pkgver=20251222
pkgrel=1
arch=('powerpc' 'powerpc64' 'powerpc64le' 'espresso')
url='https://github.com/fabiangreffrath/taradino'
license=('GPL2')
depends=('sdl2' 'sdl2_mixer')
makedepends=('git' 'cmake')
provides=('taradino')
conflicts=('taradino')
install=$_pkgname.install
options=('!debug' 'strip')
source=("git+$url.git")
md5sums=('SKIP')

pkgver() {
	cd $_pkgname
	git describe --tags
}

build() {
	cmake -B build -S "$_pkgname" \
		-DCMAKE_BUILD_TYPE='Release' \
		-DCMAKE_INSTALL_PREFIX:path="/usr/"
    cmake --build build
}

package() {
	DESTDIR="$pkgdir" cmake --install build
}
