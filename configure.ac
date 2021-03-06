#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ([2.69])
AC_INIT([mtcp], [3], [mtcp@list.ndsl.kaist.edu])
AC_CONFIG_SRCDIR([mtcp/src/eventpoll.c])
AC_CONFIG_HEADERS([config.h])

# Checks for programs.
AC_PROG_CC
AC_LANG(C)
AC_DISABLE_OPTION_CHECKING

# Checks for header files.
AC_CHECK_HEADERS([linux/sched.h pthread.h numa.h arpa/inet.h fcntl.h limits.h netdb.h netinet/in.h stdint.h stdlib.h string.h sys/ioctl.h sys/socket.h sys/time.h unistd.h])

# Check for AC_PTHREAD [FC is preventing this to be enabled..]
#AX_PTHREAD( [
#            AC_DEFINE(HAVE_PTHREAD,1,[Define if you have POSIX threads libraries and header files.])
#            CLIBS="$PTHREAD_LIBS $LIBS"
#            CFLAGS="$CFLAGS $PTHREAD_CFLAGS"
#            LDFLAGS="$LDFLAGS $PTHREAD_CFLAGS"
#            CC="$PTHREAD_CC"],[])

# Checks for typedefs, structures, and compiler characteristics.
AC_C_INLINE
AC_TYPE_INT16_T
AC_TYPE_INT32_T
AC_TYPE_INT64_T
AC_TYPE_INT8_T
AC_TYPE_PID_T
AC_TYPE_SIZE_T
AC_TYPE_SSIZE_T
AC_TYPE_UINT16_T
AC_TYPE_UINT32_T
AC_TYPE_UINT64_T
AC_TYPE_UINT8_T

# Checks for library functions.
AC_FUNC_MALLOC
AC_FUNC_MMAP
AC_CHECK_FUNCS([bzero clock_gettime getpagesize gettimeofday memmove memset munmap select socket strchr strerror strstr strtol])

# Reset DPDK to 0
AC_SUBST(DPDK, 0)
# Reset PSIO to 0
AC_SUBST(PSIO, 0)
# Reset NETMAP to 0
AC_SUBST(NETMAP, 0)

# Check dpdk-1.8.0 path (lib & inc)
AC_ARG_WITH(stuff, [  --with-dpdk-lib      path to the dpdk-2.2.0 install root])
if test "$with_dpdk_lib" != ""
then
        AC_SUBST(DPDKLIBPATH, $with_dpdk_lib)
	AC_SUBST(DPDK, 1)
fi

# Check psio path (lib & inc)
AC_ARG_WITH(stuff, [  --with-psio-lib      path to the ioengine install root])
if test "$with_psio_lib" != ""
then
        AC_SUBST(PSLIBPATH, $with_psio_lib)
	AC_SUBST(PSIO, 1)
fi

dnl Example of default-disabled feature
AC_ARG_ENABLE([netmap],
	AS_HELP_STRING([--enable-netmap], [Enable netmap module (EXPERIMENTAL)]))

AS_IF([test "x$enable_netmap" = "xyes"], [
	    AC_SUBST(NETMAP, 1)
])

if test "$with_psio_lib" == "" && test "$with_dpdk_lib" == "" && test "x$enable_netmap" = "xno"
then
	AC_MSG_ERROR([Packet I/O library is missing. Please set either dpdk or psio or netmap as your I/O lib.])
fi

AM_INIT_AUTOMAKE(mtcp, 3)
AC_CONFIG_FILES([Makefile])
AC_OUTPUT(mtcp/src/Makefile)
AC_OUTPUT(apps/example/Makefile)
AC_OUTPUT(util/Makefile)
AC_OUTPUT(io_engine/lib/Makefile)
