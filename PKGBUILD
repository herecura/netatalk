# Maintainer: SJ_UnderWater
# Based on netatalk package :
# Maintainer: Dominik Dingel <mail at wodar dot de>
# Contributor: William Udovich <nerdzrule7 at earthlink dot net>
# Contributor: Farhan Yousaf <farhany at xaviya dot com>

pkgname=netatalk
pkgver=3.0.1
pkgrel=3
pkgdesc='A kernel-level implementation of AFP services'
arch=('i686' 'x86_64')
url='http://netatalk.sourceforge.net'
license=('GPL')
depends=('avahi>=0.6' 'libldap' 'libgcrypt>=1.2.3' 'libevent')
replaces=('netatalk-git' 'netatalk2')
backup=('etc/afp.conf')
options=('!libtool')
install=$pkgname.install
changelog=$pkgname.changelog
source=(http://iweb.dl.sourceforge.net/project/$pkgname/$pkgname/$pkgver/$pkgname-$pkgver.tar.bz2)
md5sums=('b4f5c932b2ca99f5292bd6b6d69b3ebc')

build() {
	cd $pkgname-$pkgver
	msg2 'Fixing...'
	sed -i 's/x"linux/x"generic/' macros/netatalk.m4
	sed -i 's:/lib:/usr/lib:' distrib/initscripts/Makefile.{am,in}
	autoreconf &>/dev/null
	msg2 'Configuring...'
	CFLAGS="-Wno-unused-result" ./configure --prefix=/usr --localstatedir=/var/state --sysconfdir=/etc --with-init-style=systemd \
		--with-cracklib --with-cnid-cdb-backend --enable-pgp-uam --without-libevent-header --without-libevent-lib
	sed -i -e s/-Ino// -e s/-Lno// etc/netatalk/Makefile
	msg2 'Making...'
	make >/dev/null
}
package() {
	cd $pkgname-$pkgver
	msg2 'Building...'
	make DESTDIR="$pkgdir" install >/dev/null
}
