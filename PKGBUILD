# Maintainer: Jimmy Stelzer <jimmy dot stelzer at gmail dot com>
# Contributor: Mikołaj Chwalisz <chwalisz at tkn.tu-berlin dot de>
pkgname=uniflash
pkgver=4.3.0.1802
pkgrel=1
pkgdesc="Universal Flash Programmer for Texas Instruments devices. Provides a single interface for programming Flash memory and executing Flash based operations on supported targets."
arch=('i686' 'x86_64')
url="http://processors.wiki.ti.com/index.php/Category:CCS_UniFlash"
license=('custom:TECHNOLOGY SOFTWARE PUBLICLY AVAILABLE by Texas Instruments Incorporated')
depends=('libudev0-shim'
	     'libusb-compat'
	     'ticloudagent')
source=(${pkgname}_sl.$pkgver.run::http://software-dl.ti.com/ccs/esd/uniflash/${pkgname}_sl.$pkgver.run )
noextract=("${pkgname}_sl.$pkgver.run" )
options=(!strip)
md5sums=('04a751173260d3c95316604602900036')
sha256sums=('feb00f4db5df8df5abbfbceb90ebc2e9f4f4c9071544bf0470fd909988c3c553')
DLAGENTS=('http::/usr/bin/curl -fLC - --cookie nada -o %o %u')
prepare() {
	cd "$srcdir"
	msg "If you continue you will accept the license, more information at http://processors.wiki.ti.com/index.php/Category:CCS_UniFlash."
	chmod +x ${pkgname}_sl.$pkgver.run
}
build() {
	cd "$srcdir"

}

package() {
	cd "$srcdir"
	./${pkgname}_sl.$pkgver.run --unattendedmodeui none --mode unattended --prefix $pkgdir/opt/ti/uniflash
	cd "$pkgdir/opt/ti/uniflash"

	sed -s "s|$pkgdir||" -i UniFlash.desktop
	install -d "$pkgdir/usr/share/applications"
	install -m 644 "$pkgdir/opt/ti/uniflash/UniFlash.desktop" "$pkgdir/usr/share/applications/UniFlash.desktop"
}
