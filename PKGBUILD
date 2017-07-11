pkgname=hotspot-git
pkgver=r286.773d8a0
pkgrel=1
pkgdesc="The Linux perf GUI for performance analysis"
arch=('x86_64')
url="https://github.com/KDAB/hotspot"
license=('GPL')
depends=('qt5-base' 'elfutils' 'threadweaver' 'ki18n' 'kconfig' 'kitemviews' 'kcoreaddons' 'kitemmodels' 'kconfigwidgets')
makedepends=('git' 'cmake' 'extra-cmake-modules')
source=('hotspot::git+https://github.com/KDAB/hotspot.git')
md5sums=('SKIP')

pkgver() {
	cd "$srcdir/${pkgname%-git}"
	printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
	cd "$srcdir"
	mkdir -p build-hotspot
	cd "${pkgname%-git}"
	git submodule update --init --recursive
}

build() {
	cd "$srcdir/build-hotspot"
	cmake "-DCMAKE_INSTALL_PREFIX=$pkgdir/usr" "$srcdir/${pkgname%-git}"
	make
}

package() {
	cd "$srcdir/build-hotspot"
	make install
	mv "$pkgdir/usr/lib64" "$pkgdir/usr/lib"
	rm -rf "$pkgdir/usr/share/icons"
}
