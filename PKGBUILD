# Maintainer: Andrea Crotti <mail andrea dot crotti dot 0 at gmail dot com>
# Contributor: William Udovich <nerdzrule7 at earthlink dot net>
# Contributor: Farhan Yousaf <farhany at xaviya dot com>

pkgname=netatalk
pkgver=2.2.2
pkgrel=1
pkgdesc="A kernel level implementation of the AppleTalk Protocol Suite"
arch=('i686' 'x86_64')
url="http://netatalk.sourceforge.net"
options=('!libtool')
license=("GPL")
backup=('etc/netatalk/afpd.conf'
        'etc/netatalk/netatalk.conf'
        'etc/netatalk/atalkd.conf'
        'etc/netatalk/papd.conf'
        'etc/netatalk/AppleVolumes.default'
        'etc/netatalk/AppleVolumes.system')

depends=('libcups' 'pam' 'coreutils>=7.1-2' 'db')
optdepends=('avahi' 'tcp_wrappers' 'openssl' 'libgcrypt')
makedepends=('make' 'patch' 'gcc')
source=(
	"http://downloads.sourceforge.net/project/netatalk/netatalk/$pkgver/netatalk-$pkgver.tar.bz2"
	"afpd"
	"atalkd"
	"papd"
	"cnid"
	"afpd.service"
)
install=netatalk.install

md5sums=('bd42b686ec7209d9ab47bd8e2e2431c4'
         '16ab9fa50ec4abde6de478fc7de57805'
         '2d05de4a16faf7d4af21b5f14e33fa82'
         'b16a687c96dd1ca7ffefd7c995356c0d'
         'e21ef8051269583764e68d00683691bb'
         '9b6b2fee54fe052bba0c69f00d335bdb')

build() {
    cd $startdir/src/netatalk-$pkgver
    ./configure --prefix=/usr --with-ssl-dir=/usr --localstatedir=/var --enable-fhs --enable-zeroconf=/usr --disable-srvloc --with-cnid-cdb-backend --enable-ddp
    make || return 1
    make DESTDIR=$startdir/pkg install

    mv $startdir/pkg/usr/include/netatalk{,2}

    install -d $startdir/pkg/etc/rc.d
    install -m755 ../{afpd,atalkd,papd,cnid} $startdir/pkg/etc/rc.d

    install -d $startdir/pkg/etc/avahi/services
    install -m744 ../afpd.service $startdir/pkg/etc/avahi/services

    rm -f $startdir/pkg/usr/share/man/man1/timeout.1{,.gz}
}
