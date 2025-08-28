pkgname=kbd
pkgver=2.8.0
pkgrel=1
pkgdesc="Keytable files and keyboard utilities"
arch=('x86_64')
url="https://kbd-project.org/"
license=('GPL-2.0-or-later')
depends=('glibc')
options=('!lto')
source=(https://www.kernel.org/pub/linux/utils/${pkgname}/${pkgname}-${pkgver}.tar.xz
    https://www.linuxfromscratch.org/patches/downloads/${pkgname}/${pkgname}-${pkgver}-backspace-1.patch)
sha256sums=(01f5806da7d1d34f594b7b2a6ae1ab23215344cf1064e8edcd3a90fef9776a11
    8be28dcb11420624a500f2ea4fe975f771174bffee50e54ec8cd295a2dec104e)

prepare() {
    cd ${pkgname}-${pkgver}

    patch -Np1 -i ${srcdir}/${pkgname}-${pkgver}-backspace-1.patch

    sed -i '/RESIZECONS_PROGS=/s/yes/no/' configure
    sed -i 's/resizecons.8 //' docs/man/man8/Makefile.in
}

build() {
    cd ${pkgname}-${pkgver}

    local configure_args=(
        --sysconfdir=/etc
        --disable-vlock
        ${configure_options}
    )

    ./configure "${configure_args[@]}"

    make
}

package() {
    cd ${pkgname}-${pkgver}

    make DESTDIR=${pkgdir} install

    install -vdm755 ${pkgdir}/usr/share/doc/${pkgname}-${pkgver}
    cp -R -v docs/doc -T ${pkgdir}/usr/share/doc/${pkgname}-${pkgver}
}
