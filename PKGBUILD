pkgname=kdeplasma-applets-networkmanagement-git
pkgver=20111029
pkgrel=1
pkgdesc="KDE4 Network Management plasmoid, git version"
arch=('i686' 'x86_64')
url="http://kde.org/"
license=('GPL')
depends=('kdebase-workspace' 'networkmanager' 'libnm-qt-git')
makedepends=('cmake'  'python2' 'automoc4' 'git' 'mobile-broadband-provider-info'  'openconnect')
optdepends=('mobile-broadband-provider-info: allow to add new mobile connection'
	    'openconnect: Cisco AnyConnect compatible VPN client')
provides=('kdeplasma-applets-networkmanagement')
conflicts=('kdeplasma-applets-networkmanagement')
install=kdeplasma-applets-networkmanagement-git.install

_gitroot="git://anongit.kde.org/networkmanagement"
_gitname=networkmanagement

build() {

cd $srcdir

  msg "Connecting to the GIT server...."
  
  if [[ -d $srcdir/$_gitname ]] ; then
    cd $_gitname
    git pull origin
    git checkout master
    msg "The local files are updated."
  else
    git clone $_gitroot
  fi
  
  msg "GIT checkout done"
  msg "Starting make..."
  if [[ -d ${srcdir}/${_gitname}-build ]]; then
    msg "Cleaning the previous build directory..."
    rm -rf ${srcdir}/${_gitname}-build
  fi
  mkdir $srcdir/$_gitname-build
  cd $srcdir/$_gitname-build
  cmake $startdir/src/$_gitname -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_BUILD_TYPE=Release
}

package() {
  cd ${srcdir}/$_gitname-build
  make DESTDIR=${pkgdir} install
}
