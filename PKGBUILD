# Maintainer: rsunix <rsunix g-mail>                                                                                                                                                                                                                              
# Based on jre: https://aur.archlinux.org/packages/jdk/                                                                                                                                                                                                              
                                                                                                                                                                                                                                                                     
pkgname=('jre8-oraclejdk' 'jdk8-oraclejdk')
#pkgname=('oraclejdk8-src' 'oraclejdk8-javafxsrc')

pkgbase=java8-oraclejdk
_java_ver=8                                                                                                                                                                                                                                                             
_jdk_update=92                                                                                                                                                                                                                                                            
_jdk_build=b14                                                                                                                                                                                                                                                           
pkgver=${_java_ver}.u${_jdk_update}
_oracle_ver=${_java_ver}u${_jdk_update}
pkgrel=1                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            
arch=('i686' 'x86_64' 'armv6h' 'armv7h' 'aarch64')                                                                                                                                                                                                                                      
url=http://www.oracle.com/technetwork/java/javase/downloads/index.html                                                                                                                                                                                               
license=('custom')                                                                                                                                                                                                                                                   

# Variables
DLAGENTS=('http::/usr/bin/curl -fLC - --retry 3 --retry-delay 3 -b oraclelicense=a -o %o %u')

source=("http://download.oracle.com/otn-pub/java/jce/$_java_ver/jce_policy-$_java_ver.zip"
        "policytool-oraclejdk8.desktop"
        "jconsole-oraclejdk8.desktop"
        "jmc-oraclejdk8.desktop"
        "jvisualvm-oraclejdk8.desktop") 
md5sums=('b3c7031bc65c28c2340302065e7d00d3'
         'cdddb2bff911ee5225d7997177ea83b8'
         'd2afd3c4437086f5cafc3ea80cd4325c'
         '35667c2c35ebcce0459b1af415404a80'
         '8368a37da3afa365a9b1284585982679')

source_i686=("http://download.oracle.com/otn-pub/java/jdk/${_oracle_ver}-${_jdk_build}/jdk-${_oracle_ver}-linux-i586.tar.gz")
md5sums_i686=('0f2839ff1066438123dac3404702a3ef')             
             
source_x86_64=("http://download.oracle.com/otn-pub/java/jdk/${_oracle_ver}-${_jdk_build}/jdk-${_oracle_ver}-linux-x64.tar.gz") 
md5sums_x86_64=('65a1cc17ea362453a6e0eb4f13be76e4')
             
source_armv6h=("http://download.oracle.com/otn-pub/java/jdk/${_oracle_ver}-${_jdk_build}/jdk-${_oracle_ver}-linux-arm32-vfp-hflt.tar.gz")
md5sums_armv6h=('2eee13c2769c867993c257a77e7470f1')

source_armv7h=("http://download.oracle.com/otn-pub/java/jdk/${_oracle_ver}-${_jdk_build}/jdk-${_oracle_ver}-linux-arm32-vfp-hflt.tar.gz")
md5sums_armv7h=('2eee13c2769c867993c257a77e7470f1')

source_aarch64=("http://download.oracle.com/otn-pub/java/jdk/${_oracle_ver}-${_jdk_build}/jdk-${_oracle_ver}-linux-arm64-vfp-hflt.tar.gz")
md5sums_aarch64=('ffe0ba53d3f9077d3ed6e0ca88aece5e')

case "${CARCH}" in
  'x86_64' | 'i686') _JARCH=amd64 ;;
  'armv6h' | 'armv7h' | 'aarch64' ) _JARCH=arm ;;
esac

_jdkname=oraclejdk8
_jvmdir=/usr/lib/jvm/java-8-oraclejdk
_imgdir=jdk1.${_java_ver}.0_${_jdk_update}
_deletefolder=(lib/desktop)
              
