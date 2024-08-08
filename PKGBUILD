pkgname=nexpod-host-shim
pkgver=0.0.0
pkgrel=1
pkgdesc="provides the shim for libnexpod (and others) to work inside of the container"
url="https://github.com/KilianHanich/libnexpod"
license=('Apache')
arch=('x86_64')
depends=('glibc' 'flatpak-xdg-utils')
makedepends=('zig')
provides=('podman')
conflicts=('podman')

source=("git+https://github.com/KilianHanich/libnexpod#commit=e746d06b12ffcd5d8e10d151930b8bb68a6dfe7a")
sha256sums=('6f59d354cfecdec5dd37836f0397c7a5ace84bcfe1e7ed6339671718fd1db3d2')

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
    zig build --release test
}

package() {
    cd libnexpod
    zig build --release --sysroot "${pkgdir}" --prefix "${pkgdir}/usr" nexpod-host-shim
    mkdir -p "${pkgdir}/usr/bin"
    ln -s "/usr/libexec/nexpod/nexpod-host-shim" "${pkgdir}/usr/bin/podman"
}
