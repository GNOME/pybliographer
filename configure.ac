dnl -*- m4 -*-
dnl This file is part of pybliographer
dnl
dnl Copyright (C) 1998-2004 Frederic GOBRY
dnl Email : gobry@pybliographer.org
dnl          
dnl This program is free software; you can redistribute it and/or
dnl modify it under the terms of the GNU General Public License
dnl as published by the Free Software Foundation; either version 2 
dnl of the License, or (at your option) any later version.
dnl   
dnl This program is distributed in the hope that it will be useful,
dnl but WITHOUT ANY WARRANTY; without even the implied warranty of
dnl MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
dnl GNU General Public License for more details. 
dnl
dnl You should have received a copy of the GNU General Public License
dnl along with this program; if not, write to the Free Software 
dnl Foundation, Inc., 59 Temple Place - Suite 330, Boston, MA  02111-1307, USA.
dnl
dnl
dnl Process this file with autoconf to produce a configure script.

AC_PREREQ(2.57)

AC_INIT([pybliographer], [1.4.0])
AM_INIT_AUTOMAKE
m4_ifdef([AM_SILENT_RULES], [AM_SILENT_RULES([yes])])

AC_CONFIG_SRCDIR(pybliographer.in)

AC_PROG_LN_S

GETTEXT_PACKAGE=AC_PACKAGE_TARNAME
AC_SUBST([GETTEXT_PACKAGE])
AC_DEFINE_UNQUOTED([GETTEXT_PACKAGE], "$GETTEXT_PACKAGE", [Gettext package])

AM_GNU_GETTEXT_VERSION([0.19.8])
AM_GNU_GETTEXT

AM_PATH_PYTHON(2.7)
PKG_CHECK_MODULES(PYGTK, pygtk-2.0 >= 2.24.0)

# PACKAGERS
AC_ARG_ENABLE([depchecks],
   [AS_HELP_STRING([--disable-depchecks],
      [skip dependency checks (while building packages for instance)])],
   [],
   [enable_depchecks=yes])

AC_MSG_CHECKING([for module requirements])
if test x${enable_depchecks} = "xyes" ; then
	# Check that recode and bibtex work as expected
	${PYTHON} -c "import _recode as r, sys
sys.exit(not r.recode(r.request('latin1..latex'), 'abcd') == 'abcd')" 2>/dev/null
	if test $? -ne 0; then
		AC_MSG_ERROR([Broken recode version])
	fi

	${PYTHON} -c "import _bibtex;_bibtex.next_unfiltered" 2>/dev/null
	if test $? -ne 0; then
		AC_MSG_ERROR([python-bibtex module required with function 'next_unfiltered'])
	fi
else
	AC_MSG_RESULT([disabled by user])
fi



# Documentation
YELP_HELP_INIT

AC_CONFIG_FILES(
	Makefile 
	po/Makefile.in
	scripts/Makefile
	tests/Makefile
	Pyblio/Makefile
	Pyblio/GnomeUI/Makefile
	Pyblio/GnomeUI/glade/Makefile
	Pyblio/Format/Makefile
	Pyblio/Output/Makefile
	Pyblio/ConfDir/Makefile
	Pyblio/Style/Makefile
	help/Makefile
	Styles/Makefile
	data/Makefile
	data/icons/Makefile
	data/pixmaps/Makefile
	data/src/Makefile
)


AC_OUTPUT

echo "pybliographer is now configured. Type make to build it"
