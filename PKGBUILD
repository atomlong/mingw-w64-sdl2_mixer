# maintainer: amF6enRpY2tldHNAZ21haWwuY29tCg==
pkgname=mingw-w64-sdl2_mixer
pkgver=2.8.0
pkgrel=1
pkgdesc="A simple multi-channel audio mixer (mingw-w64)"
arch=(any)
url="http://www.libsdl.org/projects/SDL_mixer"
license=("zlib")
depends=(mingw-w64-crt mingw-w64-sdl2 mingw-w64-libmodplug mingw-w64-libvorbis mingw-w64-flac mingw-w64-mpg123)
makedepends=(mingw-w64-gcc mingw-w64-configure)
options=(staticlibs !strip !buildflags)
source=("https://github.com/libsdl-org/SDL_mixer/releases/download/release-$pkgver/SDL2_mixer-$pkgver.tar.gz")
sha256sums=('1cfb34c87b26dbdbc7afd68c4f545c0116ab5f90bbfecc5aebe2a9cb4bb31549')

_architectures="i686-w64-mingw32 x86_64-w64-mingw32"

build() {
	cd "${srcdir}/SDL2_mixer-${pkgver}"

	for _arch in ${_architectures}; do
		mkdir -p build-${_arch} && pushd build-${_arch}
		${_arch}-configure
		make
		popd
	done
}

package() {
	for _arch in ${_architectures}; do
		cd "${srcdir}/SDL2_mixer-${pkgver}/build-${_arch}"
		make DESTDIR="$pkgdir" install
		${_arch}-strip --strip-unneeded "$pkgdir"/usr/${_arch}/bin/*.dll
		${_arch}-strip -g "$pkgdir"/usr/${_arch}/lib/*.a
	done
}
