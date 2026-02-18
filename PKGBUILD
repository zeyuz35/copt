# Maintainer: MeronPan35 <MeronPan35>
pkgname=copt
pkgver=8.0.3
pkgrel=1
pkgdesc="Cardinal Optimizer (COPT) - Mathematical optimization solver"
arch=('x86_64')
url="https://www.shanshu.ai/copt"
license=('custom')
depends=('glibc')
source=("https://pub.shanshu.ai/download/copt/${pkgver}/linux64/CardinalOptimizer-${pkgver}-lnx64.tar.gz")
sha256sums=('9360946df8bdd8d968ec872f856913b285bc41cbe2d17dcb5458befe7b1d42e7')

package() {
  # Extract creates CardinalOptimizer-X.X.X-lnx64/copt80/
  cd "$srcdir"
  
  # Install to /opt/copt80 as per official documentation
  install -dm755 "$pkgdir/opt"
  cp -r "copt80" "$pkgdir/opt/"
  
  # Create symlinks for binaries in /usr/bin
  install -dm755 "$pkgdir/usr/bin"
  ln -s /opt/copt80/bin/copt_cmd "$pkgdir/usr/bin/copt_cmd"
  ln -s /opt/copt80/bin/copt_licgen "$pkgdir/usr/bin/copt_licgen"
  ln -s /opt/copt80/bin/coptampl "$pkgdir/usr/bin/coptampl"
  
  # Configure library path using ld.so.conf.d
  install -dm755 "$pkgdir/etc/ld.so.conf.d"
  echo "/opt/copt80/lib" > "$pkgdir/etc/ld.so.conf.d/copt.conf"
  
  # Set up COPT_HOME and COPT_LICENSE_DIR environment variables
  install -dm755 "$pkgdir/etc/profile.d"
  cat > "$pkgdir/etc/profile.d/copt.sh" << 'EOF'
# COPT environment variables
export COPT_HOME=/opt/copt80
export COPT_LICENSE_DIR=/opt/copt80
EOF
  
  # Install EULA as license
  install -Dm644 "$srcdir/copt80/copt-eula_en.pdf" "$pkgdir/usr/share/licenses/$pkgname/copt-eula_en.pdf" 2>/dev/null || true
  
  # Notify user about license requirements
  echo ""
  echo "=========================================="
  echo "COPT requires license files to function."
  echo "Please apply for a license at: https://www.shanshu.ai/copt"
  echo ""
  echo "After obtaining license.dat and license.key:"
  echo "  Recommended: Move them to \$HOME/copt/"
  echo "  Alternative: Set COPT_LICENSE_DIR to point to license directory"
  echo "=========================================="
  echo ""
}