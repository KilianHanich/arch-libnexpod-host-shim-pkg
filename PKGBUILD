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

source=("git+https://github.com/libnexpod/libnexpod#commit=1a309dc23949965e97aa8e882a706886e2715677")
sha256sums=('83cd14336de0e8789b54da5f997e6eabc54ba12593002cdd9f803ed14c1dbac9')

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
