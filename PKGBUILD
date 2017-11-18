# Maintainer: SJ_UnderWater
# Based on netatalk package :
# Maintainer: Dominik Dingel <mail at wodar dot de>
# Contributor: William Udovich <nerdzrule7 at earthlink dot net>
# Contributor: Farhan Yousaf <farhany at xaviya dot com>

pkgname=netatalk
pkgver=3.1.11
pkgrel=1
pkgdesc='A kernel-level implementation of AFP services'
arch=('x86_64')
url='http://netatalk.sourceforge.net'
license=('GPL')
depends=('avahi>=0.6' 'libldap' 'libgcrypt>=1.2.3' 'libevent' 'python' 'dbus-glib')
replaces=('netatalk-git' 'netatalk2')
backup=('etc/afp.conf'
	'etc/extmap.conf')
options=('!libtool')
install=$pkgname.install
changelog=$pkgname.changelog
source=("http://downloads.sourceforge.net/project/$pkgname/$pkgname/$pkgver/$pkgname-$pkgver.tar.bz2")
sha256sums=('3434472ba96d3bbe3b024274438daad83b784ced720f7662a4c1d0a1078799a6')

build() {
	cd $pkgname-$pkgver
	msg2 'Configuring...'
	CFLAGS="-Wno-unused-result -O2" ./configure --prefix=/usr --localstatedir=/var/state --sysconfdir=/etc --sbindir=/usr/bin --with-init-style=systemd \
		--with-cracklib --with-cnid-cdb-backend --enable-pgp-uam --with-libevent=no
	sed -i -e s/-Ino// -e s/-Lno// etc/netatalk/Makefile
	msg2 'Making...'
	make
}

package() {
	cd $pkgname-$pkgver
	msg2 'Building...'
	make DESTDIR="$pkgdir" install
}

