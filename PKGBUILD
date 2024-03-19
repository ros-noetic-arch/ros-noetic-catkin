pkgdesc="ROS - Low-level build system macros and infrastructure for ROS."
url='https://wiki.ros.org/catkin'

pkgname='ros-noetic-catkin'
pkgver='0.8.10'
arch=('any')
pkgrel=3
license=('BSD')

ros_makedepends=(
)

makedepends=(
    cmake
    ${ros_makedepends[@]}
    python-catkin_pkg
    python-empy
    python
)

ros_depends=(
)

depends=(
    ${ros_depends[@]}
    python-nose
    gtest
    python-catkin_pkg
    python-empy
    gmock
    python
    ros-build-tools
)

_commit="ff31d451ce1c68d47bc058a4693aad6c0fb63a43"
_dir="catkin-${_commit}/"
source=("${pkgname}-${pkgver}.tar.gz"::"https://github.com/ros/catkin/archive/${_commit}.tar.gz")
sha256sums=('5884a16cc6e3cf28274a5d209011caef53e1b9133ed22b9866f6f0dcc0acda8a')

build() {
    # Use ROS environment variables.
    source /usr/share/ros-build-tools/clear-ros-env.sh
    [ -f /opt/ros/noetic/setup.bash ] && source /opt/ros/noetic/setup.bash

    # Create the build directory.
    [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
    cd ${srcdir}/build

    # Build the project.
    cmake ${srcdir}/${_dir} \
        -DCATKIN_BUILD_BINARY_PACKAGE=OFF \
        -DCMAKE_INSTALL_PREFIX=/opt/ros/noetic \
        -DPYTHON_EXECUTABLE=/usr/bin/python \
        -DSETUPTOOLS_DEB_LAYOUT=OFF
    make
}

package() {
    cd "${srcdir}/build"
    make DESTDIR="${pkgdir}/" install
}
