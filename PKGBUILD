# Maintainer: Bernhard Landauer <oberon@manjaro.org
# Maintainer: Stefano Capitani <stefano@manjaro.org>
# Contributor: Ramon Buldó <rbuldo@gmail.com>

pkgname=manjaro-browser-settings
pkgver=20231111
pkgrel=1
pkgdesc="Manjaro Linux settings browser defaults"
arch=('any')
url="https://gitlab.manjaro.org/profiles-and-settings/manjaro-browser-settings"
license=('GPL-3.0-or-later')
makedepends=('git')
conflicts=('manjaro-firefox-settings')
replaces=('manjaro-firefox-settings')
_commit=453f952ccad2ac3b2bc81e1ee8016bc9662ad97e  # branch/master
source=("git+https://gitlab.manjaro.org/profiles-and-settings/manjaro-browser-settings.git#commit=${_commit}")
sha256sums=('84d9fe54e8c87ae5d949fdacf6f0c2f83c54368a3020227fb2c5f341f5da1eb6')

pkgver() {
  cd "$pkgname"
  git show -s --date=format:'%Y%m%d' --format=%cd
}

prepare() {
  cd "$pkgname"
}

package() {
  cd "$pkgname"
  install -d "$pkgdir"/usr/lib/{chrome,chromium,brave,{firefox,firefox-developer-edition,palemoon,thunderbird}/distribution}
  for i in chrome chromium brave; do
    cp -r chrome/* "$pkgdir/usr/lib/${i}/"
  done

  cp -r palemoon/* "$pkgdir/usr/lib/palemoon/distribution/"
  install -d "$pkgdir/etc/skel/.config/falkon/profiles"
  cp -r falkon/* "$pkgdir/etc/skel/.config/falkon/profiles/"
  install -Dm644 firefox/distribution.ini "$pkgdir/etc/manjaro-firefox.ini"
  install -Dm644 thunderbird/distribution.ini "$pkgdir/etc/manjaro-thunderbird.ini"
  install -Dm644 firefox/distribution.ini "$pkgdir/etc/manjaro-firefox-developer-edition.ini"
  sed -i 's/Firefox/Firefox Developer Edition/;s/firefox/firefox-developer-edition/' "$pkgdir/etc/manjaro-firefox-developer-edition.ini"
  install -Dm644 firefox/distribution.ini "$pkgdir/etc/manjaro-firefox-kde.ini"
  sed -i 's/Firefox/Firefox KDE Edition/' "$pkgdir/etc/manjaro-firefox-kde.ini"
  install -Dm644 firefox/all-companyname.js "$pkgdir/usr/lib/firefox/browser/defaults/preferences/all-companyname.js"
  install -Dm644 firefox/all-companyname.js "$pkgdir/usr/lib/firefox-developer-edition/browser/defaults/preferences/all-companyname.js"

  # Hooks
  install -Dm644 firefox-pre.hook "$pkgdir/usr/share/libalpm/hooks/firefox-pre.hook"
  install -Dm644 firefox-post.hook "$pkgdir/usr/share/libalpm/hooks/firefox-post.hook"
  install -Dm644 firefox-pre.hook "$pkgdir/usr/share/libalpm/hooks/firefox-dev-pre.hook"
  sed -i 's/firefox/firefox-developer-edition/g' "$pkgdir/usr/share/libalpm/hooks/firefox-dev-pre.hook"
  install -Dm644 firefox-post.hook "$pkgdir/usr/share/libalpm/hooks/firefox-dev-post.hook"
  sed -i 's/firefox/firefox-developer-edition/g' "$pkgdir/usr/share/libalpm/hooks/firefox-dev-post.hook"
  install -Dm644 firefox-kde-pre.hook "$pkgdir/usr/share/libalpm/hooks/firefox-kde-pre.hook"
  install -Dm644 firefox-kde-post.hook "$pkgdir/usr/share/libalpm/hooks/firefox-kde-post.hook"
  install -Dm644 thunderbird-pre.hook "$pkgdir/usr/share/libalpm/hooks/thunderbird-pre.hook"
  install -Dm644 thunderbird-post.hook "$pkgdir/usr/share/libalpm/hooks/thunderbird-post.hook"
}
