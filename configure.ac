dnl Process this file with autoconf to produce a configure script.

AC_PREREQ(2.61)

AC_INIT([mate-submodules], [1.24.0], [https://mate-desktop.org])
AM_INIT_AUTOMAKE([1.9 foreign dist-xz no-dist-gzip check-news])
m4_ifdef([AM_SILENT_RULES], [AM_SILENT_RULES([yes])])

AC_CONFIG_SRCDIR([config.h.in])
AC_CONFIG_HEADER([config.h])
AC_CONFIG_MACRO_DIR([m4])

MATE_COMMON_INIT
MATE_DEBUG_CHECK([no])
MATE_COMPILE_WARNINGS

AC_PROG_CC
AM_DISABLE_STATIC
AC_PROG_LIBTOOL
PKG_PROG_PKG_CONFIG
GLIB_GSETTINGS

AC_PATH_PROG(GLIB_GENMARSHAL, glib-genmarshal)
AC_PATH_PROG(GLIB_MKENUMS, glib-mkenums)
AC_PATH_PROG(GLIB_COMPILE_RESOURCES, glib-compile-resources)

dnl ==========================================================================
dnl
dnl If you add a version number here, you *must* add an AC_SUBST line for
dnl it too, or it will never make it into the spec file!
dnl
dnl ==========================================================================

GLIB_REQUIRED=2.50.0
GIO_REQUIRED=2.50.0
GTK_REQUIRED=3.22.0
ICE_REQUIRED=1.0.0
SM_REQUIRED=1.0.0

AC_SUBST(GLIB_REQUIRED)
AC_SUBST(GIO_REQUIRED)
AC_SUBST(GTK_REQUIRED)
AC_SUBST(ICE_REQUIRED)
AC_SUBST(SM_REQUIRED)

dnl ===========================================================================

PKG_CHECK_MODULES(LIBEGG, [gtk+-3.0 >= $GTK_REQUIRED sm >= $SM_REQUIRED ice >= $ICE_REQUIRED])
AC_SUBST([LIBEGG_CFLAGS])
AC_SUBST([LIBEGG_LIBS])

dnl ===========================================================================

PKG_CHECK_MODULES(MS,				\
	glib-2.0 >= $GLIB_REQUIRED		\
	gthread-2.0						\
	gio-unix-2.0 >= $GIO_REQUIRED	\
	gtk+-3.0 >= $GTK_REQUIRED)
AC_SUBST(MS_CFLAGS)
AC_SUBST(MS_LIBS)

dnl ******************************

AC_CONFIG_FILES([Makefile
		 libegg/Makefile])
AC_OUTPUT

echo "
Configuration:

	Source code location:   ${srcdir}
	Compiler:               ${CC}
	Compiler flags:         ${CFLAGS}
	Warning flags:          ${WARN_CFLAGS}
	Linker flags:           ${LDFLAGS}
"
