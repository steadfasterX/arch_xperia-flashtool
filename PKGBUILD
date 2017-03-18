# Maintainer: Muflone http://www.muflone.com/contacts/english/

pkgname=xperia-flashtool
_realname=flashtool
pkgver=0.9.23.1
pkgrel=1
pkgdesc="A S1 protocol flashing software for Sony Xperia phones"
arch=('i686' 'x86_64')
url="http://www.flashtool.net/"
license=('unknown')
depends=('libselinux')
makedepends=('p7zip')
source=("flashtool-${pkgver}-linux.tar.7z"
        "${pkgname}.sh")

# needed for FWUL:
downloadurl="https://forum.xda-developers.com/devdb/project/dl/?id=23693&task=get"

# backup 1 is on datafilehost (no DDL): http://www.datafilehost.com/get.php?file=efb20448
# backup 2 is on AFH (no DDL): https://www.androidfilehost.com/?fid=457095661767145062
# backup 3 is on ZippyShare: http://www99.zippyshare.com/v/VGK1tzim/file.html

sha256sums=('254ed7e992b5a3617c95b00d539251f5eb1476d5bd5e16cd03eaf092249b042c'
            'b6b91cec623461e7b31bc3250045071350237962388ecd6df46bb437bc536803')
options=('!strip')

build() {
  tar xf "${_realname}-${pkgver}-linux.tar"
}

package() {
  # Remove useless files for the selected architecture
  pushd "FlashTool/x10flasher_lib" > /dev/null
  if [ "$CARCH"=="x86_64" ]; then
    rm -rf "adb.linux.x86" "fastboot.linux.x86" "unyaffs.linux.x86" \
      "linjre32" "linux/lib32" "swtlin/swt32.jar"
  else
    rm -rf "adb.linux.x64" "fastboot.linux.x64" "unyaffs.linux.x64" \
      "linjre64" "linux/lib64" "swtlin/swt64.jar"
  fi
  popd > /dev/null
  # Install all the program files
  install -m 755 -d "${pkgdir}/usr/lib/${pkgname}"
  cp -rt "${pkgdir}/usr/lib/${pkgname}" FlashTool/*
  # Install launcher scripts
  install -m 755 -d "${pkgdir}/usr/bin"
  install -m 755 "${pkgname}.sh" "${pkgdir}/usr/bin/${pkgname}"
}
