# Maintainer: Nikos Toutountzoglou <nikos.toutou@protonmail.com>
# Original install script: https://aur.archlinux.org/packages/snowmix

pkgname=snowmix
_appname=Snowmix
pkgver=0.5.1.1
pkgrel=1
pkgdesc="Dynamic audio and video feed mixer"
arch=(i686 x86_64 armv7h)
url="https://snowmix.sourceforge.net"
license=(GPL)
depends=(
	openbsd-netcat
	bc
	gstreamer
	gst-plugins-good
	gst-plugins-bad
	gst-plugins-ugly
	gst-libav
	bwidget
)
makedepends=(
	pkg-config
	autoconf
	automake
	make
	bc
	libtool
	awk
	gcc
	tcl
	tk
)
source=("https://downloads.sourceforge.net/sourceforge/snowmix/$_appname-$pkgver.tar.gz"
	"snowmix.sh")
sha256sums=('e72d3fdab4b4c03b52787b8641fd6399b3a0a0c8976bf019a959b99f0f0a459d'
            '5ea9ef7dce105873fcd8bd838d7fe46fa82d8a5b9a5404cc779f6c5ac9ca1483')

build() {
	cd $_appname-$pkgver
	mkdir -p m4
	aclocal
	autoconf
	libtoolize --force
	automake --add-missing

	# --enable-snowmixgui: 		Turn on GUI for Snowmix. Under development (req. bwidget)
	# --enable-snowmixosmesa: 	Turn on Off Screen Mesa (OpenGL)
	# --enable-snowmixx11: 		Turn on X11 (OpenGL for X-Windows)
	# --enable-snowmixglu: 		Turn on OpenGL Utility Library
	# --enable-snowmixglut: 	Turn on OpenGL Utility Toolkit Library
	./configure --prefix=/usr \
		--enable-snowmixosmesa \
		--enable-snowmixx11 \
		--enable-snowmixglu \
		--enable-snowmixglut \
		--enable-snowmixgui
	make
}

package() {
	cd $_appname-$pkgver
	make DESTDIR="$pkgdir" install
	# Install snowmix path (lougout required)
	install -Dvm755 "$srcdir"/snowmix.sh "$pkgdir"/etc/profile.d/snowmix.sh
	# Install license files
	install -Dvm644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
	# Outro message
	msg2 "Please logout/login user '$USER' to update snowmix path."
}
