# This is an example PKGBUILD file. Use this as a start to creating your own,
# and remove these comments. For more information, see 'man PKGBUILD'.
# NOTE: Please fill out the license field for your package! If it is unknown,
# then please put 'unknown'.

# Maintainer: James Williams <jowilliams12000 at gmail dot com>
pkgname='wallust-git'
_pkgname="wallust"
pkgver=2.9.0.r5.g0a6981a
pkgrel=4
pkgdesc="generate colors from an image"
arch=('any')
url="https://codeberg.org/explosion-mental/wallust"
license=('custom:MIT')
makedepends=('cargo' 'git' 'make')
provides=('wallust')
conflicts=('wallust')
optdepends=('imagemagick: WAL backend support')
source=("$pkgname::git+$url#branch=dev")
sha256sums=('SKIP')

pkgver() {
	cd "$_pkgname"
	git describe --long --tags | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g'
}

build() {
	cd "$_pkgname"
	export RUSTUP_TOOLCHAIN=stable
	export CARGO_BUILD_DIR=target
	make CARGOFLAGS="--frozen --release"
}

package() {
	cd "$pkgname"
	make PREFIX=/usr DESTDIR="$pkgdir" install
	install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/wallust/LICENSE"
}
