pkgname=dmenu-toki83w
_pkgname=dmenu
pkgver=5.3
pkgrel=1
pkgdesc='Generic menu for X'
url='https://github.com/toki83w/dmenu'
arch=('x86_64')
license=('MIT')
makedepends=('git')
depends=('sh' 'glibc' 'coreutils' 'libx11' 'libxinerama' 'libxft' 'freetype2' 'fontconfig' 'libfontconfig.so')
source=("git+https://github.com/toki83w/dmenu")
sha512sums=('SKIP')

provides=("$_pkgname")
conflicts=("$pkgname" "$_pkgname")

pkgver() {
    cd ${_pkgname}
    printf "%s.r%s.%s" "$(awk '/^VERSION =/ {print $3}' config.mk)" \
        "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
    cd ${_pkgname}
    echo "CPPFLAGS+=${CPPFLAGS}" >> config.mk
    echo "CFLAGS+=${CFLAGS}" >> config.mk
    echo "LDFLAGS+=${LDFLAGS}" >> config.mk
    cp config.def.h config.h
}
 
build() {
    cd ${_pkgname}
    make \
        X11INC=/usr/include/X11 \
        X11LIB=/usr/lib/X11 \
        FREETYPEINC=/usr/include/freetype2
}

package() {
    cd ${_pkgname}
    make PREFIX=/usr DESTDIR="${pkgdir}" install
    install -Dm 644 LICENSE -t "${pkgdir}/usr/share/licenses/${pkgname}"
}

