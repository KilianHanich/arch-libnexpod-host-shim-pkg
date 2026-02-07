pkgname=libnexpod-host-shim
pkgver=0.0.0
pkgrel=3
pkgdesc="provides the shim for libnexpod (and others) to work inside of the container"
url="https://github.com/KilianHanich/libnexpod"
license=('Apache')
arch=('x86_64')
depends=('glibc' 'flatpak-xdg-utils')
#makedepends=('zig')
provides=('podman')
conflicts=('podman')

source=("git+https://github.com/KilianHanich/libnexpod#commit=39b8758ac839d34572cf98b9b4c33eeda33da200")
sha256sums=('73269b578bfdaa6bc331f9ef4201ef2980970b7aae0a10a62c3d755d032fdff2')

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
