# $Id: Makefile.in,v 1.95 2015/08/05 09:24:06 tom Exp $
##############################################################################
# Copyright (c) 1998-2014,2015 Free Software Foundation, Inc.                #
#                                                                            #
# Permission is hereby granted, free of charge, to any person obtaining a    #
# copy of this software and associated documentation files (the "Software"), #
# to deal in the Software without restriction, including without limitation  #
# the rights to use, copy, modify, merge, publish, distribute, distribute    #
# with modifications, sublicense, and/or sell copies of the Software, and to #
# permit persons to whom the Software is furnished to do so, subject to the  #
# following conditions:                                                      #
#                                                                            #
# The above copyright notice and this permission notice shall be included in #
# all copies or substantial portions of the Software.                        #
#                                                                            #
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR #
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,   #
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL    #
# THE ABOVE COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER      #
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING    #
# FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER        #
# DEALINGS IN THE SOFTWARE.                                                  #
#                                                                            #
# Except as contained in this notice, the name(s) of the above copyright     #
# holders shall not be used in advertising or otherwise to promote the sale, #
# use or other dealings in this Software without prior written               #
# authorization.                                                             #
##############################################################################
#
# Author: Thomas E. Dickey 1996-on
#
# Makefile for ncurses source code.
#
# This makes the ncurses utility programs.
#
# The variable 'srcdir' refers to the source-distribution, and can be set with
# the configure script by "--srcdir=DIR".
#
# The rules are organized to produce the libraries for the configured models,
# and the programs with the configured default model.

# turn off _all_ suffix rules; we'll generate our own
.SUFFIXES:

SHELL		= /bin/sh

THIS		= Makefile

CF_MFLAGS 	= 


x		= 
o		= .o

MODEL		= ../obj_s
DESTDIR		= 
top_srcdir	= ..
srcdir		= .
prefix		= /usr/local
exec_prefix	= ${prefix}
bindir		= ${exec_prefix}/bin
libdir		= ${exec_prefix}/lib
includedir	= ${prefix}/include
datarootdir	= /usr/share
datadir		= ${datarootdir}
includesubdir	= /ncursesw

INCLUDEDIR	= $(DESTDIR)$(includedir)$(includesubdir)

PACKAGE		= ncursesw

LIBTOOL		= 
LIBTOOL_OPTS	= 
LIBTOOL_CLEAN	= 
LIBTOOL_COMPILE	= 
LIBTOOL_LINK	= ${CC}
LIBTOOL_INSTALL	= 
LIBTOOL_UNINSTALL = 

INSTALL		= /usr/bin/install -c
INSTALL_PROG	= ${INSTALL}
transform	= s,x,x,

AWK		= awk
LN_S		= ln -s -f

CTAGS		= ctags
ETAGS		= 

CC		= gcc
CPP		= gcc -E
CFLAGS		= -O2 -no-cpp-precomp --param max-inline-insns-single=1200

INCDIR		= $(top_srcdir)/include
CPPFLAGS	= -DHAVE_CONFIG_H -I. -I../include   -D_DARWIN_C_SOURCE -DNDEBUG

CCFLAGS		= $(CPPFLAGS) $(CFLAGS)

CFLAGS_LIBTOOL	= $(CCFLAGS)
CFLAGS_NORMAL	= $(CCFLAGS)
CFLAGS_DEBUG	= $(CCFLAGS) -g -DTRACE
CFLAGS_PROFILE	= $(CCFLAGS) -pg
CFLAGS_SHARED	= $(CCFLAGS) -dynamic

CFLAGS_DEFAULT	= $(CFLAGS_SHARED)

REL_VERSION	= 5.4.9
ABI_VERSION	= 5.4
LOCAL_LIBDIR	= /Users/kevans/aapl-git/ncurses/ncurses/lib

LD		= ld
LINK		=  $(LIBTOOL_LINK)
LDFLAGS		=   -Wl,-search_paths_first
RPATH_LIST	= ${libdir}

LDFLAGS_LIBTOOL	= $(LDFLAGS) $(CFLAGS_LIBTOOL)
LDFLAGS_NORMAL	= $(LDFLAGS) $(CFLAGS_NORMAL)
LDFLAGS_DEBUG	= $(LDFLAGS) $(CFLAGS_DEBUG)
LDFLAGS_PROFILE	= $(LDFLAGS) $(CFLAGS_PROFILE)
LDFLAGS_SHARED	= $(LDFLAGS) $(CFLAGS_SHARED) 

