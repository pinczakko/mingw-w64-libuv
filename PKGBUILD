# $Id$
# Maintainer: Massimiliano Torromeo <massimiliano.torromeo@gmail.com>
# Modified by Darmawan Salihun <darmawan.salihun@gmail.com> for mingw-w64 

pkgname=mingw-w64-libuv
_pkgname=libuv
pkgver=1.9.1
pkgrel=1
pkgdesc="Multi-platform support library with a focus on asynchronous I/O"
arch=('any')
url="https://github.com/libuv/libuv"
license=('custom')
#depends=('glibc')
makedepends=('python-sphinx' 'mingw-w64-gcc')
source=("https://github.com/libuv/libuv/archive/v$pkgver/$pkgname-$pkgver.tar.gz")
sha256sums=('a6ca9f0648973d1463f46b495ce546ddcbe7cce2f04b32e802a15539e46c57ad')

_architectures="x86_64-w64-mingw32 i686-w64-mingw32"

build() {
  cd "$srcdir/${_pkgname}-$pkgver"
  for _arch in ${_architectures}; do
    mkdir -p build-${_arch} && pushd build-${_arch}
	../autogen.sh
	${_arch}-configure --enable-shared 
    make V=1
	popd
  done
}

package() {

  for _arch in ${_architectures}; do
    cd "${srcdir}/${_pkgname}-${pkgver}/build-${_arch}"
    make install DESTDIR="${pkgdir}"
    rm -rf "${pkgdir}/usr/${_arch}/share/man"
    ${_arch}-strip -x -g "${pkgdir}/usr/${_arch}/bin/"*.dll
#    ${_arch}-strip -g "${pkgdir}/usr/${_arch}/lib/"*.a
  done
}

