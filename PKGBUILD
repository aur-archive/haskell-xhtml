# Maintainer: Vesa Kaihlavirta <vesa@archlinux.org>
# Contributor: Arch Haskell Team <arch-haskell@haskell.org>
# Package generated by cabal2arch 0.7.6

_hkgname=xhtml
pkgname=haskell-xhtml
pkgver=3000.2.0.5
pkgrel=1
pkgdesc="Combinators for producing XHTML 1.0, including the Strict, Transitional and Frameset variants."
url="http://hackage.haskell.org/package/xhtml"
license=('custom:BSD3')
arch=('i686' 'x86_64')
depends=('ghc=7.4.1-2' 'sh')
source=(http://hackage.haskell.org/packages/archive/${_hkgname}/$pkgver/${_hkgname}-$pkgver.tar.gz)
install=${pkgname}.install
md5sums=('d51e20de416b825aba6b874a221acfc4')

build() {
    cd ${srcdir}/${_hkgname}-${pkgver}
    runhaskell Setup configure -O -p --enable-split-objs --enable-shared --prefix=/usr \
      --docdir=/usr/share/doc/${pkgname} --libsubdir=\$compiler/site-local/\$pkgid
    runhaskell Setup build
    runhaskell Setup haddock
    runhaskell Setup register   --gen-script
    runhaskell Setup unregister --gen-script
    sed -i -r -e "s|ghc-pkg.*unregister[^ ]* |&'--force' |" unregister.sh
}

package() {
    cd ${srcdir}/${_hkgname}-${pkgver}
    install -D -m744 register.sh   ${pkgdir}/usr/share/haskell/${pkgname}/register.sh
    install    -m744 unregister.sh ${pkgdir}/usr/share/haskell/${pkgname}/unregister.sh
    install -d -m755 ${pkgdir}/usr/share/doc/ghc/html/libraries
    ln -s /usr/share/doc/${pkgname}/html ${pkgdir}/usr/share/doc/ghc/html/libraries/${_hkgname}
    runhaskell Setup copy --destdir=${pkgdir}
    install -D -m644 LICENSE ${pkgdir}/usr/share/licenses/${pkgname}/LICENSE
    rm -f ${pkgdir}/usr/share/doc/${pkgname}/LICENSE
}
