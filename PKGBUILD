# Maintainer: Jingbei Li <i@jingbei.li>

pkgname=raspi-config
_gitname=raspi-config-manjaro
pkgver=20211130.r388.d535e2e
pkgrel=1
pkgdesc="A simple configuration tool for common Raspberry Pi administrative tasks (ArchlinuxARM fork)"
arch=('any')
url="https://github.com/sileshn/raspi-config-manjaro"
license=('MIT')
depends=(
	alsa-utils
	dtc
	libnewt # Debian: whiptail
	lua
	#systemd # Debian: initramfs-tools
	parted
	psmisc
	vim
)
makedepends=('git')
optdepends=(
	iw
	triggerhappy
	raspi-firmware
	xorg-xrandr
)
provides=('raspi-config')
conflicts=('raspi-config')
source=("git+${url}")
md5sums=('SKIP')

pkgver() {
	cd "${srcdir}/${_gitname}"
	(
		set -o pipefail
		git describe --long 2>/dev/null | sed 's/\([^-]*-g\)/r\1/;s/-/./g' ||
		printf "%s.r%s.%s" \
		"$(git log -1 --date=format:%Y%m%d --format=%ad)" \
		"$(git rev-list --count HEAD)" \
		"$(git log | head -n 1 | cut -d" " -f2 | awk '{print substr($0,0,7)}')"
	)
}

package() {
	cd "${srcdir}/${_gitname}"
	install -dm750 ${pkgdir}/etc/sudoers.d/
	cp -r usr etc ${pkgdir}
	install -Dm755 raspi-config ${pkgdir}/usr/bin/raspi-config
	#install -Dm644 autologin@.service ${pkgdir}/etc/systemd/system/autologin@.service
}
