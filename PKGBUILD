# Maintainer: Tom Kuther <gimpel@sonnenkinder.org>

pkgname=moneyguru-bin
pkgver=2.6.2
pkgrel=1
pkgdesc="moneyGuru is a personal finance management application"
arch=(i686 x86_64)
url=http://www.hardcoded.net/moneyguru/
license=(custom:Fairware)
depends=(python pyqt sip)
makedepends=(lynx)
_filearch=i386
[ "${CARCH}" == "x86_64" ] && _filearch=amd64

build()
{
	rm -f moneyguru*.deb
	_url=https://launchpad.net/~hsoft/+archive/ppa/+files/moneyguru_${pkgver}~quantal_${_filearch}.deb
	wget ${_url}
	bsdtar -xf $(basename ${_url}) data.tar.gz
	bsdtar -xf data.tar.gz
	rm data.tar.gz
	cd usr/share/moneyguru/
	rm -f sip.so
	rm -rf PyQt4
	mkdir -p "${pkgdir}"/usr/bin
	cd "${srcdir}"/usr
	mv share "${pkgdir}"/usr/
	sed -i 's|#!/usr/bin/env python3|#!/usr/bin/python|' "${pkgdir}"/usr/share/moneyguru/run.py
	USRBINFILE="${pkgdir}"/usr/bin/moneyguru
	echo "#!/bin/bash" > "$USRBINFILE"
	echo "cd /usr/share/moneyguru" >> "$USRBINFILE"
	echo "python run.py" >> "$USRBINFILE"
	chmod +x "$USRBINFILE"
}
