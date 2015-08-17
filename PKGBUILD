# $Id: PKGBUILD 161616 2012-06-12 13:51:10Z heftig $
# Maintainer: Ionut Biru <ibiru@archlinux.org>

pkgname=udisks2-git
pkgver=20120704
pkgrel=1
pkgdesc="Disk Management Service, version 2"
arch=('i686' 'x86_64')
url="http://www.freedesktop.org/wiki/Software/udisks"
license=('GPL2')
depends=('glib2' 'udev' 'polkit' 'libatasmart' 'eject')
makedepends=('intltool' 'docbook-xsl' 'gobject-introspection' 'gnome-common' 'gtk-doc')
optdepends=('parted: partition management'
            'gptfdisk: GUID partition table support')
options=(!libtool)
#source=(http://udisks.freedesktop.org/releases/udisks-$pkgver.tar.bz2)
#sha256sums=('e58193c2f2f4fba030b6dd684708352b1eccf6826843e42899a26fef4249b0bc')

conflicts=('udisks2')
provides=('udisks2')

_gitroot='git://anongit.freedesktop.org/udisks'
_gitname='udisks'

_buildir="$srcdir/$_gitname-build"

build() {
  cd $srcdir
  if [ -d $_gitname ]; then
    cd $_gitname && git pull origin || return 1
  else
    git clone $_gitroot || return 1
  fi
  rm -rf $_buildir
  git clone $srcdir/$_gitname $_buildir

  cd $_buildir
  ./autogen.sh --prefix=/usr --sysconfdir=/etc \
      --with-systemdsystemunitdir=/usr/lib/systemd/system \
      --localstatedir=/var --disable-static
  make
}

package() {
  cd $_buildir
  make DESTDIR="$pkgdir" install \
    bash_completiondir=/usr/share/bash-completion/completions
}