package_jre8-oraclejdk() {
    pkgdesc='Oracle Java 8 full runtime environment'
    depends=('java-runtime-common' 'ca-certificates-utils' 'nss' 'xdg-utils' 'hicolor-icon-theme')
    optdepends=('java-rhino: for some JavaScript support'
              'alsa-lib: for basic sound support'
              'gtk2: for the Gtk+ look and feel - desktop usage')

    case "${CARCH}" in
        'x86_64' | 'i686') 
            provides=('java-runtime-headless=8' 'java-runtime-headless-openjdk=8' 'java-runtime=8' 'java-runtime-openjdk=8' 'java-web-start') 
        ;;
        'armv6h' | 'armv7h' | 'aarch64' ) 
            provides=('java-runtime-headless=8' 'java-runtime-headless-openjdk=8' 'java-runtime=8' 'java-runtime-openjdk=8') 
        ;;
    esac
          
    install=install_jre8-oraclejdk.sh
    
    _backup_etc=(etc/java-8-oraclejdk/${_JARCH}/jvm.cfg
                etc/java-8-oraclejdk/calendars.properties
                etc/java-8-oraclejdk/content-types.properties
                etc/java-8-oraclejdk/flavormap.properties                
                etc/java-8-oraclejdk/images/cursors/cursors.properties
                etc/java-8-oraclejdk/logging.properties
                etc/java-8-oraclejdk/management/jmxremote.access
                etc/java-8-oraclejdk/management/jmxremote.password
                etc/java-8-oraclejdk/management/management.properties
                etc/java-8-oraclejdk/management/snmp.acl
                etc/java-8-oraclejdk/net.properties
                etc/java-8-oraclejdk/psfont.properties.ja
                etc/java-8-oraclejdk/psfontj2d.properties
                etc/java-8-oraclejdk/security/java.policy                
                etc/java-8-oraclejdk/security/java.security
                etc/java-8-oraclejdk/sound.properties)
                
    case "${CARCH}" in
        'x86_64' | 'i686') 
            _backup_etc=("${_backup_etc[@]}"
                         etc/java-8-oraclejdk/javafx.properties
                         etc/java-8-oraclejdk/security/javaws.policy
                        )
        ;;
        'armv6h' | 'armv7h' | 'aarch64' )                
        ;;
    esac
    backup=(${_backup_etc[@]})
    
    msg2 "Install desktop files."    
    case "${CARCH}" in
        'x86_64' | 'i686')            
            pushd "${srcdir}/${_imgdir}/jre/lib/desktop"
                install -m 755 -d "${pkgdir}"/usr/share
                cp -a applications icons "${pkgdir}"/usr/share
            popd
        ;;
        'armv6h' | 'armv7h' | 'aarch64' );;
    esac
    install -m 755 -d "${pkgdir}"/usr/share/applications
    install -m 644 "${srcdir}"/policytool-oraclejdk8.desktop \
      "${pkgdir}"/usr/share/applications/policytool-oraclejdk8.desktop
    
    msg2 "Install main files."
    cd "${srcdir}/${_imgdir}/jre"    
    install -d -m 755 "${pkgdir}${_jvmdir}/jre/"
    cp -a bin lib "${pkgdir}${_jvmdir}/jre"
    
    msg2 "Set config files"
    mv "${pkgdir}${_jvmdir}"/jre/lib/management/jmxremote.password{.template,}
    mv "${pkgdir}${_jvmdir}"/jre/lib/management/snmp.acl{.template,}
    
    msg2 "Remove directory"
    for f in ${_deletefolder[@]}; do
        rm -rf "${pkgdir}${_jvmdir}/jre/${f}"
    done
    
    msg2 "Remove files"
    rm -f ${pkgdir}${_jvmdir}/jre/lib/fontconfig.*.bfc
    rm -f ${pkgdir}${_jvmdir}/jre/lib/fontconfig.*.properties.src
    
    msg2 "Man pages"
    pushd "${pkgdir}${_jvmdir}/jre/bin"
    install -d -m 755 "${pkgdir}"/usr/share/man/{,ja/}man1/
    for file in *; do
        if [ -f "${srcdir}/${_imgdir}/man/man1/${file}.1" ]; then
            install -m 644 "${srcdir}/${_imgdir}/man/man1/${file}.1" \
            "${pkgdir}/usr/share/man/man1/${file}-${_jdkname}.1"            
        fi
        if [ -f "${srcdir}/${_imgdir}/man/ja/man1/${file}.1" ]; then
            install -m 644 "${srcdir}/${_imgdir}/man/ja/man1/${file}.1" \
            "${pkgdir}/usr/share/man/ja/man1/${file}-${_jdkname}.1"            
        fi
    done
    popd
    
    msg2 "Link JKS keystore from ca-certificates-utils"
    rm -f "${pkgdir}${_jvmdir}/jre/lib/security/cacerts"
    ln -sf /etc/ssl/certs/java/cacerts "${pkgdir}${_jvmdir}/jre/lib/security/cacerts"
    
    msg2 "Install license"
    install -d -m 755 "${pkgdir}/usr/share/licenses/${pkgbase}/"
    install -m 644 COPYRIGHT LICENSE THIRD*.txt \
                 "${pkgdir}/usr/share/licenses/${pkgbase}"
    ln -sf /usr/share/licenses/${pkgbase} "${pkgdir}/usr/share/licenses/${pkgname}"

    
    msg2 "Move config files that were set in _backup_etc from ./lib to /etc"
    for file in ${_backup_etc[@]}; do
      _filepkgpath=${_jvmdir}/jre/lib/${file#etc/java-8-oraclejdk/}
      install -D -m 644 "${pkgdir}${_filepkgpath}" "${pkgdir}/${file}"
      ln -sf /${file} "${pkgdir}${_filepkgpath}"
    done
    
    msg2 "Installing Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy Files..."
    install -m 644 "${srcdir}"/UnlimitedJCEPolicyJDK${_java_ver}/*.jar "${pkgdir}${_jvmdir}"/jre/lib/security/
}

package_jdk8-oraclejdk() {
  pkgdesc='Oracle Java 8 development kit'
  depends=('java-environment-common' "jre8-oraclejdk=${pkgver}-${pkgrel}")
  provides=('java-environment=8' 'java-environment-openjdk=8')
  install=install_jdk8-oraclejdk.sh

  cd "${srcdir}/${_imgdir}"

  msg2 "Main files"
  install -d -m 755 "${pkgdir}${_jvmdir}"
  cp -a include lib "${pkgdir}${_jvmdir}"

  msg2 "'bin' files"
  pushd bin

  # 'java-rmi.cgi' will be handled separately as it should not be in the PATH and has no man page
  for b in $(ls | grep -v java-rmi.cgi); do
    if [ -e ../jre/bin/${b} ]; then
      # Provide a link of the jre binary in the jdk/bin/ directory
      ln -s ../jre/bin/${b} "${pkgdir}${_jvmdir}/bin/${b}"
    else
      # Copy binary to jdk/bin/
      install -D -m 755 ${b} "${pkgdir}${_jvmdir}/bin/${b}"
      # Copy man page
      if [ -f ../man/man1/${b}.1 ]; then
        install -D -m 644 ../man/man1/${b}.1 "${pkgdir}/usr/share/man/man1/${b}-${_jdkname}.1"
      fi
      if [ -f ../man/ja/man1/${b}.1 ]; then
        install -D -m 644 ../man/ja/man1/${b}.1 "${pkgdir}/usr/share/man/ja/man1/${b}-${_jdkname}.1"
      fi  
    fi
  done
  popd
  

  msg2 "Install desktop files."
  install -m 755 -d "${pkgdir}"/usr/share/applications
  install -m 644 "${srcdir}"/jconsole-oraclejdk8.desktop \
  "${pkgdir}"/usr/share/applications/jconsole-oraclejdk8.desktop 
  
  case "${CARCH}" in
    'x86_64' | 'i686') 
       install -m 644 "${srcdir}"/jmc-oraclejdk8.desktop \
       "${pkgdir}"/usr/share/applications/jmc-oraclejdk8.desktop   
       install -m 644 "${srcdir}"/jvisualvm-oraclejdk8.desktop \
       "${pkgdir}"/usr/share/applications/jvisualvm-oraclejdk8.desktop
       ;;
    'armv6h' | 'armv7h' | 'aarch64' );;
  esac

  # Handling 'java-rmi.cgi' separately
  install -D -m 755 bin/java-rmi.cgi "${pkgdir}${_jvmdir}/bin/java-rmi.cgi"

  msg2 "Link license"
  install -d -m 755 "${pkgdir}/usr/share/licenses/"
  ln -sf /usr/share/licenses/${pkgbase} "${pkgdir}/usr/share/licenses/${pkgname}"
}

#package_oraclejdk8-javafxsrc() {
#  pkgdesc='Oracle Java 8 javafx sources'
#
#  install -D "${srcdir}/${_imgdir}/javafx-src.zip" "${pkgdir}${_jvmdir}/javafx-src.zip"
#}

#package_oraclejdk8-src() {
#  pkgdesc='Oracle Java 8 sources'

#  install -D "${srcdir}/${_imgdir}/src.zip" "${pkgdir}${_jvmdir}/src.zip"
#}
