# Maintainer:  Vitalii Kuzhdin <vitaliikuzhdin@gmail.com>

_basename="xf86-input-vmmouse"
pkgname="${_basename//xf86/xlibre}"
pkgver=13.2.0.1
pkgrel=1
pkgdesc="XLibre VMWare Mouse input driver"
arch=('aarch64' 'x86_64')
url="https://github.com/X11Libre/${_basename}"
license=('custom')
depends=('glibc' 'systemd-libs')
makedepends=('xlibre-server-devel' 'xorgproto' 'X-ABI-XINPUT_VERSION=26.0')
provides=("${_basename}")
conflicts=("${_basename}" 'xorg-server<21.1.1' 'X-ABI-XINPUT_VERSION<26' 'X-ABI-XINPUT_VERSION>=27')
groups=('xlibre-drivers')
_pkgsrc="${_basename}-xlibre-${_basename}-${pkgver}"
source=("${_pkgsrc}.tar.gz::${url}/archive/refs/tags/xlibre-${_basename}-${pkgver}.tar.gz")
b2sums=('0d61296043ecbcdd2bd55e8ed29923290d39eb1addba507dbe55ee3b3f4e982dc1360f9685782289727080653074f789fc20d11f46f80410b1152bfcc7a0c1c8')

build() {
  local configure_options=(
    --prefix='/usr'
    --with-udev-rules-dir='/usr/lib/udev/rules.d'
  )

  cd "${srcdir}/${_pkgsrc}"
  autoreconf -vfi
  ./configure "${configure_options[@]}"
  make
}

package() {
  cd "${srcdir}/${_pkgsrc}"
  make DESTDIR="${pkgdir}" install

  install -vDm644 "README"  "${pkgdir}/usr/share/doc/${pkgname}/README"
  install -vDm644 "COPYING" "${pkgdir}/usr/share/licenses/${pkgname}/COPYING"
}
