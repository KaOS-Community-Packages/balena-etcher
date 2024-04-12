
pkgname=balena-etcher
_pkgname=balenaEtcher
__pkgname=etcher
pkgver=1.18.11
pkgrel=1
pkgdesc='Flash OS images to SD cards & USB drives, safely and easily'
arch=('x86_64')
url='https://balena.io/etcher'
license=('Apache')
depends=('gtk3' 'libxtst' 'libxss' 'nss' 'alsa-lib' 'glib2' 'polkit' 'libusb' 'kde-gtk-config')
makedepends=("tar")
optdepends=("libnotify: For system tray notifications")
options=('!strip')
install="${pkgname}.install"
source=("${pkgname}-${pkgver}.rpm::https://github.com/balena-io/etcher/releases/download/v${pkgver}/${pkgname}-${pkgver}.x86_64.rpm")
sha256sums=('SKIP')

package() {
  msg2 "Unpacking SOURCE files of the downloaded RMP binary package "
  mkdir -p "${pkgdir}/opt/"
  bsdtar -xf "${srcdir}/${pkgname}-${pkgver}.rpm" -C "${pkgdir}/"

  install -d "${pkgdir}/usr/share/pixmaps/"
  cp "${pkgdir}/usr/share/icons/hicolor/512x512/apps/${pkgname}.png" -t "${pkgdir}/usr/share/pixmaps/"

  msg2 "Removing unnecessary post-build ID files from the RPM package"
  rm -fdr "${pkgdir}/usr/lib/"

  sed -i -e "/Exec=/i\Path=/opt/balenaEtcher/" \
         -e "s|Exec=/opt/balenaEtcher/balena-etcher %U|Exec=/usr/bin/balena-etcher %U|g" \
         "${pkgdir}/usr/share/applications/${pkgname}.desktop"

  msg2 "Linking binaries from SOURCE to the system"
  install -d "${pkgdir}/usr/bin/"
  ln -v -f -s "/opt/${_pkgname}/${pkgname}" "${pkgdir}/usr/bin/${pkgname}"

  msg2 "Linking LICENSES from SOURCE to the system"
  install -d "${pkgdir}/usr/share/licenses/${pkgname}"
  ln -v -f -s "/opt/${_pkgname}/LICENSE.electron.txt" -t "${pkgdir}/usr/share/licenses/${pkgname}"
  ln -v -f -s "/opt/${_pkgname}/LICENSES.chromium.html" -t "${pkgdir}/usr/share/licenses/${pkgname}"
}
