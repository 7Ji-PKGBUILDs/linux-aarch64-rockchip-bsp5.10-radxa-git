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
makedepends=('xmlto' 'docbook-xsl' 'kmod' 'inetutils' 'bc' 'git' 'uboot-tools' 'dtc' 'python')
options=('!strip')

# Patch1-10 comes from Radxa: https://github.com/radxa-repo/bsp/tree/main/linux/rockchip
# Patch11: Warning Supressions for buildsystem not to quit including DistCC builds
# Patch12: Force Enabling AV1 decoder in 3588. This may be implemented in radxa git as well soon

source=("git+https://github.com/$_user/$_kernelrepo.git#branch=$_kernelbranch"
        "git+https://github.com/$_user/$_overlayrepo.git#branch=$_overlaybranch"
        "git+https://github.com/$_user-repo/$_bsprepo.git#branch=$_bspbranch"
        'kernel_config'
        'extlinux.radxa.template'
        '0001-VENDOR-Add-Radxa-overlays.patch'
        '0002-Fix-dangling-pointer-compiler-bug.patch'
        '0003-Disable-tristate-for-non-modules.patch'
        '0004-Disable-tristate-for-modules-that-uses-unexported-sy.patch'
        '0005-Disable-tristate-for-builtin-dependencies.patch'
        '0006-Revert-dma-buf-sw_sync-build-sw-sync-as-module-for-g.patch'
        '0007-Disable-tristate-for-essential-boot-services.patch'
        '0008-Modfy-GPU-node-for-Panfrost-driver.patch'
        '0009-VENDOR-Version-tagging-linux-libc-dev-as-well.patch'
        '0010-Add-ROCK-4-Core-IO-Board-Fuhai.patch'
        '0011-gcc-ignore-stringop-overread-warnings.patch'
        '0012-Enable_AV1_decoder_on_3588.patch'
        '0020-dma-buf-add-dma_resv_get_singleton-v2.patch'
        '0021-dma-buf-Add-an-API-for-exporting-sync-files-v14.patch'
        '0022-dma-buf-Add-an-API-for-importing-sync-files-v10.patch'
        '0023-make-4-4-silence.patch'
        '0024-rga3_uncompact_fix.patch'
        '0025-vop2_rgba2101010_capability_fix.patch'
        )

b2sums=('SKIP'
        'SKIP'
        'SKIP'
        '3dd5229d0b171cada8c72dd2a34525febd3c7674b9757af471c1972082d949ec31ffff6b5eefde2d9366158570692ab111cd3bf65c1cf382c4c464077d89c8c8'
        '6589d8de3ca07a2d354a3135a39f78e9b9889267c0863e7db274ca9345c53a4eb60efb861b15fb11ebef7a8eac7af5ad74a8cb9f9fb65d92e3718e04818b59ca'
        '4908b5a94c02a4eb0fe8bb9983289f1b8acbb1b8ebb541643c7ec4ac5de87be949efbdec839d34603b045500b13033f836385bdbf3e935fcd8d221f71028d604'
        'e612cf028aaf8f99c2735a6e1640170af51e62aa86a8cc795694ac089b2f31be93e67c6ee394cd22d290a787cd9f064861b0bb173033069710881280432ad45f'
        'bde631de66dde60339c7fa306b06a9100ac41adaeb16788c800157324a288a97629c41dda5076698c1ef71b8b7f44b5eba619b6aac92d0d5c59e796fb2aa407a'
        'bc56e29a4b54bc20cda18023667c115a5819bb1fff9ac9fbe6296d5b89897f82d65fa99e9d013bf25fc0a17e22be219cfef7eb55ceaa6a228da92db8b2a20406'
        '16b725f25bc150675888dcc03125cd285f2c73f7955d90d521af9a139d717836afab07a995f7018e19cdad41964061800503e40e32656ee54bf69c22e8c8a53f'
        '8a6c96251c48048ff653285646347853d5df5264d1bf0bf798a48d3636480263125f92c5cb21f7d4b4988b6d831636d34de1b882c0209110178117e3ea1a0630'
        'f5ab48ee96b6df65ec20742e5bb2badffa7ed926f5020d64bdcfe1fe924fff9cafdb70c7983084f4294ab5663c5b56eeb51e96df176253175e9bde52121c3164'
        'd7c4496318bd3fc5294af88bcdeafa49b04683d1e1fe7312b0317872fdecb929ef8e62b86332e87eddd49c1f5e7ddb9a59372dcbf0514158f7d75947e81f7d8d'
        '7dc970eebf837940c67ae61f809f9e0cc6ae9e2a033ca7975b2c4055190b23ddd190170e75949834d54818f08016743d66c6ede5175f6cf988bec2e6aa4f008d'
        'b3b9b04b0f73d07c1927c0def7e5cc991144a7e65a01dab4ec1b2dd01f092e001da3fc07e852ebefb1530509e25a99730217a9208b6a26b0333c288ca1151935'
        '1551af94cb79fd74e7921b89b4ee00a550f183da94ddf3ca4ad8c4443b62a388cd967af42985e18de3ad1242629a3a7d0e9e61f4b67ae5c95c39c8b388302e0a'
        '7c61be00b97a8acb759c35f23969cdfb4e739a8c88fd147d2af4594fa14100a2da90b160e04b8632c3dca703ff2c1973138d7f765c5b9a7039c6aae7f0078d9a'
        'c3487e98544c2d36e60f3c3f2fabff94b3d4b157f2858c67c526dd8fdac8685dae3c2c7c07d4398b898943257f16ddc469dc633619862fe5b8da76fd317bca42'
        'b9eb4d0856adc68350dba4d7a8076cddddf97061244cd9aea422c549f2dd2f1f951087835ee957ce0117bf468f0d3068d7f52ce5f486ce00263101af4ab2ba68'
        'eccbf9cf7efd9f5e4f0d12fc59b7f86e1a212ef35e99250f9bc836efe675b1abd81c8997994c8986aa5ec1886e6908abd13473e57523846a15a355fa13beeec7'
        '786a02f742015903c6c6fd852552d272912f4740e15847618a86e217f71f5419d25e1031afee585313896444934eb04b903a685b1448b755d56f701afe9be2ce'
        'b9d177486c7c80539a267bb37adb3cf7d70c20d5f58e1e39d20c36cced69e2210e6120ebf88befeaf075b05731f5321eb3048ec9ef1518b93ecec882a3e33fcb'
        'dffe835d816dab78fadaa62a1b561b4d3dd172a4fc8bb2f858957da2858f73b0f32c7458166ab5d5ed41b4aed96e9fb86a40dd4ec75b76ece54850521c9c7d26')


pkgver(){
  # gets the commit count of both repos + _pkgrel and sums them to calculate the revision number
  cd overlays
  local _ocommits="$(git rev-list --count HEAD arch/arm64/boot/dts/rockchip)"
  cd ../bsp
  local _bcommits="$(git rev-list --count HEAD linux)"
  cd ../kernel
  local _kcommits="$(git rev-list --count HEAD)"
  local _kcommit="$(git rev-parse --short HEAD)"

  local _revnum=$(($_kcommits + $_ocommits + $_bcommits + $_fcommits + $pkgrel))
  local _version="${_pkgver}.${_revnum}.${_kcommit}"
  echo $_version > pkgver
  printf $_version
}

prepare() {
  cd kernel
  cp -rf ../overlays/arch .

  # patch with radxa patches and dont care if they fail
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
    for kconfig in $(find -L ../bsp/linux/rockchip/*/* | grep -i kconfig.conf$ | sort)
    do
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
