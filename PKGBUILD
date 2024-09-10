pkgname=libnexpod-host-shim
pkgver=0.0.0
pkgrel=3
pkgdesc="provides the shim for libnexpod (and others) to work inside of the container"
url="https://github.com/KilianHanich/libnexpod"
license=('Apache')
arch=('x86_64')
depends=('glibc' 'flatpak-xdg-utils')
makedepends=('zig')
provides=('podman')
conflicts=('podman')

source=("git+https://github.com/libnexpod/libnexpod#commit=9136c8c16fc62f27239bfffbc08270636f97c32f")
sha256sums=('17460829f0712c5f4040034d75cb43855e8df1283458d7a11a4315deb84a3124')

prepare() {
    cd libnexpod
    zig build --fetch libnexpod-host-shim
}

build() {
    cd libnexpod
    zig build --release libnexpod-host-shim
}

check() {
    cd libnexpod
    zig build --release shimunittests
}

package() {
    cd libnexpod
    zig build --release --sysroot "${pkgdir}" --prefix "${pkgdir}/usr" libnexpod-host-shim
    mkdir -p "${pkgdir}/usr/bin"
    ln -s "/usr/libexec/libnexpod/libnexpod-host-shim" "${pkgdir}/usr/bin/podman"
}
