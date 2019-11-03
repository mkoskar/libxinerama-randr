libxinerama-randr
=================

This is a fork of libXinerama from
https://gitlab.freedesktop.org/xorg/lib/libxinerama.git that uses RANDR
X extension when possible and hence works even in setups that don't have
XINERAMA X extension present (such as multiple X screens aka Zaphod mode).

You can setup ``Xorg(1)`` in multiple ways:

"Big Desktop" setup:

* single X screen: 0
* RANDR present
* XINERAMA present

"Zaphod" setup:

* multiple X screens: 0, 1, ...
* RANDR present
* XINERAMA **missing**

"Xinerama" setup:

* multiple "Screen" sections included in "ServerLayout" with "Xinerama" option
* single X screen: 0
* RANDR **missing**
* XINERAMA present

This libXinerama fork addresses problem that arises when using "Zaphod" setup
and allows applications that link to libXinerama dynamically to work using
information provided by RANDR 1.5 ``XRRGetMonitor`` API.


Notes (as of 25.10.2019)
------------------------

* Old ``PanoramiX`` API implementation wasn't modified.
* ``XineramaQueryVersion`` and ``XineramaIsActive`` return hardcoded values.
* ``XineramaQueryExtension`` returns ``0`` for both ``event_base_return`` and
  ``error_base_return``.
* It would be nice to use RANDR when available and then fallback to XINERAMA, or
  other way around (configurable?).