LDFLAGS_DEFAULT	= $(LDFLAGS_SHARED)

LIBS_TIC	= -L../lib  -lncursesw -lncursesw   
LDFLAGS_TIC	= -L../lib $(LDFLAGS_SHARED) $(LIBS_TIC)

LIBS_TINFO	=  -lncursesw   
LDFLAGS_TINFO	= -L../lib $(LDFLAGS_SHARED) $(LIBS_TINFO)

LINT		= 
LINT_OPTS	= 
LINT_LIBS	= -lncurses 

AUTO_SRC = \
	termsort.c \
	transform.h

# tic relies on direct access to the terminfo database
GET_PROGS = infocmp$x clear$x tabs$x tput$x tset$x toe$x
PUT_PROGS =  tic$x
PROGS = $(PUT_PROGS) $(GET_PROGS)

# Default library, for linking applications
DEPS_CURSES = ../lib/libncursesw.dylib

HEADER_DEPS	= \
	../include/curses.h \
	$(INCDIR)/term_entry.h \
	$(INCDIR)/tic.h \
	$(INCDIR)/nc_alloc.h

################################################################################
all:		$(AUTO_SRC) $(PROGS)

sources:	$(AUTO_SRC)

install: 	$(AUTO_SRC) install.progs
uninstall: uninstall.progs

# this line simplifies the configure-script
libs \
install.libs \
uninstall.libs:

TRANSFORM = sed 's/$x$$//'|sed '$(transform)'|sed 's/$$/$x/'

# transformed names for installing files
actual_captoinfo = `echo captoinfo$x| $(TRANSFORM)`
actual_clear     = `echo clear$x|     $(TRANSFORM)`
actual_infocmp   = `echo infocmp$x|   $(TRANSFORM)`
actual_infotocap = `echo infotocap$x| $(TRANSFORM)`
actual_init      = `echo init$x|      $(TRANSFORM)`
actual_reset     = `echo reset$x|     $(TRANSFORM)`
actual_tabs      = `echo tabs$x|      $(TRANSFORM)`
actual_tic       = `echo tic$x|       $(TRANSFORM)`
actual_toe       = `echo toe$x|       $(TRANSFORM)`
actual_tput      = `echo tput$x|      $(TRANSFORM)`
actual_tset      = `echo tset$x|      $(TRANSFORM)`

# transformed names for comparing at runtime
define_captoinfo = `echo captoinfo|   $(TRANSFORM)`
define_infotocap = `echo infotocap|   $(TRANSFORM)`
define_init      = `echo init|        $(TRANSFORM)`
define_reset     = `echo reset|       $(TRANSFORM)`

transform.h :
	echo "#ifndef __TRANSFORM_H"					>$@
	echo "#define __TRANSFORM_H 1"					>>$@
	echo "#include <progs.priv.h>"					>>$@
	echo "extern bool same_program(const char *, const char *);"	>>$@
	-$(SHELL) -c 'if test -n "$x" ; then echo "#define SUFFIX_IGNORED \"$x\"">>$@; fi'
	echo "#define PROG_CAPTOINFO \"$(define_captoinfo)\""		>>$@
	echo "#define PROG_INFOTOCAP \"$(define_infotocap)\""		>>$@
	echo "#define PROG_RESET     \"$(define_reset)\""		>>$@
	echo "#define PROG_INIT      \"$(define_init)\""		>>$@
	echo "#endif /* __TRANSFORM_H */"				>>$@

