# AArch64 multi-platform
# Maintainer: Mahmut Dikcizgi <boogiepop a~t gmx com>
# Contributor: Kevin Mihelich <kevin@archlinuxarm.org>

_pkgver=5.10
_user="radxa"
_kernel=linux-aarch64-rockchip-bsp5.10-radxa
pkgbase=$_kernel-git
pkgname=("${pkgbase}-headers" $pkgbase)
pkgver=5.10.1082079.6e429d80da
pkgrel=1
arch=('aarch64')
license=('GPL2')
url="https://github.com/${_user}"
_kernelrepo="kernel"
_overlayrepo="overlays"
_bsprepo="bsp"
_kernelbranch=linux-5.10-gen-rkr4.1
_overlaybranch=main
_bspbranch="main"
pkgdesc="Latest git Linux kernel package based on 5.10.x BSP kernel published by RADXA targetting rk3399 based rock4 and rk3588 based rock5 boards" 
makedepends=('xmlto' 'docbook-xsl' 'kmod' 'inetutils' 'bc' 'git' 'uboot-tools' 'dtc' 'python' 'gitweb-dlagent')
options=('!strip')

DLAGENTS+=('gitweb-dlagent::/usr/bin/gitweb-dlagent sync %u')
_url_kernel=gitweb-dlagent://github.com/$_user/$_kernelrepo#branch=$_kernelbranch
_url_overlay=gitweb-dlagent://github.com/$_user/$_overlayrepo.git#branch=$_overlaybranch
_url_bsp=gitweb-dlagent://github.com/$_user-repo/$_bsprepo.git#branch=$_bspbranch   

# Patch1-10 comes from Radxa: https://github.com/radxa-repo/bsp/tree/main/linux/rockchip
# Patch11: Warning Supressions for buildsystem not to quit including DistCC builds
# Patch12: Force Enabling AV1 decoder in 3588. This may be implemented in radxa git as well soon

source=("$_url_kernel"
        "$_url_overlay"
        "$_url_bsp"
        'kernel_config'
        'extlinux.radxa.template'
        '1001-disable_warnings.patch'
        '1002-rga3_uncompact_fix.patch'
        '1003-vop2_rgba2101010_capability_fix.patch'
        )

b2sums=('SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP')


pkgver(){
  #gets the commit count of both repos + _pkgrel and sums them to calculate the revision number
  cd overlays
  local _ocommits=$(gitweb-dlagent version ${_url_overlay} --pattern \{revision\})
  cd ../bsp
  local _bcommits=$(gitweb-dlagent version ${_url_bsp} --pattern \{revision\})
  cd ../kernel
  
  # the dts changes do not need to be counted as a revision to prevent too frequent updates 
  local _kcommits=$(gitweb-dlagent version ${_url_kernel} --pattern \{revision\})
  local _khash=$(gitweb-dlagent version ${_url_kernel} --pattern \{commit:.8s\})

  local _revnum=$(($_kcommits + $_ocommits + $_bcommits + $pkgrel))
  local _version="${_pkgver}.${_revnum}.${_khash}"
  echo $_version > pkgver
  printf $_version
}

prepare() {
  cd kernel
  # copy overlays to build dir
  cp -rf ../overlays/arch .

  # patch with bsp patches
  for p in $(find -L ../bsp/linux/rk356x/*/* | grep -i .patch$ | sort); do
    echo "Patching with ${p}"
    patch -p1 -N -i $p || true
  done
  
  # patch with upstream patches
  for p in ../*.patch; do
    echo "Patching with ${p}"
    patch -p1 -N -i $p || true
  done

  # this is only for local builds so there is no need to integrity check
  for p in ../../custom/*.patch; do
    echo "Custom Patching with ${p}"
    patch -p1 -N -i $p || true
  done

  echo "Setting version..."
  echo "-$pkgrel" > localversion.10-pkgrel
  echo "${pkgbase#linux}" > localversion.20-pkgname

  if [ -f ../../custom/config ]; then
    echo "Using User Specific Config"
    cp -f ../../custom/config ./.config
  else 
    cp -f arch/arm64/configs/rockchip_linux_defconfig ./.config
    for kconfig in $(find -L ../bsp/linux/rockchip/*/* | grep -i kconfig.conf$ | sort);  do
      scripts/kconfig/merge_config.sh -m .config ../bsp/$kconfig    
    done
    scripts/kconfig/merge_config.sh -m .config ../bsp/linux/rockchip/kconfig.conf
    scripts/kconfig/merge_config.sh -m .config ../kernel_config
  fi
 
}

build() {
  cd kernel

  make olddefconfig prepare
  make -s kernelrelease > version

  unset LDFLAGS
  make ${MAKEFLAGS} Image modules
  make ${MAKEFLAGS} DTC_FLAGS="-@" dtbs
}

