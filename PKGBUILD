# Contributor: Leonidas <marek@xivilization.net>
pkgname=homeshick-git
pkgver=20130403
pkgrel=1
pkgdesc="bash stand-in for homesick by technicalpickles"
arch=(any)
url="https://github.com/andsens/homeshick"
license=('BSD')
makedepends=('git')

_gitroot="git://github.com/andsens/homeshick.git"
_gitname="homeshick"

build() {
  cd "$srcdir"
  msg "Connecting to GIT server...."
  if [ -d $_gitname ] ; then
    cd $_gitname && git pull origin
    msg "The local files are updated."
  else
    git clone $_gitroot $_gitname
  fi

  msg "GIT checkout done or server timeout"
  # patch out the paths
  sed -i "s|source \$homeshick|source /usr/lib/homeshick|" "$srcdir"/$_gitname/home/.homeshick
}

package() {
  # copy the 'binary' *ahem* script
  install -D "$srcdir"/$_gitname/home/.homeshick "$pkgdir"/usr/bin/homeshick
  # copy the utils scripts
  mkdir -p "$pkgdir"/usr/lib/$_gitname/utils/
  install "$srcdir"/$_gitname/utils/*.sh "$pkgdir"/usr/lib/homeshick/utils
  # copy the licenses
  mkdir -p "$pkgdir"/usr/share/licenses/$pkgname/
  install -m=644 -t "$pkgdir"/usr/share/licenses/$pkgname/ "$srcdir"/$_gitname/LICENSE*
}
