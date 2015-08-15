# Maintainer: Chipster Julien <julien dot chipster @ archlinux dot fr>

pkgname=go-mailmotiond
pkgver=0.1
pkgrel=4
pkgdesc="It send email with attachment when it found any picture on specified directory (designed to work with motion)"
arch=('any')
url="https://github.com/Chipsterjulien/go-mailmotiond"
license=('WTFPL')
makedepends=('go' 'git')
options=('!strip' '!emptydirs')
conflit=('mailmotiond')
backup=('etc/mailmotiond/mailmotiond.conf')
source=("$pkgname-$pkgver.tar.gz")
install=go-mailmotiond.install
sha256sums=('12a7859f9930ea120a298e8cebdbda53f5b423486eeb0e2826c4d36265f49b1e')

build() {
  GOPATH_exist=1
  if [ -z $GOPATH ]; then
    # path don't exit
    GOPATH_exist=0

    # create gopath directory
    mkdir -p .gopath/{bin,src}
    # export var
    export GOPATH=~/.gopath
  fi

  # Getting some lib
  go get github.com/scorredoira/email
  go get bitbucket.org/zombiezen/cardcpx/natsort
  go get github.com/vaughan0/go-ini

  cd "$pkgname-$pkgver"

  go build

  if [ $GOPATH_exist == 0 ]; then
    rm -rf ~/.gopath
    export GOPATH=
  fi
}

package() {
  cd "$pkgname-$pkgver"
  	
	# Create directory and copy files
	install -Dm644 "cfg/mailmotiond.conf" "$pkgdir/etc/mailmotiond/mailmotiond.conf"
	install -Dm644 "cfg/mailmotiond.service" "$pkgdir/usr/lib/systemd/system/mailmotiond.service"
	install -Dm644 "cfg/errors.log" "$pkgdir/var/log/mailmotiond/errors.log"

  #install -Dm755 "$pkgname-$pkgver" "$pkgdir/usr/bin/$pkgname"
  #install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  
  install -Dm755 "$pkgname-$pkgver" "$pkgdir/usr/bin/mailmotiond"
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/mailmotiond/LICENSE"
}

# vim:set ts=2 sw=2 et:
