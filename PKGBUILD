# Maintainer: Hannes Rist <hrist@selfnet.de>

pkgname=cubit-git
pkgver=20120425
pkgrel=1
pkgdesc="Cubit is an open source game in which you walk around in a world that consists only of cubes. "
arch=('x86_64')
url="http://www.cubit-project.com/"
license=('GPL')
depends=('ftgl' 'boost-libs' 'sdl_net' 'sdl_mixer' 'sdl_image' 'bullet' 'glew' 'sqlite' 'hicolor-icon-theme')
makedepends=('git' 'boost' 'cmake')
provides=('cubit-git')
conflicts=('cubit')
md5sums=('215d01b0080fc59997662479a2c1c344')
source=('cubit-git.install')

_gitroot="git://git.cubit-project.com/cubit.git"
_gitname="cubit"

build() {
  msg 'Connecting to GIT server...'

  if [[ -d $_gitname ]]; then
    ( cd "$_gitname" && git pull origin )
    msg 'The local files are updated.'
  else
    git clone "$_gitroot"
  fi

  msg 'GIT checkout done or server timeout'
  msg 'Starting make...'

  rm -rf $_gitname-build
  git clone $_gitname{,-build}
  cd $_gitname-build

  cmake -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_BUILD_TYPE=Release .

  make

}

check() {
  echo "no checks here"
}

package() {
  cd "$_gitname-build"

  make DESTDIR="$pkgdir" install

}

# vim: set ts=2 sw=2 et:
