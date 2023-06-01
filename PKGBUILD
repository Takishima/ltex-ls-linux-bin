# Maintainer: Tzu-Yu Lee <leejuyuu at gmail dot com>
# Maintainer: pu <pu.mb@qq.com>
# Contributor: Dmytro Meleshko <qzlgeb.zryrfuxb@tznvy.pbz(rot13)>
_pkgname=ltex-ls
pkgname="${_pkgname}-linux-bin"
pkgver=16.0.0
pkgrel=1
pkgdesc="LTeX Language Server: LSP language server for LanguageTool with support for LaTeX, Markdown, and others"
arch=('any')
url="https://github.com/valentjn/ltex-ls"
license=('MPL2')
depends=('bash')
provides=("${_pkgname}")
conflicts=("${_pkgname}" "${_pkgname}-bin")
source=("${url}/releases/download/${pkgver}/${_pkgname}-${pkgver}-linux-x64.tar.gz")
sha256sums=('fab3201e1f2a4977fc201fde8a79f77462a202242c621149b05482896dd4a31a')


prepare() {
  cd "${srcdir}/${_pkgname}-${pkgver}"
  for file in bin/*; do
    sed -i \
        -e 's|REPO="$BASEDIR"/lib|REPO="$BASEDIR/share/java/ltex-ls"|' \
        -e 's|JAVA_HOME="$BASEDIR"/jdk-11.0.12+7|JAVA_HOME="$BASEDIR"/share/java/ltex-ls/jdk-11.0.12+7|' \
        $file
  done
}

package() {
  cd "${srcdir}/${_pkgname}-${pkgver}"
  
  local _appdir="usr/share/${_pkgname}"
  install -Dm644 "README.md" "LICENSE.md" "ACKNOWLEDGMENTS.md" "changelog.xml" -t "${pkgdir}/${_appdir}/"
  install -Dm644 "lib"/*.jar -t "${pkgdir}/usr/share/java/${_pkgname}/"
  install -Dm755 "bin"/* -t "${pkgdir}/usr/bin"
  jdk_dir=jdk-11.0.12+7
  cp -r "$jdk_dir" "${pkgdir}/usr/share/java/${_pkgname}/"
}
