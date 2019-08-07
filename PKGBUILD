# Maintainer:Ramon Buldó <rbuldo@gmail.com>
# Maintainer: Philip Müller <philm@manjaro.org>
# Maintainer: Bernhard Landauer <oberon@manjaro.org>

pkgbase=cleanjaro-xfce-gtk3-settings
pkgname=('cleanjaro-xfce-gtk3-settings')
pkgver=20190807
pkgrel=1
pkgdesc="Cleanjaro Linux Xfce settings"
arch=('any')
url="https://github.com/Yorper/cleanjaro-xfce-settings"
license=('GPL')
depends=('manjaro-base-skel'
         'papirus-maia-icon-theme'
         'qt5-styleplugins'
         'qt5ct'
         'xcursor-breeze'
         'matcha-gtk-theme'
         'kvantum-theme-arc'
         'kvantum-theme-matcha')
makedepends=('git')
source=("$pkgbase::git+$url.git" 'cleanjaro-xfce-settings.hook' 'mxs-bgd-sym'
        'xfce-pbw.sh' 'xfce-panel-workaround.desktop')
sha256sums=('SKIP'
            '712be2c2c621bdf1420a78188af49420bf31d28638283f29107c5274bed3ddfe'
            '03770c4735b588bdee49f7e1e5d73d8500524d875603c473bdf0f4ffb862c152'
            'c2a09b24e47df963fae456df3286e0f1525eb16b48da5a020579e788037631da'
            '3afbe1b3e8b8339ace5f8496f8fcd605d5768c10145da15a71a9d487be45a8c9')

pkgver() {
	date +%Y%m%d
}

_inst_dir(){
	install -d $pkgdir/etc
	cp -rL $srcdir/$pkgbase$1/skel $pkgdir/etc

	install -d $pkgdir/usr/share/glib-2.0/schemas
	cp $srcdir/$pkgbase/schemas/* $pkgdir/usr/share/glib-2.0/schemas
}

package_cleanjaro-xfce-gtk3-settings() {
	pkgdesc='Cleanjaro Linux XFCE-GTK3 Settings'
	conflicts=('manjaro-desktop-settings' 'manjaro-xfce-settings')
	provides=('cleanjaro-desktop-settings' 'cleanjaro-xfce-settings')
	replaces=('manjaro-xfce-gtk3-settings')

	_inst_dir

	local _subst="
		s|%BIN%|mxs-bgd-sym|g
	"
	sed "${_subst}" "${srcdir}/cleanjaro-xfce-settings.hook" |
		install -Dm644 /dev/stdin "${pkgdir}/usr/share/libalpm/hooks/cleanjaro-xfce-settings.hook"
	install -Dm755 "${srcdir}/mxs-bgd-sym" "${pkgdir}/usr/bin/mxs-bgd-sym"
	install -Dm755 "${srcdir}/xfce-pbw.sh" "${pkgdir}/etc/skel/.config/autostart/xfce-pbw.sh"
	install -Dm755 "${srcdir}/xfce-panel-workaround.desktop" "${pkgdir}/etc/skel/.config/autostart/xfce-panel-workaround.desktop"
}
