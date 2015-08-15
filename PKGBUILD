# Contributor: Abhishek Dasgupta <abhidg@gmail.com>
# Contributor: Eric Belanger <eric@archlinux.org>
# Contributor: Jan Fader <jan.fader@web.de>
# Contributor: SanskritFritz (gmail)

pkgname=fishfish-git
pkgver=20121214
pkgrel=1
pkgdesc="User friendly shell intended mostly for interactive use."
arch=('i686' 'x86_64')
url="http://ridiculousfish.com/shell/"
license=("GPL")
depends=('ncurses' 'bc')
optdepends=('python2: make_completions script')
makedepends=('doxygen' 'git')
provides=('fish')
conflicts=('fish')
install=fish.install
source=()

_gitroot="git://github.com/fish-shell/fish-shell.git"
_gitname="fish-shell"

build() {
	cd "$srcdir"
	msg "Connecting to the GIT repository..."

	if [ -d "$srcdir/$_gitname" ] ; then
		cd $_gitname && git pull origin
		msg "The local files are updated."
	else
		git clone $_gitroot
	fi

	msg "GIT checkout done (who invented that stupid 'server timeout' message?:)"
	msg "Starting make..."

	cd $srcdir/$_gitname
	autoconf
	./configure --prefix=/usr --sysconfdir=/etc --docdir=/usr/share/doc/fish --without-xsel
	make || return 1
	make DESTDIR="$pkgdir" install
	install -D -m644 user_doc/html/license.html "$pkgdir/usr/share/licenses/fish/license.html"

	install -m755 make_completions.py "$pkgdir/usr/bin/make_completions"
	sed -i "s/python/python2/" "$pkgdir/usr/bin/make_completions"
}