install.progs: $(AUTO_SRC) $(PROGS) $(DESTDIR)$(bindir)
	$(LIBTOOL_INSTALL) $(INSTALL_PROG) tic$x     $(DESTDIR)$(bindir)/$(actual_tic)
	$(LIBTOOL_INSTALL) $(INSTALL_PROG) toe$x     $(DESTDIR)$(bindir)/$(actual_toe)
	@echo "linking $(actual_infotocap) to $(actual_tic)"
	-@rm -f $(DESTDIR)$(bindir)/$(actual_infotocap)
	(cd $(DESTDIR)$(bindir) && $(LN_S) $(actual_tic) $(actual_infotocap))
	@echo "linking $(actual_captoinfo) to $(actual_tic)"
	-@rm -f $(DESTDIR)$(bindir)/$(actual_captoinfo)
	(cd $(DESTDIR)$(bindir) && $(LN_S) $(actual_tic) $(actual_captoinfo))
	$(LIBTOOL_INSTALL) $(INSTALL_PROG) infocmp$x $(DESTDIR)$(bindir)/$(actual_infocmp)
	$(LIBTOOL_INSTALL) $(INSTALL_PROG) clear$x   $(DESTDIR)$(bindir)/$(actual_clear)
	$(LIBTOOL_INSTALL) $(INSTALL_PROG) tabs$x    $(DESTDIR)$(bindir)/$(actual_tabs)
	$(LIBTOOL_INSTALL) $(INSTALL_PROG) tput$x    $(DESTDIR)$(bindir)/$(actual_tput)
	$(LIBTOOL_INSTALL) $(INSTALL_PROG) tset$x    $(DESTDIR)$(bindir)/$(actual_tset)
	@echo "linking $(actual_reset) to $(actual_tset)"
	-@rm -f $(DESTDIR)$(bindir)/$(actual_reset)
	(cd $(DESTDIR)$(bindir) && $(LN_S) $(actual_tset) $(actual_reset))

uninstall.progs:
	-@$(LIBTOOL_CLEAN) rm -f $(DESTDIR)$(bindir)/$(actual_tic)
	-@$(LIBTOOL_CLEAN) rm -f $(DESTDIR)$(bindir)/$(actual_toe)
	-@rm -f $(DESTDIR)$(bindir)/$(actual_captoinfo)
	-@rm -f $(DESTDIR)$(bindir)/$(actual_infotocap)
	-@$(LIBTOOL_CLEAN) rm -f $(DESTDIR)$(bindir)/$(actual_infocmp)
	-@$(LIBTOOL_CLEAN) rm -f $(DESTDIR)$(bindir)/$(actual_clear)
	-@$(LIBTOOL_CLEAN) rm -f $(DESTDIR)$(bindir)/$(actual_tabs)
	-@$(LIBTOOL_CLEAN) rm -f $(DESTDIR)$(bindir)/$(actual_tput)
	-@$(LIBTOOL_CLEAN) rm -f $(DESTDIR)$(bindir)/$(actual_tset)
	-@rm -f $(DESTDIR)$(bindir)/$(actual_reset)

$(DESTDIR)$(bindir) :
	mkdir -p $@

#
# Utilities normally built by make all start here
#

DEPS_TIC = \
	$(MODEL)/tic$o \
	$(MODEL)/dump_entry$o \
	$(MODEL)/tparm_type$o \
	$(MODEL)/transform$o

tic$x: $(DEPS_TIC) $(DEPS_CURSES) transform.h
	 $(LINK) $(DEPS_TIC) $(LDFLAGS_TIC) -o $@

DEPS_TOE = \
	$(MODEL)/toe$o

toe$x: $(DEPS_TOE) $(DEPS_CURSES)
	 $(LINK) $(DEPS_TOE) $(LDFLAGS_TIC) -o $@

DEPS_CLEAR = \
	$(MODEL)/clear$o

clear$x: $(DEPS_CLEAR) $(DEPS_CURSES)
	 $(LINK) $(DEPS_CLEAR) $(LDFLAGS_TINFO) -o $@

DEPS_TABS = \
	$(MODEL)/tabs$o

tabs$x: $(DEPS_TABS) $(DEPS_TABS)
	 $(LINK) $(DEPS_TABS) $(LDFLAGS_TINFO) -o $@

DEPS_TPUT = \
	$(MODEL)/tput$o \
	$(MODEL)/tparm_type$o \
	$(MODEL)/transform$o

tput$x: $(DEPS_TPUT) $(DEPS_CURSES) transform.h
	 $(LINK) $(DEPS_TPUT) $(LDFLAGS_TINFO) -o $@

DEPS_INFOCMP = \
	$(MODEL)/infocmp$o \
	$(MODEL)/dump_entry$o

infocmp$x: $(DEPS_INFOCMP) $(DEPS_CURSES)
	 $(LINK) $(DEPS_INFOCMP) $(LDFLAGS_TIC) -o $@

DEPS_TSET = \
	$(MODEL)/tset$o \
	$(MODEL)/transform$o

tset$x: $(DEPS_TSET) $(DEPS_CURSES) transform.h
	 $(LINK) $(DEPS_TSET) $(LDFLAGS_TINFO) -o $@

