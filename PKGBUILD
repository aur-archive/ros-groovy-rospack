pkgdesc="ROS - Package Tool"
url='http://www.ros.org/'

pkgname='ros-groovy-rospack'
pkgver='2.1.21'
arch=('i686' 'x86_64')
pkgrel=1
license=('BSD')
makedepends=('ros-build-tools')

depends=(
  ros-groovy-catkin
  python2
  gtest
  boost
  tinyxml
  pkg-config)

build() {
  [ -f /opt/ros/groovy/setup.bash ] && source /opt/ros/groovy/setup.bash
  if [ -d ${srcdir}/rospack ]; then
    cd ${srcdir}/rospack
    git fetch origin --tags
    git reset --hard release/groovy/rospack/${pkgver}-0
  else
    git clone -b release/groovy/rospack/${pkgver}-0 git://github.com/ros-gbp/rospack-release.git ${srcdir}/rospack
  fi
  [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
  cd ${srcdir}/build
  /usr/share/ros-build-tools/fix-python-scripts.sh ${srcdir}/rospack
  cmake ${srcdir}/rospack -DCATKIN_BUILD_BINARY_PACKAGE=ON -DCMAKE_INSTALL_PREFIX=/opt/ros/groovy -DPYTHON_EXECUTABLE=/usr/bin/python2 -DPYTHON_INCLUDE_DIR=/usr/include/python2.7 -DPYTHON_LIBRARY=/usr/lib/libpython2.7.so -DSETUPTOOLS_DEB_LAYOUT=OFF
  make
}

package() {
  cd "${srcdir}/build"
  make DESTDIR="${pkgdir}/" install
}
