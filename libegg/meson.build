tree_dnd_sources = [
  'eggtreemultidnd.c',
  'eggtreemultidnd.h',
  ]

smclient_sources = [
  'eggdesktopfile.c',
  'eggdesktopfile.h',
  'eggsmclient.c',
  'eggsmclient.h',
  'eggsmclient-private.h',
  'eggsmclient-xsmp.c',
]

cargs = [
  '-DEGG_SM_CLIENT_BACKEND_XSMP',
  '-DG_LOG_DOMAIN="EggSMClient"',
]

egg = static_library('libegg',
  tree_dnd_sources,
  smclient_sources,
  c_args : cargs,
  dependencies : libegg_deps,
)
