pkgname=nexpod-host-shim
pkgver=0.0.0
pkgrel=2
pkgdesc="provides the shim for libnexpod (and others) to work inside of the container"
url="https://github.com/KilianHanich/libnexpod"
license=('Apache')
arch=('x86_64')
depends=('glibc' 'flatpak-xdg-utils')
makedepends=('zig')
provides=('podman')
conflicts=('podman')

source=("git+https://github.com/KilianHanich/libnexpod#commit=272ec000347e4e9d19cd11a12a8e632f51fafe40")
sha256sums=('71a81c29f0ef73fc70589dfede71c0d3c20e2923cf419d217a6f5dc164f3b567')

prepare() {
    cd libnexpod
    zig build --fetch nexpod-host-shim
}

build() {
    cd libnexpod
    zig build --release nexpod-host-shim
}

check() {
    cd libnexpod
    zig build --release shimunittests
}

package() {
    cd libnexpod
    zig build --release --sysroot "${pkgdir}" --prefix "${pkgdir}/usr" nexpod-host-shim
    mkdir -p "${pkgdir}/usr/bin"
    ln -s "/usr/libexec/nexpod/nexpod-host-shim" "${pkgdir}/usr/bin/podman"
}
