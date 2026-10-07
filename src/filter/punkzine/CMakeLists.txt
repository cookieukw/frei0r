# Punk Zine: ransom-note text, scissor cut-outs, xerox and riso halftone.
# Plain C; pthreads for row bands where available, a serial path otherwise
# (see PZ_THREADS in punkzine.c).
set(PUNKZINE_LIBS)
if(NOT WIN32)
  set(THREADS_PREFER_PTHREAD_FLAG ON)
  find_package(Threads REQUIRED)
  list(APPEND PUNKZINE_LIBS Threads::Threads)
endif()
if(UNIX)
  list(APPEND PUNKZINE_LIBS m)
endif()

frei0r_add_plugin(
  NAME punkzine KIND FILTER SOURCES punkzine.c
  BUNDLE_ID punkzine UPDATE TRUE UPDATE2 FALSE BUNDLE_ELIGIBLE
  LINK_LIBRARIES ${PUNKZINE_LIBS}
  MSVC_DEFINITION ${FREI0R_DEF}
)
