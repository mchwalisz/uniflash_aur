# Maintainer: Jimmy Stelzer <jimmy dot stelzer at gmail dot com>
# Contributor: Mikołaj Chwalisz <chwalisz at tkn.tu-berlin dot de>
pkgname=uniflash
pkgver=4.4.0.1922
pkgrel=1
pkgdesc="Universal Flash Programmer for Texas Instruments devices. Provides a single interface for programming Flash memory and executing Flash based operations on supported targets."
arch=('i686' 'x86_64')
url="http://processors.wiki.ti.com/index.php/Category:CCS_UniFlash"
license=('custom:TECHNOLOGY SOFTWARE PUBLICLY AVAILABLE by Texas Instruments Incorporated')
depends=('libudev0-shim'
		'libusb-compat')
source=(${pkgname}_sl.$pkgver.run::http://software-dl.ti.com/ccs/esd/uniflash/${pkgname}_sl.$pkgver.run
		62-msp430uif.rules)
noextract=("${pkgname}_sl.$pkgver.run" )
options=(!strip)
sha256sums=('8539b38be78e08bdeff7dccd0aa2a448a676e1ac1da0b4215817b92f0bc8b052'
            'e6fc064be173031f3a845f937b2dd7bd6742125e2bcb18f943968dde27b10cfb')
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

	cd "TICloudAgentHostApp/install_scripts/"
	install -d "$pkgdir/etc/udev/rules.d/"
	install -m 644 -D "70-mm-no-ti-emulators.rules" "$pkgdir/etc/udev/rules.d/72-mm-no-ti-emulators.rules"
	install -m 644 -D "71-ti-permissions.rules" "$pkgdir/etc/udev/rules.d/73-ti-permissions.rules"
	install -m 644 "$srcdir/62-msp430uif.rules" "$pkgdir/etc/udev/rules.d/62-msp430uif.rules"
}
