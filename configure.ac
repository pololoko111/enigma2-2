AC_INIT([enigma2],[5.3],[http://www.openbh.net])
AM_INIT_AUTOMAKE([dist-bzip2 no-define tar-pax -Wno-portability])
AC_CONFIG_HEADERS([enigma2_config.h])

# Silent rules are available since 1.11, but older versions
# are still in use. So don't use them unconditionally.
m4_ifdef([AM_SILENT_RULES], [AM_SILENT_RULES([yes])])

AC_USE_SYSTEM_EXTENSIONS
AC_SYS_LARGEFILE

AC_PROG_CC
AC_PROG_CXX
m4_ifdef([LT_INIT], [LT_INIT], [AC_PROG_LIBTOOL])
AC_CONFIG_MACRO_DIR([m4])
AC_OPENMP()

AC_PATH_PROG(MSGFMT, msgfmt, AC_MSG_ERROR(Could not find msgfmt))
AC_PATH_PROG(MSGINIT, msginit, AC_MSG_ERROR(Could not find msginit))
AC_PATH_PROG(MSGMERGE, msgmerge, AC_MSG_ERROR(Could not find msgmerge))
AC_PATH_PROG(MSGUNIQ, msguniq, AC_MSG_ERROR(Could not find msguniq))
AC_PATH_PROG(XGETTEXT, xgettext, AC_MSG_ERROR(Could not find xgettext))

AM_PATH_PYTHON
AX_PYTHON_DEVEL
AX_PKG_SWIG
AX_SWIG_ENABLE_CXX
AX_SWIG_PYTHON
AX_PTHREAD

TUXBOX_APPS_DVB

AM_CONDITIONAL(HAVE_GIT_DIR, test -d "$srcdir/.git")
AM_CONDITIONAL(HAVE_FAKE_GIT_DIR, test -f "$srcdir/.git/last_commit_info")

dnl versions of gstreamer and plugins-base
AC_ARG_WITH(gstversion,
	AS_HELP_STRING([--with-gstversion],[use gstreamer version (major.minor)]),
	[GST_MAJORMINOR=$withval],[GST_MAJORMINOR=0.10])

PKG_CHECK_MODULES(GSTREAMER, gstreamer-$GST_MAJORMINOR gstreamer-pbutils-$GST_MAJORMINOR)
PKG_CHECK_MODULES(BASE, [freetype2 fribidi glib-2.0 gstreamer-$GST_MAJORMINOR gstreamer-pbutils-$GST_MAJORMINOR libdvbsi++ libpng libxml-2.0 sigc++-3.0 libssl libcrypto])
PKG_CHECK_MODULES(LIBDDVD, libdreamdvd, HAVE_LIBDDVD="yes", HAVE_LIBDDVD="no")
AM_CONDITIONAL(HAVE_LIBDDVD, test "$HAVE_LIBDDVD" = "yes")
PKG_CHECK_MODULES(AVAHI, avahi-client)

AC_CHECK_LIB([udfread], [udfread_init])
AC_CHECK_LIB([dl], [dlopen], [LIBDL_LIBS="-ldl"], [AC_MSG_ERROR([Could not find libdl])])
AC_SUBST(LIBDL_LIBS)
AC_CHECK_LIB([jpeg], [jpeg_set_defaults], [LIBJPEG_LIBS="-ljpeg"], [AC_MSG_ERROR([Could not find libjpeg])])
AC_SUBST(LIBJPEG_LIBS)
AC_CHECK_LIB([ungif], [DGifOpen], [LIBGIF_LIBS="-lungif"], [AC_CHECK_LIB([gif], [DGifOpen], [LIBGIF_LIBS="-lgif"], [AC_MSG_ERROR([Could not find libgif or libungif])])])
AC_SUBST(LIBGIF_LIBS)

AC_ARG_WITH(boxtype,
	[  --with-boxtype=NAME box type [[none,dm800...]]],
	[BOXTYPE="$withval"],[BOXTYPE="dm800"])
AC_SUBST(BOXTYPE)
AC_DEFINE_UNQUOTED(BOXTYPE,"$BOXTYPE",[box type])

AM_CONDITIONAL(AZBOX, test `echo "$BOXTYPE" | cut -b 1-5` == "azbox")
AM_CONDITIONAL(CUBE, test `echo "$BOXTYPE" | cut -b 1-4` == "cube")
AM_CONDITIONAL(DAGS, test `echo "$BOXTYPE" | cut -b 1-4` == "dags")
AM_CONDITIONAL(DREAMBOX, test `echo "$BOXTYPE" | cut -b 1-2` == "dm")
AM_CONDITIONAL(EBOX, test `echo "$BOXTYPE" | cut -b 1-4` == "ebox")
AM_CONDITIONAL(GIGABLUE, test `echo "$BOXTYPE" | cut -b 1-2` == "gb")
AM_CONDITIONAL(INI, test `echo "$BOXTYPE" | cut -b 1-3` == "ini")
AM_CONDITIONAL(IXUSS, test `echo "$BOXTYPE" | cut -b 1-4` == "ixus")
AM_CONDITIONAL(ODIN, test `echo "$BOXTYPE" | cut -b 1-4` == "odin")
AM_CONDITIONAL(SPARK, test `echo "$BOXTYPE" | cut -b 1-5` == "spark")
AM_CONDITIONAL(VUPLUS, test `echo "$BOXTYPE" | cut -b 1-2` == "vu")
AM_CONDITIONAL(WETEK, test `echo "$BOXTYPE" | cut -b 1-5` == "wetek")
AM_CONDITIONAL(XTREND, test `echo "$BOXTYPE" | cut -b 1-2` == "et")

AM_CONDITIONAL(AZBOXHD, test "$BOXTYPE" == "azboxhd")
AM_CONDITIONAL(AZBOXME, test "$BOXTYPE" == "azboxme")
AM_CONDITIONAL(AZBOXMINIME, test "$BOXTYPE" == "azboxminime")
AM_CONDITIONAL(BLACKBOX7405, test "$BOXTYPE" == "blackbox7405")
AM_CONDITIONAL(CUBE, test "$BOXTYPE" == "cube")
AM_CONDITIONAL(DAGS1, test "$BOXTYPE" == "dags1")
AM_CONDITIONAL(DAGS2, test "$BOXTYPE" == "dags2")
AM_CONDITIONAL(DAGS3, test "$BOXTYPE" == "dags3")
AM_CONDITIONAL(DAGS4, test "$BOXTYPE" == "dags4")
AM_CONDITIONAL(DAGS5, test "$BOXTYPE" == "dags5")
AM_CONDITIONAL(DAGS6, test "$BOXTYPE" == "dags6")
AM_CONDITIONAL(DM500HD, test "$BOXTYPE" == "dm500hd")
AM_CONDITIONAL(DM500HDV2, test "$BOXTYPE" == "dm500hdv2")
AM_CONDITIONAL(DM7020HD, test "$BOXTYPE" == "dm7020hd")
AM_CONDITIONAL(DM7020HDV2, test "$BOXTYPE" == "dm7020hdv2")
AM_CONDITIONAL(DM800, test "$BOXTYPE" == "dm800")
AM_CONDITIONAL(DM8000, test "$BOXTYPE" == "dm8000")
AM_CONDITIONAL(DM800SE, test "$BOXTYPE" == "dm800se")
AM_CONDITIONAL(DM800SEV2, test "$BOXTYPE" == "dm800sev2")
AM_CONDITIONAL(E3HD, test "$BOXTYPE" == "e3hd")
AM_CONDITIONAL(EBOX5000, test "$BOXTYPE" == "ebox5000")
AM_CONDITIONAL(EBOX5100, test "$BOXTYPE" == "ebox5100")
AM_CONDITIONAL(EBOX7358, test "$BOXTYPE" == "ebox7358")
AM_CONDITIONAL(EBOXLUMI, test "$BOXTYPE" == "eboxlumi")
AM_CONDITIONAL(ET10000, test "$BOXTYPE" == "et10000")
AM_CONDITIONAL(ET4X00, test "$BOXTYPE" == "et4x00")
AM_CONDITIONAL(ET5X00, test "$BOXTYPE" == "et5x00")
AM_CONDITIONAL(ET6X00, test "$BOXTYPE" == "et6x00")
AM_CONDITIONAL(ET8000, test "$BOXTYPE" == "et8000")
AM_CONDITIONAL(ET9X00, test "$BOXTYPE" == "et9x00")
AM_CONDITIONAL(EW7356, test `echo "$BOXTYPE"` == "ew7356")
AM_CONDITIONAL(EW7358, test `echo "$BOXTYPE"` == "ew7358")
AM_CONDITIONAL(EW7362, test `echo "$BOXTYPE"` == "ew7362")
AM_CONDITIONAL(FORMULER1, test "$BOXTYPE" == formuler1)
AM_CONDITIONAL(FORMULER3, test "$BOXTYPE" == formuler3)
AM_CONDITIONAL(GB800SE, test "$BOXTYPE" == "gb800se")
AM_CONDITIONAL(GB800SEPLUS, test "$BOXTYPE" == "gb800seplus")
AM_CONDITIONAL(GB800SOLO, test "$BOXTYPE" == "gb800solo")
AM_CONDITIONAL(GB800UE, test "$BOXTYPE" == "gb800ue")
AM_CONDITIONAL(GB800UEPLUS, test "$BOXTYPE" == "gb800ueplus")
AM_CONDITIONAL(GBIPBOX, test "$BOXTYPE" == "gbipbox")
AM_CONDITIONAL(GBQUAD, test "$BOXTYPE" == "gbquad")
AM_CONDITIONAL(GBQUADPLUS, test "$BOXTYPE" == "gbquadplus")
AM_CONDITIONAL(HD1100, test "$BOXTYPE" == "hd1100")
AM_CONDITIONAL(HD1200, test "$BOXTYPE" == "hd1200")
AM_CONDITIONAL(HD2400, test "$BOXTYPE" == "hd2400")
AM_CONDITIONAL(HD500C, test "$BOXTYPE" == "hd500c")
AM_CONDITIONAL(INIHDE, test "$BOXTYPE" == "inihde")
AM_CONDITIONAL(INIHDE2, test `echo "$BOXTYPE" | cut -b 1-7` == inihde2)
AM_CONDITIONAL(INIHDP, test "$BOXTYPE" == "inihdp")
AM_CONDITIONAL(INIHDX, test "$BOXTYPE" == "inihdx")
AM_CONDITIONAL(IXUSSONE, test "$BOXTYPE" == "ixussone")
AM_CONDITIONAL(IXUSSZERO, test "$BOXTYPE" == "ixusszero")
AM_CONDITIONAL(ODINM6, test "$BOXTYPE" == odinm6)
AM_CONDITIONAL(ODINM7, test "$BOXTYPE" == odinm7)
AM_CONDITIONAL(ODINM7C, test "$BOXTYPE" == odinm7c)
AM_CONDITIONAL(ODINM7S, test "$BOXTYPE" == odinm7s)
AM_CONDITIONAL(ODINM9, test "$BOXTYPE" == odinm9)
AM_CONDITIONAL(SH1, test `echo "$BOXTYPE"` == "sh1")
AM_CONDITIONAL(SH2, test `echo "$BOXTYPE"` == "sh2")
AM_CONDITIONAL(SPARK, test `echo "$BOXTYPE" | cut -b 1-5` == spark)
AM_CONDITIONAL(TM2TOE, test "$BOXTYPE" == tm2t)
AM_CONDITIONAL(TMNANO, test "$BOXTYPE" == tmnano)
AM_CONDITIONAL(TMNANO2T, test "$BOXTYPE" == tmnano2t)
AM_CONDITIONAL(TMNANOSE, test "$BOXTYPE" == tmnanose)
AM_CONDITIONAL(TMSINGLE, test "$BOXTYPE" == tmsingle)
AM_CONDITIONAL(TMTWINOE, test "$BOXTYPE" == tmtwin)
AM_CONDITIONAL(VG2000, test `echo "$BOXTYPE"` == "vg2000")
AM_CONDITIONAL(VG5000, test `echo "$BOXTYPE"` == "vg5000")
AM_CONDITIONAL(VP7358CI, test "$BOXTYPE" == "vp7358ci")
AM_CONDITIONAL(VUDUO, test "$BOXTYPE" == vuduo)
AM_CONDITIONAL(VUDUO2, test "$BOXTYPE" == vuduo2)
AM_CONDITIONAL(VUDUO4K, test "$BOXTYPE" == vuduo4k)
AM_CONDITIONAL(VUDUO4KSE, test "$BOXTYPE" == vuduo4kse)
AM_CONDITIONAL(VUSOLO, test "$BOXTYPE" == vusolo)
AM_CONDITIONAL(VUSOLO2, test "$BOXTYPE" == vusolo2)
AM_CONDITIONAL(VUSOLO4K, test "$BOXTYPE" == vusolo4k)
AM_CONDITIONAL(VUSOLOSE, test "$BOXTYPE" == vusolose)
AM_CONDITIONAL(VUULTIMO, test "$BOXTYPE" == vuultimo)
AM_CONDITIONAL(VUULTIMO4K, test "$BOXTYPE" == vuultimo4k)
AM_CONDITIONAL(VUUNO, test "$BOXTYPE" == vuuno)
AM_CONDITIONAL(VUUNO4K, test "$BOXTYPE" == vuuno4k)
AM_CONDITIONAL(VUUNO4KSE, test "$BOXTYPE" == vuuno4kse)
AM_CONDITIONAL(VUZERO, test "$BOXTYPE" == vuzero)
AM_CONDITIONAL(VUZERO4K, test "$BOXTYPE" == vuzero4k)
AM_CONDITIONAL(XC7358, test "$BOXTYPE" == xc7358)
AM_CONDITIONAL(XC7358CI, test "$BOXTYPE" == xc7358ci)
AM_CONDITIONAL(XC7362, test "$BOXTYPE" == xc7362)
AM_CONDITIONAL(XP1000, test "$BOXTYPE" == xp1000)

AC_ARG_WITH(accelerationthreshold,
	AS_HELP_STRING([--with-accelerationthreshold=n], [use acceleration threshold of n bytes]),
	[[with_accelerationthreshold=$withval]],
	[[with_accelerationthreshold=48000]]
)

AC_DEFINE_UNQUOTED(GFX_SURFACE_ACCELERATION_THRESHOLD, $with_accelerationthreshold,[Configure threshold for accelerated surfaces (in bytes)])

AC_ARG_WITH(fillaccelerationthreshold,
	AS_HELP_STRING([--with-fillaccelerationthreshold=n], [use fill acceleration threshold of n bytes]),
	[[with_fillaccelerationthreshold=$withval]],
	[[with_fillaccelerationthreshold=80000]]
)

AC_DEFINE_UNQUOTED(GFX_SURFACE_FILL_ACCELERATION_THRESHOLD, $with_fillaccelerationthreshold,[Configure threshold for accelerated fill operations (in bytes)])

AC_ARG_WITH(blitaccelerationthreshold,
	AS_HELP_STRING([--with-blitaccelerationthreshold=n], [use blit acceleration threshold of n bytes]),
	[[with_blitaccelerationthreshold=$withval]],
	[[with_blitaccelerationthreshold=0]]
)

AC_DEFINE_UNQUOTED(GFX_SURFACE_BLIT_ACCELERATION_THRESHOLD, $with_blitaccelerationthreshold,[Configure threshold for accelerated blit operations (in bytes)])

AC_ARG_WITH(alphablendingacceleration,
	AS_HELP_STRING([--with-alphablendingacceleration=never/always/auto], [alphablending acceleration strategy: never accelerate / always accelerate / automatically decide when to accelerate (default)]),
	[[with_alphablendingacceleration=$withval]],
	[[with_alphablendingacceleration=auto]]
)

if test x"$with_alphablendingacceleration" = xnever ; then
	AC_DEFINE_UNQUOTED(FORCE_NO_BLENDING_ACCELERATION, 1, [Do not attempt to accelerate alphablending blits])
elif test x"$with_alphablendingacceleration" = xalways ; then
	AC_DEFINE_UNQUOTED(FORCE_ALPHABLENDING_ACCELERATION, 1, [Accelerate alphablending blits])
fi

AC_ARG_WITH(accelerationaccumulation,
	AS_HELP_STRING([--with-accelerationaccumulation], [accumulate blit/fill acceleration operations]),
	[[with_accelerationaccumulation=$withval]],
	[[with_accelerationaccumulation=no]]
)

if test x"$with_accelerationaccumulation" = xyes ; then
	AC_DEFINE(SUPPORT_ACCUMULATED_ACCELERATION_OPERATIONS, 1,[Accumulate blit/fill acceleration operations])
fi

AC_ARG_WITH(libvugles2,
	AS_HELP_STRING([--with-libvugles2],[use libvugles2, yes or no]),
	[with_libvugles2=$withval],[with_libvugles2=no])
if test "$with_libvugles2" = "yes"; then
	PKG_CHECK_MODULES(LIBVUGLES2, [libvugles2])
	GLES_CFLAGS="-DUSE_LIBVUGLES2"
fi
AM_CONDITIONAL(HAVE_LIBVUGLES2, test "$with_libvugles2" = "yes")

AC_ARG_WITH(libhiaccel,
	AS_HELP_STRING([--with-libhiaccel],[use libhiaccel, yes or no]),
	[with_libhiaccel=$withval],[with_libhiaccel=no])
if test "$with_libhiaccel" = "yes"; then
	PKG_CHECK_MODULES(LIBHIACCEL, [libhiaccel])
	HIACCEL_CFLAGS="-DUSE_LIBHIACCEL"
fi

if test x"$with_libhiaccel" != xno ; then
	AC_DEFINE(HAVE_HISILICON_ACCEL, 1,[define add HISILICON ACCEL])
fi

AC_ARG_WITH(osdanimation,
	AS_HELP_STRING([--with-osdanimation], [use osd animation, yes or no]),
	[[withosdanimation=$withval]],
	[[withosdanimation=no]]
)
if test x"$withosdanimation" != xno ; then

	AC_DEFINE(HAVE_OSDANIMATION, 1,[Define if driver supports animation of osd])
fi
AM_CONDITIONAL(HAVE_OSDANIMATION, test x"$withosdanimation" != xno)


if test `echo "$BOXTYPE" | cut -b 1-2` == "dm"; then
	AC_DEFINE(DREAMBOX, 1, [Dreambox hardware])
	AC_DEFINE(KEY_PLAY_ACTUALLY_IS_KEY_PLAYPAUSE, 1,[define when rc sends a KEY_PLAY event for its KEY_PLAYPAUSE key])
fi

AC_ARG_WITH(nolcd,
	AS_HELP_STRING([--with-nolcd], [disable ascii based lcd, yes or no]),
	[[withnolcd=$withval]],
	[[withnolcd=no]]
)
if test x"$withnolcd" != xno ; then
	AC_DEFINE(NO_LCD, 1,[Define when disable an ascii based lcd device])
fi
AM_CONDITIONAL(NO_LCD, test x"$withnolcd" != xno)

AC_ARG_WITH(textlcd,
	AS_HELP_STRING([--with-textlcd], [use ascii based lcd, yes or no]),
	[[withtextlcd=$withval]],
	[[withtextlcd=no]]
)
if test x"$withtextlcd" != xno ; then
	AC_DEFINE(HAVE_TEXTLCD, 1,[Define when using an ascii based lcd device])
fi
AM_CONDITIONAL(HAVE_TEXTLCD, test x"$withtextlcd" != xno)

AC_ARG_WITH(7segment,
	AS_HELP_STRING([--with-7segment], [use ascii based lcd, yes or no]),
	[[with7segment=$withval]],
	[[with7segment=no]]
)
if test x"$with7segment" != xno ; then
	AC_DEFINE(HAVE_7SEGMENT, 1,[Define when using an ascii based lcd device])
fi
AM_CONDITIONAL(HAVE_7SEGMENT, test x"$with7segment" != xno)

AC_ARG_WITH(colorlcd,
	AS_HELP_STRING([--with-colorlcd], [use 96x64 16bpp color display, yes or no]),
	[[withcolorlcd=$withval]],
	[[withcolorlcd=no]]
)
if test x"$withcolorlcd" != xno ; then
	AC_DEFINE(HAVE_COLORLCD, 1,[Define when using a 96x64 color display device])
fi
AM_CONDITIONAL(HAVE_COLORLCD, test x"$withcolorlcd" != xno)

AC_ARG_WITH(colorlcd128,
	AS_HELP_STRING([--with-colorlcd128], [use 128x64 16bpp color display, yes or no]),
	[[withcolorlcd128=$withval]],
	[[withcolorlcd128=no]]
)
if test x"$withcolorlcd128" != xno ; then
	AC_DEFINE(HAVE_COLORLCD128, 1,[Define when using a 128x64 color display device])
fi
AM_CONDITIONAL(HAVE_COLORLCD128, test x"$withcolorlcd" != xno)

AC_ARG_WITH(colorlcd220,
	AS_HELP_STRING([--with-colorlcd220], [use 220x176 16bpp color display, yes or no]),
	[[withcolorlcd220=$withval]],
	[[withcolorlcd220=no]]
)
if test x"$withcolorlcd220" != xno ; then
	AC_DEFINE(HAVE_COLORLCD220, 1,[Define when using a 220x176 color display device])
fi
AM_CONDITIONAL(HAVE_COLORLCD220, test x"$withcolorlcd220" != xno)

AC_ARG_WITH(colorlcd400,
	AS_HELP_STRING([--with-colorlcd400], [use 400x176 16bpp color display, yes or no]),
	[[withcolorlcd400=$withval]],
	[[withcolorlcd400=no]]
)
if test x"$withcolorlcd400" != xno ; then
	AC_DEFINE(HAVE_COLORLCD400, 1,[Define when using a 400x176 color display device])
fi
AM_CONDITIONAL(HAVE_COLORLCD400, test x"$withcolorlcd400" != xno)

AC_ARG_WITH(colorlcd480,
	AS_HELP_STRING([--with-colorlcd480], [use 480x320 16bpp color display, yes or no]),
	[[withcolorlcd480=$withval]],
	[[withcolorlcd480=no]]
)
if test x"$withcolorlcd480" != xno ; then
	AC_DEFINE(HAVE_COLORLCD480, 1,[Define when using a 480x320 color display device])
fi
AM_CONDITIONAL(HAVE_COLORLCD480, test x"$withcolorlcd480" != xno)

AC_ARG_WITH(colorlcd720,
	AS_HELP_STRING([--with-colorlcd720], [use 720x576 16bpp color display, yes or no]),
	[[withcolorlcd720=$withval]],
	[[withcolorlcd720=no]]
)
if test x"$withcolorlcd720" != xno ; then
	AC_DEFINE(HAVE_COLORLCD720, 1,[Define when using a 720x576 color display device])
fi

AM_CONDITIONAL(HAVE_COLORLCD720, test x"$withcolorlcd720" != xno)

AC_ARG_WITH(colorlcd800,
	AS_HELP_STRING([--with-colorlcd800], [use 800x480 16bpp color display, yes or no]),
	[[withcolorlcd800=$withval]],
	[[withcolorlcd800=no]]
)
if test x"$withcolorlcd800" != xno ; then
	AC_DEFINE(HAVE_COLORLCD800, 1,[Define when using a 800x480 color display device])
fi

AM_CONDITIONAL(HAVE_COLORLCD800, test x"$withcolorlcd800" != xno)

AC_ARG_WITH(bwlcd255,
	AS_HELP_STRING([--with-bwlcd255], [use 255x64 1bpp black and white display, yes or no]),
	[[withbwlcd255=$withval]],
	[[withbwlcd255=no]]
)
if test x"$withbwlcd255" != xno ; then
	AC_DEFINE(HAVE_BWLCD255, 1,[Define when using a 255x64 black and white display device])
fi
AM_CONDITIONAL(HAVE_BWLCD255, test x"$withbwlcd255" != xno)

AC_ARG_WITH(bwlcd140,
	AS_HELP_STRING([--with-bwlcd140], [use 140x32 1bpp black and white display, yes or no]),
	[[withbwlcd140=$withval]],
	[[withbwlcd140=no]]
)
if test x"$withbwlcd140" != xno ; then
	AC_DEFINE(HAVE_BWLCD140, 1,[Define when using a 140x32 black and white display device])
fi
AM_CONDITIONAL(HAVE_BWLCD140, test x"$withbwlcd140" != xno)

AC_ARG_WITH(bwlcd128,
	AS_HELP_STRING([--with-bwlcd128], [use 128x32 1bpp black and white display, yes or no]),
	[[withbwlcd128=$withval]],
	[[withbwlcd128=no]]
)
if test x"$withbwlcd128" != xno ; then
	AC_DEFINE(HAVE_BWLCD128, 1,[Define when using a 128x32 black and white display device])
fi
AM_CONDITIONAL(HAVE_BWLCD128, test x"$withbwlcd128" != xno)

AC_ARG_WITH(oldpvr,
	AS_HELP_STRING([--with-oldpvr], [use /dev/misc/pvr instead of /dev/dvb/adapterX/dvrX, yes or no]),
	[[witholdpvr=$withval]],
	[[witholdpvr=no]]
)
if test x"$witholdpvr" != xno ; then
	AC_DEFINE(HAVE_OLDPVR, 1,[Define when using /dev/misc/pvr])
fi
AM_CONDITIONAL(HAVE_OLDPVR, test x"$witholdpvr" != xno)

if test `echo "$BOXTYPE" | cut -b 1-2` == "et" ; then
	AC_DEFINE(KEY_PLAY_ACTUALLY_IS_KEY_PLAYPAUSE, 1,[define when rc sends a KEY_PLAY event for its KEY_PLAYPAUSE key])
fi

if test `echo "$BOXTYPE" | cut -b 1-4` == "odin"; then
	AC_DEFINE(KEY_PLAY_ACTUALLY_IS_KEY_PLAYPAUSE, 1,[define when rc sends a KEY_PLAY event for its KEY_PLAYPAUSE key])
	AC_DEFINE(FORCE_NO_BLENDING_ACCELERATION, 1,[define when the framebuffer acceleration does not have alphablending support, though the autodetection might indicate that it does])
fi

if test `echo "$BOXTYPE" | cut -b 1-2` == "vu"; then
	AC_DEFINE(FORCE_NO_BLENDING_ACCELERATION, 1,[define when the framebuffer acceleration does not have alphablending support, though the autodetection might indicate that it does])
	AC_DEFINE(FORCE_ADVANCED_REMOTE, 1,[define to fixup the input device identification when the remote control is actually an 'advanced' remote (with play/forward/rewind keys)])
fi

if test `echo "$BOXTYPE" | cut -b 1-2` == "gb"; then
	AC_DEFINE(KEY_PLAY_ACTUALLY_IS_KEY_PLAYPAUSE, 1,[define when rc sends a KEY_PLAY event for its KEY_PLAYPAUSE key])
	AC_DEFINE(FORCE_NO_BLENDING_ACCELERATION, 1,[define when the framebuffer acceleration does not have alphablending support, though the autodetection might indicate that it does])
fi

if test `echo "$BOXTYPE" | cut -b 1-3` == "ini"; then
	AC_DEFINE(KEY_PLAY_ACTUALLY_IS_KEY_PLAYPAUSE, 1,[define when rc sends a KEY_PLAY event for its KEY_PLAYPAUSE key])
	AC_DEFINE(FORCE_NO_BLENDING_ACCELERATION, 1,[define when the framebuffer acceleration does not have alphablending support, though the autodetection might indicate that it does])
fi

if test `echo "$BOXTYPE" | cut -b 1-4` == "dags"; then
	AC_DEFINE(FORCE_NO_BLENDING_ACCELERATION, 1,[define when the framebuffer acceleration does not have alphablending support, though the autodetection might indicate that it does])
	AC_DEFINE(FORCE_ADVANCED_REMOTE, 1,[define to fixup the input device identification when the remote control is actually an 'advanced' remote (with play/forward/rewind keys)])
	AC_DEFINE(HAVE_CPULOADFIX, 1,[define to fixup the high load of cpu then playback ts and mediafiles])
fi

if test `echo "$BOXTYPE" | cut -b 1-4` == "ixus"; then
	AC_DEFINE(FORCE_NO_BLENDING_ACCELERATION, 1,[define when the framebuffer acceleration does not have alphablending support, though the autodetection might indicate that it does])
fi

if test "$BOXTYPE" == "blackbox7405"; then
	AC_DEFINE(FORCE_ADVANCED_REMOTE, 1,[define to fixup the input device identification when the remote control is actually an 'advanced' remote (with play/forward/rewind keys)])
	AC_DEFINE(KEY_PLAY_IS_KEY_PLAYPAUSE, 1,[define when rc sends a KEY_PLAY event for its KEY_PLAYPAUSE key])
fi

if test "$BOXTYPE" == "g300"; then
	AC_DEFINE(FORCE_BLENDING_ACCELERATION, 1,[define when the framebuffer acceleration has alphablending support, but detection slow down all])
	AC_DEFINE(FORCE_ADVANCED_REMOTE, 1,[define to fixup the input device identification when the remote control is actually an 'advanced' remote (with play/forward/rewind keys)])
fi

if test "$BOXTYPE" == "et8500"; then
	AC_DEFINE(FORCE_BLENDING_ACCELERATION, 1,[define when the framebuffer acceleration has alphablending support, but detection slow down all])
	AC_DEFINE(FORCE_ADVANCED_REMOTE, 1,[define to fixup the input device identification when the remote control is actually an 'advanced' remote (with play/forward/rewind keys)])
fi

if test "$BOXTYPE" == "sf4008"; then
	AC_DEFINE(FORCE_BLENDING_ACCELERATION, 1,[define when the framebuffer acceleration has alphablending support, but detection slow down all])
	AC_DEFINE(FORCE_ADVANCED_REMOTE, 1,[define to fixup the input device identification when the remote control is actually an 'advanced' remote (with play/forward/rewind keys)])
fi

if test "$BOXTYPE" == "et7x00"; then
	AC_DEFINE(KEY_F1_TO_KEY_F2, 1,[define when rc sends a KEY_F1 event for its KEY_F2 key])
	AC_DEFINE(FORCE_BLENDING_ACCELERATION, 1,[define when the framebuffer acceleration has alphablending support, but detection slow down all])
fi

if test "$BOXTYPE" == "sf8008" -o "$BOXTYPE" == "sx88v2" -o "$BOXTYPE" == "sx988" -o "$BOXTYPE" == "sfx6008" -o "$BOXTYPE" == "dagsmv200" -o "$BOXTYPE" == "gbmv200" -o "$BOXTYPE" == "ustym4kpro"; then
	AC_DEFINE(HAVE_HISILICON, 1,[define add HISILICON chip])
	AC_DEFINE(CONFIG_HISILICON_FB, 1,[define add HISILICON framebuffer blit])
	AC_DEFINE(FORCE_ALPHABLENDING_ACCELERATION, 1,[define when the framebuffer acceleration has alphablending support, but detection slow down all])
fi

if test "$BOXTYPE" == "u5" -o "$BOXTYPE" == "u5pvr" -o "$BOXTYPE" == "u51" -o "$BOXTYPE" == "u52" -o "$BOXTYPE" == "u53" -o "$BOXTYPE" == "u532" -o "$BOXTYPE" == "u533" -o "$BOXTYPE" == "u54" -o "$BOXTYPE" == "u55" -o "$BOXTYPE" == "u56" -o "$BOXTYPE" == "u57" -o "$BOXTYPE" == "u571" -o "$BOXTYPE" == "u41" -o "$BOXTYPE" == "u42" -o "$BOXTYPE" == "u43"; then
	AC_DEFINE(HAVE_HISILICON, 1,[define add HISILICON chip])
fi

if test "$BOXTYPE" == "u53"; then
	AC_DEFINE(KEY_F6_TO_KEY_FAVORITES, 1,[define when rc FAV key sends a KEY_F6 event for its KEY_FAVORITES key])
	AC_DEFINE(KEY_CONTEXT_MENU_TO_KEY_BACK, 1,[define when rc MOUSE key sends a KEY_CONTEXT_MENU event for its KEY_BACK key])
	AC_DEFINE(KEY_WWW_TO_KEY_FILE, 1,[define when rc HOME key sends a KEY_WWW event for its KEY_FILE key])
	AC_DEFINE(KEY_HELP_TO_KEY_AUDIO, 1,[define when rc SETTINGS key sends a KEY_HELP event for its KEY_AUDIO key])
fi

if test "$BOXTYPE" == "7000s"; then
	AC_DEFINE(FORCE_NO_BLENDING_ACCELERATION, 1,[define when the framebuffer acceleration has alphablending support, but detection slow down all])
	AC_DEFINE(KEY_PLAY_ACTUALLY_IS_KEY_PLAYPAUSE, 1,[define when rc sends a KEY_PLAY event for its KEY_PLAYPAUSE key])
fi

if test "$BOXTYPE" == "7005s"; then
	AC_DEFINE(FORCE_NO_BLENDING_ACCELERATION, 1,[define when the framebuffer acceleration has alphablending support, but detection slow down all])
	AC_DEFINE(KEY_PLAY_ACTUALLY_IS_KEY_PLAYPAUSE, 1,[define when rc sends a KEY_PLAY event for its KEY_PLAYPAUSE key])
fi

if test "$BOXTYPE" == "7210s"; then
	AC_DEFINE(FORCE_NO_BLENDING_ACCELERATION, 1,[define when the framebuffer acceleration has alphablending support, but detection slow down all])
fi

if test "$BOXTYPE" == "formuler4turbo"; then
	AC_DEFINE(FORCE_ADVANCED_REMOTE, 1,[define to fixup the input device identification when the remote control is actually an 'advanced' remote (with play/forward/rewind keys)])
	AC_DEFINE(KEY_PLAY_ACTUALLY_IS_KEY_PLAYPAUSE, 1,[define when rc sends a KEY_PLAY event for its KEY_PLAYPAUSE key])
fi

if test "$BOXTYPE" == "formuler1"; then
	AC_DEFINE(KEY_BOOKMARKS_TO_KEY_MEDIA, 1,[define when rc Playlist sends a KEY_BOOKMARKS event for its KEY_MEDIA key])
	AC_DEFINE(KEY_VIDEO_TO_KEY_FAVORITES, 1,[define when rc FAV key sends a KEY_VIDEO event for its KEY_FAVORITES key])
fi

AC_ARG_WITH(libsdl,
	AS_HELP_STRING([--with-libsdl],[use libsdl, yes or no]),
	[with_libsdl=$withval],[with_libsdl=no])
if test "$with_libsdl" = "yes"; then
	PKG_CHECK_MODULES(LIBSDL, sdl)
fi
AM_CONDITIONAL(HAVE_LIBSDL, test "$with_libsdl" = "yes")

AC_ARG_WITH(libxine,
	AS_HELP_STRING([--with-libxine],[use libxine, yes or no]),
	[with_libxine=$withval],[with_libxine=no])
if test "$with_libxine" = "yes"; then
	PKG_CHECK_MODULES(LIBXINE, libxine)
	AC_DEFINE([WITH_XINE],[1],[Define to 1 if you have libxine])
fi
AM_CONDITIONAL(HAVE_LIBXINE, test "$with_libxine" = "yes")

AC_ARG_WITH(debug,
	AS_HELP_STRING([--without-debug],[disable debugging code]),
	[with_debug="$withval"],[with_debug="yes"])
if test "$with_debug" = "yes"; then
	AC_DEFINE([DEBUG],[1],[Define to 1 to enable debugging code])
fi

AC_ARG_WITH(memcheck,
	AS_HELP_STRING([--with-memcheck],[enable memory leak checks]),
	[with_memcheck="$withval"],[with_memcheck="no"])
if test "$with_memcheck" = "yes"; then
	AC_DEFINE([MEMLEAK_CHECK],[1],[Define to 1 to enable memory leak checks])
fi

AC_ARG_WITH(fbdev,
	AS_HELP_STRING([--with-fbdev=devicename], [use devicename for framebuffer device, e.g. /dev/fb0 ]),
	[[with_fbdev=$withval]],
	[[with_fbdev=no]]
)
if test x"$with_fbdev" != xno ; then
	AC_DEFINE_UNQUOTED(FB_DEV, "$withval", [Defines which device to use for main framebuffer (e.g. /dev/fb0)])
fi

AC_ARG_WITH(lcddev,
	AS_HELP_STRING([--with-lcddev=devicename], [use devicename for lcd framebuffer device, e.g. /dev/fb1 ]),
	[[with_lcddev=$withval]],
	[[with_lcddev=no]]
)
if test x"$with_lcddev" != xno ; then
	AC_DEFINE_UNQUOTED(LCD_DEV, "$withval", [Defines which device to use for lcd (e.g. /dev/fb1)])
fi

AC_ARG_WITH(fcc,
	AS_HELP_STRING([--with-fcc], [add FCC system plugin]),
	[[with_fcc=$withval]],
	[[with_fcc=no]]
)

AM_CONDITIONAL(HAVE_FCC, test x"$with_fcc" = xyes)
if test x"$with_fcc" = xyes ; then
	AC_DEFINE(HAVE_FCC, 1,[add FCC system plugin])
fi

AC_CHECK_HEADERS([sys/klog.h])
AC_CHECK_FUNCS([klogctl])

ENIGMA2_CFLAGS="-fno-rtti -fno-exceptions -rdynamic -funwind-tables"
AC_SUBST(ENIGMA2_CFLAGS)

AX_CXX_COMPILE_STDCXX_17([ext],[mandatory])

AX_CHECK_COMPILE_FLAG([-Wattribute-alias], [CXXFLAGS="$CXXFLAGS -Wattribute-alias"])
AX_CHECK_COMPILE_FLAG([-Wattribute-alias=1], [CXXFLAGS="$CXXFLAGS -Wattribute-alias=1"])

CPPFLAGS="$CPPFLAGS $PYTHON_CPPFLAGS"
CFLAGS="$CFLAGS -Wall"
CXXFLAGS="$CXXFLAGS -Wall -Wextra\
	-Wformat=2 -Wformat-overflow=2 -Wformat-nonliteral -Wformat-security \
	-Wimplicit-fallthrough=5 -Wduplicated-branches -Wtrampolines \
	-Wdangling-else -Wshift-overflow=2 -Wswitch \
	-Wunused-but-set-parameter -Wunused-const-variable=1 -Wuninitialized \
	-Wstringop-overflow=3 -Woverlength-strings \
	-Wunsafe-loop-optimizations -Wpointer-arith \
	-Wfloat-equal -Wlogical-op \
	-Wno-error=cast-align=strict -Wno-error=ignored-qualifiers \
	-Wno-error=cast-function-type \
	-Wno-error=stringop-truncation -Wno-error=shadow -Wno-error=cast-qual \
	-Wno-error=aggregate-return -Wno-error=missing-field-initializers \
	-Wno-error=packed -Wno-error=vla -Wno-error=clobbered -Wno-error=unused-parameter \
	$BASE_CFLAGS $ENIGMA2_CFLAGS $PTHREAD_CFLAGS $OPENMP_CFLAGS $ALSA_CFLAGS $GLES_CFLAGS"
AX_SWIG_PYTHON_OPT="$AX_SWIG_PYTHON_OPT -DSWIG_PYTHON_LEGACY_BOOL"

AC_CONFIG_FILES([
Makefile
data/Makefile
data/fonts/Makefile
data/keymaps/Makefile
data/displaytext/Makefile
data/7segment/Makefile
data/display96/Makefile
data/display128/Makefile
data/display220/Makefile
data/display400/Makefile
data/display480/Makefile
data/display480/OpenBh-LCDskin/Makefile
data/display720/Makefile
data/display720/Default_with_Analogue_Clock_Standby/Makefile
data/display720/Default_with_Picon_and_Analogue_Clock_Standby/Makefile
data/display720/Default_with_Picon_Fullscreen/Makefile
data/display720/Default_with_Picon_Fullscreen_and_Analogue_Clock_Standby/Makefile
data/display800/Makefile
data/display800/Default_with_Picon_Fullscreen/Makefile
data/vfd128/Makefile
data/vfd140/Makefile
data/vfd255/Makefile
etc/Makefile
etc/cron/Makefile
etc/cron/crontabs/Makefile
include/Makefile
lib/Makefile
lib/base/eenv.cpp
lib/python/Makefile
lib/python/Components/Makefile
lib/python/Components/Addons/Makefile
lib/python/Components/Converter/Makefile
lib/python/Components/Renderer/Makefile
lib/python/Components/Sources/Makefile
lib/python/Screens/Makefile
lib/python/Plugins/Makefile
lib/python/Plugins/Extensions/Makefile
lib/python/Plugins/Extensions/CutListEditor/Makefile
lib/python/Plugins/Extensions/CutListEditor/meta/Makefile
lib/python/Plugins/Extensions/DVDBurn/Makefile
lib/python/Plugins/Extensions/DVDBurn/meta/Makefile
lib/python/Plugins/Extensions/DVDPlayer/Makefile
lib/python/Plugins/Extensions/DVDPlayer/meta/Makefile
lib/python/Plugins/Extensions/MediaPlayer/Makefile
lib/python/Plugins/Extensions/MediaPlayer/meta/Makefile
lib/python/Plugins/Extensions/MediaScanner/Makefile
lib/python/Plugins/Extensions/MediaScanner/meta/Makefile
lib/python/Plugins/Extensions/PicturePlayer/Makefile
lib/python/Plugins/Extensions/PicturePlayer/meta/Makefile
lib/python/Plugins/Extensions/SocketMMI/Makefile
lib/python/Plugins/Extensions/SocketMMI/meta/Makefile
lib/python/Plugins/Extensions/SocketMMI/src/Makefile
lib/python/Plugins/Extensions/TuxboxPlugins/Makefile
lib/python/Plugins/Extensions/TuxboxPlugins/meta/Makefile
lib/python/Plugins/SystemPlugins/Makefile
lib/python/Plugins/SystemPlugins/AnimationSetup/Makefile
lib/python/Plugins/SystemPlugins/CableScan/Makefile
lib/python/Plugins/SystemPlugins/CommonInterfaceAssignment/Makefile
lib/python/Plugins/SystemPlugins/CommonInterfaceAssignment/meta/Makefile
lib/python/Plugins/SystemPlugins/DefaultServicesScanner/Makefile
lib/python/Plugins/SystemPlugins/DefaultServicesScanner/meta/Makefile
lib/python/Plugins/SystemPlugins/DiseqcTester/Makefile
lib/python/Plugins/SystemPlugins/DiseqcTester/meta/Makefile
lib/python/Plugins/SystemPlugins/FastChannelChange/Makefile
lib/python/Plugins/SystemPlugins/FastChannelChange/meta/Makefile
lib/python/Plugins/SystemPlugins/FastScan/Makefile
lib/python/Plugins/SystemPlugins/FrontprocessorUpgrade/Makefile
lib/python/Plugins/SystemPlugins/FrontprocessorUpgrade/meta/Makefile
lib/python/Plugins/SystemPlugins/Hotplug/Makefile
lib/python/Plugins/SystemPlugins/Hotplug/meta/Makefile
lib/python/Plugins/SystemPlugins/NetworkWizard/Makefile
lib/python/Plugins/SystemPlugins/NetworkWizard/meta/Makefile
lib/python/Plugins/SystemPlugins/OpentvZapper/Makefile
lib/python/Plugins/SystemPlugins/PositionerSetup/Makefile
lib/python/Plugins/SystemPlugins/PositionerSetup/meta/Makefile
lib/python/Plugins/SystemPlugins/SABnzbdSetup/Makefile
lib/python/Plugins/SystemPlugins/SatelliteEquipmentControl/Makefile
lib/python/Plugins/SystemPlugins/SatelliteEquipmentControl/meta/Makefile
lib/python/Plugins/SystemPlugins/Satfinder/Makefile
lib/python/Plugins/SystemPlugins/Satfinder/meta/Makefile
lib/python/Plugins/SystemPlugins/VideoClippingSetup/Makefile
lib/python/Plugins/SystemPlugins/VideoEnhancement/Makefile
lib/python/Plugins/SystemPlugins/VideoEnhancement/meta/Makefile
lib/python/Plugins/SystemPlugins/VideoTune/Makefile
lib/python/Plugins/SystemPlugins/VideoTune/meta/Makefile
lib/python/Plugins/SystemPlugins/OBH/Makefile
lib/python/Plugins/SystemPlugins/OBH/images/Makefile
lib/python/Plugins/SystemPlugins/WirelessLan/Makefile
lib/python/Plugins/SystemPlugins/WirelessLan/meta/Makefile
lib/python/Tools/Makefile
po/Makefile
main/Makefile
tools/Makefile
tools/enigma2.sh
enigma2.pc
])
AC_OUTPUT
