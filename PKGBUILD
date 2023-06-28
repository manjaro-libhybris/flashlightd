# Maintainer: Bardia Moshiri <fakeshell@bardia.tech>

pkgname=flashlightd
pkgver=7
pkgrel=1
_commit=6c934562a089a7f117a53da74436db39a68f559a
pkgdesc="simple daemon to manage camera flash light using gstreamer"
url="https://github.com/droidian/flashlightd"
license=("GPL3")
arch=('i686' 'x86_64' 'armv6h' 'armv7h' 'aarch64')
makedepends=('gstreamer' 'glib2' 'vala' 'git' 'meson')
source=("git+https://github.com/droidian/flashlightd#commit=${_commit}")
sha256sums=('SKIP')

pkgver() {
  cd "${srcdir}/${pkgname}"
  git describe --tags | sed 's/^v//;s/-/+/g;s|pureos/||g;s|droidian/||g;s|bookworm/||g'
}

prepare() {
  cd "${srcdir}/${pkgname}"
}

build() {
  rm -rf build
  arch-meson "${srcdir}/${pkgname}" build 
  meson compile -C build
}

package() {
  DESTDIR="${pkgdir}" ninja -C build install
  install -Dm644 "${srcdir}/${pkgname}"/org.droidian.Flashlightd.service ${pkgdir}/usr/lib/systemd/user/flashlightd.service
  mkdir -p ${pkgdir}/usr/lib/systemd/user/gnome-session.target.wants/
  sed -i 's#/usr/libexec/flashlightd#/usr/lib/flashlightd#g' ${pkgdir}/usr/lib/systemd/user/flashlightd.service
  ln -s /usr/lib/systemd/user/flashlightd.service ${pkgdir}/usr/lib/systemd/user/gnome-session.target.wants/flashlightd.service
}