termsort.c: $(srcdir)/MKtermsort.sh
	$(SHELL) $(srcdir)/MKtermsort.sh $(AWK) $(srcdir)/../include/Caps >$@

#
# Utility productions start here
#

tags:
	$(CTAGS) *.[ch]

#TAGS:
#	$(ETAGS) *.[ch]

mostlyclean ::
	-rm -f core tags TAGS *~ *.bak *.i *.ln *.atac trace

clean :: mostlyclean
	-$(SHELL) -c "if test -n '$x' ; then $(MAKE) clean x=''; fi"
	-rm -f $(AUTO_SRC)
	-rm -f $(PROGS)
	-rm -rf .libs *.dSYM

distclean :: clean
	-rm -f Makefile

realclean :: distclean

# These rules are used to allow "make -n" to work on a clean directory-tree
../include/hashsize.h \
../include/parametrized.h \
../include/term.h :
	cd ../include; $(MAKE) $(CF_MFLAGS)
$(DEPS_CURSES) :
	cd ../ncurses; $(MAKE) $(CF_MFLAGS)

lint:
	$(LINT) $(LINT_OPTS) $(CPPFLAGS) $(srcdir)/tic.c     $(srcdir)/dump_entry.c $(LINT_LIBS)
	$(LINT) $(LINT_OPTS) $(CPPFLAGS) $(srcdir)/toe.c     $(srcdir)/dump_entry.c $(LINT_LIBS)
	$(LINT) $(LINT_OPTS) $(CPPFLAGS) $(srcdir)/clear.c                          $(LINT_LIBS)
	$(LINT) $(LINT_OPTS) $(CPPFLAGS) $(srcdir)/infocmp.c $(srcdir)/dump_entry.c $(LINT_LIBS)
	$(LINT) $(LINT_OPTS) $(CPPFLAGS) $(srcdir)/tabs.c                           $(LINT_LIBS)
	$(LINT) $(LINT_OPTS) $(CPPFLAGS) $(srcdir)/tput.c                           $(LINT_LIBS)
	$(LINT) $(LINT_OPTS) $(CPPFLAGS) $(srcdir)/tset.c    $(srcdir)/dump_entry.c $(LINT_LIBS)

###############################################################################
# The remainder of this file is automatically generated during configuration
###############################################################################

# Generated by CF_LIB_RULES
resulting.map: 
	sed  -e "s/NCURSES\([WT]\+\)\?_/NCURSES\15.4_/g" -e "/deprecated in ABI5.4/d" <  >$@

clean::
	rm -f resulting.map

# generated by mk-0th.awk
#   libname:    progsw
#   subsets:    ticlib+termlib+ext_tinfo+base+widechar+ext_funcs

.SUFFIXES: .c .cc .h .i .ii
.c.i :
	$(CPP) $(CPPFLAGS) $< >$@
.cc.ii :
	$(CPP) $(CPPFLAGS) $< >$@
.h.i :
	$(CPP) $(CPPFLAGS) $< >$@

C_SRC = \
	$(srcdir)/clear.c \
	$(srcdir)/tic.c \
	$(srcdir)/toe.c \
	$(srcdir)/dump_entry.c \
	$(srcdir)/infocmp.c \
	$(srcdir)/tabs.c \
	$(srcdir)/tparm_type.c \
	$(srcdir)/tput.c \
	$(srcdir)/tset.c \
	$(srcdir)/transform.c

lintlib :
	@echo no action needed

# generated by mk-1st.awk (subset=ticlib+termlib+ext_tinfo+base+widechar+ext_funcs)
#  name:          progsw
#  traces:        DEBUG
#  MODEL:         SHARED
#  CXX_MODEL:     SHARED
#  model:         obj_s
#  prefix:        lib
#  suffix:        .dylib
#  subset:        ticlib+termlib+ext_tinfo+base+widechar+ext_funcs
#  driver:        no
#  ShlibVer:      abi
#  ShlibVerInfix: yes
#  SymLink:       ln -s -f
#  TermlibRoot:   ncursesw
#  TermlibSuffix: .dylib
#  ReLink:        yes
#  DoLinks:       yes
#  rmSoLocs:      no
#  ldconfig:      
#  overwrite:     no
#  depend:        ../include/ncurses_cfg.h ./progs.priv.h
#  host:          arm-apple-darwin23.0.0

