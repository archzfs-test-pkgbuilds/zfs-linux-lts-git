# Maintainer: Jan Houben <jan@nexttrex.de>
# Contributor: Jesus Alvarez <jeezusjr at gmail dot com>
#
# This PKGBUILD was generated by the archzfs build scripts located at
#
# http://github.com/archzfs/archzfs
#
# ! WARNING !
#
# The archzfs packages are kernel modules, so these PKGBUILDS will only work with the kernel package they target. In this
# case, the archzfs-linux-lts packages will only work with the default linux-lts package! To have a single PKGBUILD target
# many kernels would make for a cluttered PKGBUILD!
#
# If you have a custom kernel, you will need to change things in the PKGBUILDS. If you would like to have AUR or archzfs repo
# packages for your favorite kernel package built using the archzfs build tools, submit a request in the Issue tracker on the
# archzfs github page.
#
pkgbase="zfs-linux-lts-git"
pkgname=("zfs-linux-lts-git" "zfs-linux-lts-git-headers")

pkgver=2018.08.17.r4677.g802715b74.4.14.63.1
pkgrel=1
makedepends=("linux-lts-headers=4.14.63-1" "git")
arch=("x86_64")
url="http://zfsonlinux.org/"
source=("git+https://github.com/zfsonlinux/zfs.git#commit=802715b74a23a58d66028699a99eb141c85b7447"
        "upstream-ac09630-Fix-zpl_mount-deadlock.patch"
        "upstream-9f64c1e-Linux-4.18-compat-inode-timespec_timespec64.patch"
        "upstream-9161ace-Linux-compat-4.18-check_disk_size_change.patch")
sha256sums=("SKIP" 
            "1799f6f7b2a60a23b66106c9470414628398f6bfc10da3d0f41c548bba6130e8"
            "03ed45af40850c3a51a6fd14f36c1adc06501c688a67afb13db4fded6ec9db1d"
            "afbde4a2507dff989404665dbbdfe18eecf5aba716a6513902affa0e4cb033fe")
license=("CDDL")
depends=("kmod" "zfs-utils-common-git=2018.08.17.r4677.g802715b74" "linux-lts=4.14.63-1")

build() {
    cd "${srcdir}/zfs"
    ./autogen.sh
    ./configure --prefix=/usr --sysconfdir=/etc --sbindir=/usr/bin --libdir=/usr/lib \
                --datadir=/usr/share --includedir=/usr/include --with-udevdir=/lib/udev \
                --libexecdir=/usr/lib/zfs-0.7.9 --with-config=kernel \
                --with-linux=/usr/lib/modules/4.14.63-1-lts/build \
                --with-linux-obj=/usr/lib/modules/4.14.63-1-lts/build
    make
}

package_zfs-linux-lts-git() {
    pkgdesc="Kernel modules for the Zettabyte File System."
    install=zfs.install
    provides=("zfs")
    groups=("archzfs-linux-lts-git")
    conflicts=('zfs-linux-lts' 'spl-linux-lts-git')
    replaces=("spl-linux-lts-git")
    cd "${srcdir}/zfs"
    make DESTDIR="${pkgdir}" install
    cp -r "${pkgdir}"/{lib,usr}
    rm -r "${pkgdir}"/lib
    # Remove src dir
    rm -r "${pkgdir}"/usr/src
}

package_zfs-linux-lts-git-headers() {
    pkgdesc="Kernel headers for the Zettabyte File System."
    conflicts=('zfs-archiso-linux-headers' 'zfs-archiso-linux-git-headers' 'zfs-linux-hardened-headers' 'zfs-linux-hardened-git-headers' 'zfs-linux-lts-headers'  'zfs-linux-headers' 'zfs-linux-git-headers' 'zfs-linux-vfio-headers' 'zfs-linux-vfio-git-headers' 'zfs-linux-zen-headers' 'zfs-linux-zen-git-headers' )
    cd "${srcdir}/zfs"
    make DESTDIR="${pkgdir}" install
    rm -r "${pkgdir}/lib"
    # Remove reference to ${srcdir}
    sed -i "s+${srcdir}++" ${pkgdir}/usr/src/zfs-*/4.14.63-1-lts/Module.symvers
}
