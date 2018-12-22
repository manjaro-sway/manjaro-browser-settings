# Maintainer: Ramon Buldó <rbuldo@gmail.com>
# Maintainer: Bernhard Landauer <oberon@manjaro.org
# Maintainer: Stefano Capitani <stefano@manjaro.org>

pkgname=manjaro-browser-settings
pkgver=20181222
pkgrel=1
pkgdesc="Manjaro Linux settings browser defaults"
arch=('any')
url="https://gitlab.manjaro.org/profiles-and-settings/$pkgname"
license=('GPL')
_gitcommit=4d4ed7f1e11ab0898d5d1249824db88b00257c0f
conflicts=('manjaro-firefox-settings')
replaces=('manjaro-firefox-settings')
source=("$pkgname-$_gitcommit.tar.gz::$url/-/archive/$_gitcommit/$pkgname-$_gitcommit.tar.gz")
md5sums=('ae9a5041800617bb11a3f38e57c35579')

pkgver() {
  date +%Y%m%d
}

package() {
  cd $pkgname-$_gitcommit
  mkdir -p $pkgdir/usr/lib/{chrome,chromium,brave,{firefox,firefox-developer-edition,palemoon,thunderbird}/distribution}
  for i in chrome chromium brave; do
  	cp chrome/* $pkgdir/usr/lib/$i
  done
  cp palemoon/* $pkgdir/usr/lib/palemoon/distribution
  install -dm755 $pkgdir/etc/skel/.config/falkon/profiles
  cp -r falkon/* $pkgdir/etc/skel/.config/falkon/profiles
  install -Dm644 firefox/distribution.ini $pkgdir/etc/manjaro-firefox.ini
  install -Dm644 thunderbird/distribution.ini $pkgdir/etc/manjaro-thunderbird.ini
  install -Dm644 firefox/distribution.ini $pkgdir/etc/manjaro-firefox-developer-edition.ini
  sed -i 's/Firefox/Firefox Developer Edition/;s/firefox/firefox-developer-edition/' $pkgdir/etc/manjaro-firefox-developer-edition.ini
  install -Dm644 firefox/distribution.ini $pkgdir/etc/manjaro-firefox-kde.ini
  sed -i 's/Firefox/Firefox KDE Edition/' $pkgdir/etc/manjaro-firefox-kde.ini

#Hook
  install -Dm644 firefox-pre.hook $pkgdir/usr/share/libalpm/hooks/firefox-pre.hook
  install -Dm644 firefox-post.hook $pkgdir/usr/share/libalpm/hooks/firefox-post.hook
  install -Dm644 firefox-pre.hook $pkgdir/usr/share/libalpm/hooks/firefox-dev-pre.hook
  sed -i 's/firefox/firefox-developer-edition/g' $pkgdir/usr/share/libalpm/hooks/firefox-dev-pre.hook
  install -Dm644 firefox-post.hook $pkgdir/usr/share/libalpm/hooks/firefox-dev-post.hook
  sed -i 's/firefox/firefox-developer-edition/g' $pkgdir/usr/share/libalpm/hooks/firefox-dev-post.hook
  install -Dm644 firefox-kde-pre.hook $pkgdir/usr/share/libalpm/hooks/firefox-kde-pre.hook
  install -Dm644 firefox-kde-post.hook $pkgdir/usr/share/libalpm/hooks/firefox-kde-post.hook
  install -Dm644 thunderbird-pre.hook $pkgdir/usr/share/libalpm/hooks/thunderbird-pre.hook
  install -Dm644 thunderbird-post.hook $pkgdir/usr/share/libalpm/hooks/thunderbird-post.hook
}