SHARED_OBJS = \
	../obj_s/clear$o \
	../obj_s/tic$o \
	../obj_s/toe$o \
	../obj_s/dump_entry$o \
	../obj_s/infocmp$o \
	../obj_s/tabs$o \
	../obj_s/tparm_type$o \
	../obj_s/tput$o \
	../obj_s/tset$o \
	../obj_s/transform$o

$(SHARED_OBJS) : ../include/ncurses_cfg.h ./progs.priv.h

mostlyclean::
	-rm -f $(SHARED_OBJS)

clean ::
	-rm -f $(SHARED_OBJS)

# generated by mk-2nd.awk
#   model:      obj_s
#   MODEL:      SHARED
#   echo:       yes
#   subset:     ticlib+termlib+ext_tinfo+base+widechar+ext_funcs
#   crenames:   yes
#   cxxrenames: 
#   traces:     DEBUG
#   srcdir:     .

../obj_s/clear$o :	$(srcdir)/clear.c \
			$(HEADER_DEPS)
	$(LIBTOOL_COMPILE) $(CC) $(CFLAGS_SHARED) -c ../progs/clear.c -o ../obj_s/clear$o

../obj_s/tic$o :	$(srcdir)/tic.c \
			$(HEADER_DEPS) \
			transform.h \
			$(srcdir)/dump_entry.h \
			$(srcdir)/tparm_type.h
	$(LIBTOOL_COMPILE) $(CC) $(CFLAGS_SHARED) -c ../progs/tic.c -o ../obj_s/tic$o

../obj_s/toe$o :	$(srcdir)/toe.c \
			$(HEADER_DEPS) \
			$(INCDIR)/hashed_db.h
	$(LIBTOOL_COMPILE) $(CC) $(CFLAGS_SHARED) -c ../progs/toe.c -o ../obj_s/toe$o

../obj_s/dump_entry$o :	$(srcdir)/dump_entry.c \
			$(HEADER_DEPS) \
			$(srcdir)/dump_entry.h \
			../include/parametrized.h \
			$(INCDIR)/capdefaults.c \
			termsort.c
	$(LIBTOOL_COMPILE) $(CC) $(CFLAGS_SHARED) -c ../progs/dump_entry.c -o ../obj_s/dump_entry$o

../obj_s/infocmp$o :	$(srcdir)/infocmp.c \
			$(HEADER_DEPS) \
			$(srcdir)/dump_entry.h
	$(LIBTOOL_COMPILE) $(CC) $(CFLAGS_SHARED) -c ../progs/infocmp.c -o ../obj_s/infocmp$o

../obj_s/tabs$o :	$(srcdir)/tabs.c \
			$(HEADER_DEPS)
	$(LIBTOOL_COMPILE) $(CC) $(CFLAGS_SHARED) -c ../progs/tabs.c -o ../obj_s/tabs$o

../obj_s/tparm_type$o :	$(srcdir)/tparm_type.c \
			$(HEADER_DEPS) \
			$(srcdir)/tparm_type.h
	$(LIBTOOL_COMPILE) $(CC) $(CFLAGS_SHARED) -c ../progs/tparm_type.c -o ../obj_s/tparm_type$o

../obj_s/tput$o :	$(srcdir)/tput.c \
			$(HEADER_DEPS) \
			transform.h \
			$(srcdir)/dump_entry.h \
			$(srcdir)/tparm_type.h \
			termsort.c
	$(LIBTOOL_COMPILE) $(CC) $(CFLAGS_SHARED) -c ../progs/tput.c -o ../obj_s/tput$o

../obj_s/tset$o :	$(srcdir)/tset.c \
			$(HEADER_DEPS) \
			transform.h \
			$(srcdir)/dump_entry.h \
			../include/termcap.h
	$(LIBTOOL_COMPILE) $(CC) $(CFLAGS_SHARED) -c ../progs/tset.c -o ../obj_s/tset$o

../obj_s/transform$o :	$(srcdir)/transform.c \
			$(HEADER_DEPS) \
			transform.h
	$(LIBTOOL_COMPILE) $(CC) $(CFLAGS_SHARED) -c ../progs/transform.c -o ../obj_s/transform$o

depend : ${AUTO_SRC}
	makedepend -- ${CPPFLAGS} -- ${C_SRC}

# DO NOT DELETE THIS LINE -- make depend depends on it.
