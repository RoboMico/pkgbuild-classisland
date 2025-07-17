# Maintainer: RoboMico <robomico at outlook dot com>

pkgname=classisland
_appname=cn.classisland.app
pkgver=1.7.103.0
pkgrel=1
pkgdesc="Class schedule displaying tool for interactive whiteboards in classrooms. (Latest release)"
arch=('x86_64' 'aarch64')
url="https://github.com/ClassIsland/ClassIsland"
license=('GPL-3.0-only')
depends=('dotnet-runtime-8.0')
makedepends=(
    'dotnet-sdk-8.0'
    'git'
)
source=(
    "git+${url}.git#tag=${pkgver}"
    "git+https://github.com/ClassIsland/EdgeTtsSharp.git#branch=classisland-v2"
    "${pkgname}.sh"
)
sha256sums=(
    'SKIP'
    'SKIP'
    '5342aed758213e2068c1a41c696b317b935fe491158fc750f454156686a35388'
)

prepare () {
    cd "${srcdir}/ClassIsland"
    cp -r "${srcdir}/EdgeTtsSharp" ./vendors
    git remote set-url origin https://github.com/ClassIsland/ClassIsland # resolve the SourceLink issue
}
build() {
    cd "${srcdir}/ClassIsland/ClassIsland.Desktop"
    mkdir -p ./_output/${pkgname}
    dotnet build -c Release -o ./_output/${pkgname}
}
package() {
    mkdir -p "${pkgdir}/opt" "${pkgdir}/usr/bin"
    cp -r "${srcdir}/ClassIsland/ClassIsland.Desktop/_output/${pkgname}" "${pkgdir}/opt"
    printf "deb" > "${pkgdir}/opt/${pkgname}/PackageType"
    install -Dm644 "${srcdir}/ClassIsland/ClassIsland/Assets/AppLogo_AppLogo.svg" "${pkgdir}/usr/share/icons/hicolor/scalable/apps/${pkgname}.svg"
    install -Dm644 "${srcdir}/ClassIsland/ClassIsland/Assets/ShortcutTemplates/${_appname}.desktop" "${pkgdir}/usr/share/applications/${_appname}.desktop"
    sed -i "s/{0}/${pkgver}/" "${pkgdir}/usr/share/applications/${_appname}.desktop"
    sed -i "s/{1}/\/usr\/bin\/${pkgname}/" "${pkgdir}/usr/share/applications/${_appname}.desktop"
    install -Dm755 "${srcdir}/${pkgname}.sh" "${pkgdir}/usr/bin/${pkgname}"
}
