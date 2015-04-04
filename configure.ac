#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ(2.59)
AC_INIT([vbackup], [1.0.0~pre1], [v13@v13.gr])
AM_INIT_AUTOMAKE

AC_ARG_WITH( tar,
	[AC_HELP_STRING([--with-tar=PATH],
		[Full path to GNU tar])	],
	[GTAR="$with_tar"])

AC_ARG_WITH( find,
	[AC_HELP_STRING([--with-find=PATH],
		[Full path to GNU find])],
	[GFIND="$with_find"])

# Checks for programs.

# Check for GNU tar
if test -z "$GTAR" ; then
	AC_PATH_PROG([GTAR], [tar], [])
fi

if test -z "$GFIND" ; then
	AC_PATH_PROG([GFIND], [find], [])
fi

AC_CACHE_CHECK(
	[for GNU tar],
	[vbackup_cv_gtar],
	[
	 	if test -z "$GTAR" ; then
			vbackup_cv_gtar="no"
		else
			T=`$GTAR --version 2>&1 |grep 'GNU'`
			if test -z "$T" ; then
				vbackup_cv_gtar="no"
			else
				vbackup_cv_gtar="$GTAR"
			fi
		fi
	])

if test "$vbackup_cv_gtar" = "no" ; then
	GTAR=""
else
	GTAR="$vbackup_cv_gtar"
fi

# Check for GNU find
AC_CACHE_CHECK(
	[for GNU find],
	[vbackup_cv_gfind],
	[
	 	if test -z "$GFIND" ; then
			vbackup_cv_gfind="no"
		else
			T=`$GFIND --version 2>&1 |grep 'GNU'`
			if test -z "$T" ; then
				vbackup_cv_gfind="no"
			else
				vbackup_cv_gfind="$GFIND"
			fi
		fi
	])

if test "$vbackup_cv_gfind" = "no" ; then
	GFIND=""
else
	GFIND="$vbackup_cv_gfind"
fi

# Check for xfsdump and other programs
PATH2="$PATH:/sbin:/usr/sbin:/usr/local/sbin"
AC_PATH_PROG([XFSDUMP], [xfsdump], [], [$PATH2])
AC_PATH_PROG([FDISK], [fdisk], [], [$PATH2])
AC_PATH_PROG([SFDISK], [sfdisk], [], [$PATH2])
AC_PATH_PROG([MDADM], [mdadm], [], [$PATH2])
AC_PATH_PROG([LVDISPLAY], [lvdisplay], [], [$PATH2])
AC_PATH_PROG([VGDISPLAY], [vgdisplay], [], [$PATH2])
AC_PATH_PROG([PVDISPLAY], [pvdisplay], [], [$PATH2])
AC_PATH_PROG([SCP], [scp], [], [$PATH2])
AC_PATH_PROG([OPENSSL], [openssl], [], [$PATH2])
AC_PATH_PROG([SLAPCAT], [slapcat], [], [$PATH2])
AC_PATH_PROG([MD5SUM], [md5sum], [], [$PATH2])

# Check for echo that accepts newlines
T=`echo -e ""`
if test -z "$T" ; then
	ECHO_E="echo -e"
else
	ECHO_E="echo"
fi

# Checks for libraries.

# Checks for header files.

# Checks for typedefs, structures, and compiler characteristics.

AC_SUBST([mybindir], [${datadir}/vbackup/bin])
AC_SUBST([myhelperdir], [${datadir}/vbackup/helpers])
AC_SUBST([myscriptdir], [${datadir}/vbackup/scripts])
AC_SUBST([myconfdir], [${sysconfdir}/vbackup])
dnl AC_SUBST([sampledir], [${myconfdir}/samples])
dnl AC_SUBST([sampledir], [${docdir}/samples])
AC_SUBST([sampledir], [${datadir}/vbackup/samples])
AC_SUBST([wizdir], [${datadir}/vbackup/wizard])

AC_SUBST([GTAR])
AC_SUBST([GFIND])
AC_SUBST([XFSDUMP])
AC_SUBST([FDISK])
AC_SUBST([SFDISK])
AC_SUBST([MDADM])
AC_SUBST([LVDISPLAY])
AC_SUBST([VGDISPLAY])
AC_SUBST([PVDISPLAY])
AC_SUBST([SCP])
AC_SUBST([ECHO_E])

# Checks for library functions.
AC_CONFIG_FILES([Makefile
		scripts/Makefile
		scripts/bin/Makefile
		scripts/bin/run
		scripts/bin/vbackup
		scripts/bin/common
		scripts/bin/vbackup-wizard
		scripts/scripts/Makefile
		scripts/scripts/mount/Makefile
		scripts/scripts/db/Makefile
		scripts/scripts/misc/Makefile
		scripts/scripts/fs/Makefile
		scripts/scripts/pkg/Makefile
		scripts/scripts/netcp/Makefile
		scripts/scripts/encrypt/Makefile
		scripts/wizard/Makefile
		])
AC_OUTPUT

ERR=0
if test -z "$GTAR" ; then
	echo 
	echo " * No GNU tar was found. The tar method will not function."
	ERR=1
fi

if test -z "$GFIND" ; then
	echo 
	echo " * No GNU find was found. This script will not work."
	ERR=1
fi

if test -z "$XFSDUMP" ; then
	echo 
	echo " * xfsdump was not found. The xfsdump method will not function."
	ERR=1
fi

if test -z "$SCP" ; then
	echo
	echo " * scp was not found. The scp method will not function."
	ERR=1
fi

test "x$ERR" = "x1" && echo

true
