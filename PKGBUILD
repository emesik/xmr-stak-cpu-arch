pkgname=xmr-stak-cpu-git
pkgver=r244.7ad999d
pkgrel=1
pkgdesc="Monero CPU miner"
arch=('x86_64')
url="https://github.com/nicehash/xmr-stak-cpu"
license=('GPL3')
makedepends=('git' 'cmake' 'fakeroot')
depends=('libmicrohttpd' 'openssl' 'hwloc')
source=('git+https://github.com/fireice-uk/xmr-stak-cpu.git'
        'no-donate.patch'
        'config-log.patch'
        'xmr-stak-cpu.service')
sha256sums=('SKIP'
            'c973333e53efa4a94042f5b7c5d5d1b6995bb2cf261ac0ac7f735d93d795a6a6'
            '008318b504bcab7173628e181f5cf4fa1af9cfd683430723744f1c9cf50621ba'
            '159c2ca7df5bfc7acd00622f565ca264f943bcff35d28ae24664df3d291a9118')
install=xmr-stak-cpu.install
backup=('etc/xmr-stak-cpu.json')

pkgver() {
    cd "$srcdir/xmr-stak-cpu"
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
    cd "$srcdir/xmr-stak-cpu"
    #patch -p1 -i ../../no-donate.patch
    patch -p1 -i ../../config-log.patch
}

build() {
    cd "$srcdir/xmr-stak-cpu"
    cmake .
    make
}

package() {
    install -D -m755 "$srcdir/xmr-stak-cpu/bin/xmr-stak-cpu" -t "$pkgdir/usr/bin/"
    install -D -m644 "$srcdir/xmr-stak-cpu/config.txt" "$pkgdir/etc/xmr-stak-cpu.json"
    install -D -m644 "../xmr-stak-cpu.service" "$pkgdir/usr/lib/systemd/system/xmr-stak-cpu.service"
}
