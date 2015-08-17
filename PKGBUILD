# Maintainer: Serge Zirukin <ftrvxmtrx@gmail.com>

pkgname=ocaml-argot
pkgver=1.1
pkgrel=1
pkgdesc="Enhanced HTML generator for the ocamldoc tool of OCaml"
arch=('i686' 'x86_64')
url=("http://argot.x9c.fr")
# LGPL + linking exception
license=('GPLv3')
depends=('ocaml' 'ocaml-findlib')
makedepends=('ocaml')
_pkgname=argot
source=(http://argot.x9c.fr/distrib/${_pkgname}-${pkgver}.tar.gz
        Makefile.patch)
md5sums=('8957d817c8a7d70048fb2645a62e946c'
         '2cd92b308ae2a1e9e7a36f78ef91ad01')

build () {
  cd "${srcdir}/${_pkgname}-${pkgver}"

  chmod +x ./configure
  ./configure || return 1
  make all || return 1
}

package () {
  OCAMLFIND_DESTDIR="${pkgdir}$(ocamlfind printconf destdir)"
  mkdir -p "$OCAMLFIND_DESTDIR"
  cd "${srcdir}/${_pkgname}-${pkgver}"

  patch -Np1 -i $startdir/Makefile.patch
  sed "s|PATH_INSTALL=|PATH_INSTALL=${pkgdir}/|" -i Makefile
  OCAMLFIND_DESTDIR="${OCAMLFIND_DESTDIR}" make install || return 1
  rm -f "${OCAMLFIND_DESTDIR}/argot/myocamlbuild.cmi"
  install -D "doc/argot.pdf" "${pkgdir}/usr/share/doc/${_pkgname}/argot.pdf"
}