_package() {
  pkgdesc="The linux kernel, ${_desc}"
  depends=('coreutils' 'kmod' 'initramfs')
  optdepends=('wireless-regdb: to set the correct wireless channels of your country')

  cd kernel
  
  # install dtbs
  make INSTALL_DTBS_PATH="${pkgdir}/boot/dtbs/${_kernel}" dtbs_install
  
  # install extlinux template
  install -Dm644 ../extlinux.radxa.template "$pkgdir/boot/extlinux/extlinux.radxa.template"
  
  # install modules
  make INSTALL_MOD_PATH="${pkgdir}/usr" INSTALL_MOD_STRIP=1 modules_install
  
  # copy kernel
  local _dir_module="${pkgdir}/usr/lib/modules/$(<version)"
  install -Dm644 arch/arm64/boot/Image "${_dir_module}/vmlinuz"

  # Install pkgbase
  echo "${_kernel}" | install -D -m 644 /dev/stdin "${_dir_module}/pkgbase"

  # remove reference to build host
  rm -f "${_dir_module}/"{build,source}
}

_package-headers() {
  pkgdesc="Headers and scripts for building modules for the linux kernel, ${_desc}"
  depends=("python")

  cd kernel
  local builddir="${pkgdir}/usr/lib/modules/$(<version)/build"

  echo "Installing build files..."
  install -Dt "$builddir" -m644 .config Makefile Module.symvers System.map version
  install -Dt "$builddir/kernel" -m644 kernel/Makefile
  install -Dt "$builddir/arch/arm64" -m644 arch/arm64/Makefile
  cp -t "$builddir" -a scripts

  # add xfs and shmem for aufs building
  mkdir -p "$builddir"/{fs/xfs,mm}

  echo "Installing headers..."
  cp -t "$builddir" -a include
  cp -t "$builddir/arch/arm64" -a arch/arm64/include
  install -Dt "$builddir/arch/arm64/kernel" -m644 arch/arm64/kernel/asm-offsets.s
  mkdir -p "$builddir/arch/arm"
  cp -t "$builddir/arch/arm" -a arch/arm/include

  install -Dt "$builddir/drivers/md" -m644 drivers/md/*.h
  install -Dt "$builddir/net/mac80211" -m644 net/mac80211/*.h

  # https://bugs.archlinux.org/task/13146
  install -Dt "$builddir/drivers/media/i2c" -m644 drivers/media/i2c/msp3400-driver.h

  # https://bugs.archlinux.org/task/20402
  install -Dt "$builddir/drivers/media/usb/dvb-usb" -m644 drivers/media/usb/dvb-usb/*.h
  install -Dt "$builddir/drivers/media/dvb-frontends" -m644 drivers/media/dvb-frontends/*.h
  install -Dt "$builddir/drivers/media/tuners" -m644 drivers/media/tuners/*.h

  # https://bugs.archlinux.org/task/71392
  install -Dt "$builddir/drivers/iio/common/hid-sensors" -m644 drivers/iio/common/hid-sensors/*.h

  echo "Installing KConfig files..."
  find . -name 'Kconfig*' -exec install -Dm644 {} "$builddir/{}" \;

  echo "Removing unneeded architectures..."
  local arch
  for arch in "$builddir"/arch/*/; do
    [[ $arch = */arm64/ || $arch == */arm/ ]] && continue
    echo "Removing $(basename "$arch")"
    rm -r "$arch"
  done

  echo "Removing documentation..."
  rm -r "$builddir/Documentation"

  echo "Removing broken symlinks..."
  find -L "$builddir" -type l -printf 'Removing %P\n' -delete

  echo "Removing loose objects..."
  find "$builddir" -type f -name '*.o' -printf 'Removing %P\n' -delete

  echo "Stripping build tools..."
  local file
  while read -rd '' file; do
    case "$(file -bi "$file")" in
      application/x-sharedlib\;*)      # Libraries (.so)
        strip -v $STRIP_SHARED "$file" ;;
      application/x-archive\;*)        # Libraries (.a)
        strip -v $STRIP_STATIC "$file" ;;
      application/x-executable\;*)     # Binaries
        strip -v $STRIP_BINARIES "$file" ;;
      application/x-pie-executable\;*) # Relocatable binaries
        strip -v $STRIP_SHARED "$file" ;;
    esac
  done < <(find "$builddir" -type f -perm -u+x ! -name -print0)

  echo "Adding symlink..."
  mkdir -p "$pkgdir/usr/src"
  ln -sr "$builddir" "$pkgdir/usr/src/$pkgbase"
}

for _p in ${pkgname[@]}; do
  eval "package_${_p}() {
    $(declare -f "_package${_p#$pkgbase}")
    _package${_p#${pkgbase}}
  }"
done
