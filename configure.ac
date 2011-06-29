
AC_INIT(openconnect, 3.10)
PKG_PROG_PKG_CONFIG
AC_LANG_C
AM_INIT_AUTOMAKE([foreign])

AC_ARG_WITH([openssl],
            AS_HELP_STRING([--with-openssl],
                           [Location of OpenSSL build dir]),
            [OPENSSL_CFLAGS="-I${with_openssl}/include"
             OPENSSL_LIBS="${with_openssl}/libssl.a ${with_openssl}/libcrypto.a -ldl -lz"
	     AC_SUBST(OPENSSL_CFLAGS)
	     AC_SUBST(OPENSSL_LIBS)
	     AC_ENABLE_STATIC
	     AC_DISABLE_SHARED],
	    [PKG_CHECK_MODULES(OPENSSL, openssl)
	     AC_ENABLE_SHARED
	     AC_DISABLE_STATIC])

AC_PROG_LIBTOOL

PKG_CHECK_MODULES(LIBXML2, libxml-2.0)

libproxy_hdr=no
AC_CHECK_HEADER([libproxy.h],
    [libproxy_hdr='"libproxy.h"'],
    [AC_CHECK_HEADER([proxy.h],
        [libproxy_hdr='"libproxy.h"'])])
if (test "$libproxy_hdr" != "no"); then
   AC_DEFINE([LIBPROXY_HDR], $libproxy_hdr)
   PKG_CHECK_MODULES(LIBPROXY, libproxy-1.0, AC_SUBST(LIBPROXY_PC, libproxy-1.0), dummy=yes)
fi

AC_CHECK_HEADER([if_tun.h],
    [AC_DEFINE([IF_TUN_HDR], ["if_tun.h"])],
    [AC_CHECK_HEADER([linux/if_tun.h],
        [AC_DEFINE([IF_TUN_HDR], ["linux/if_tun.h"])],
        [AC_CHECK_HEADER([net/if_tun.h],
            [AC_DEFINE([IF_TUN_HDR], ["net/if_tun.h"])],
            [AC_CHECK_HEADER([net/tun/if_tun.h],
                [AC_DEFINE([IF_TUN_HDR], ["net/tun/if_tun.h"])])])])])

AC_OUTPUT(Makefile openconnect.pc)