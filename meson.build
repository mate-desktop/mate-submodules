project(
  'mate-submodules', 'c',
  version: '1.24.0',
  meson_version: '>=0.47.0',
  license: 'GPL2',
  default_options : [ 'warning_level=1', 'buildtype=debugoptimized', 'c_std=gnu11'],
)

package_name = meson.project_name()
package_version = meson.project_version()
package_string = '@0@ @1@'.format(package_name, package_version)

config_h = configuration_data()
config_h.set_quoted('PACKAGE', package_name, description: 'Name of package')
config_h.set_quoted('PACKAGE_NAME', package_name, description: 'Define to the full name of this package.')
config_h.set_quoted('PACKAGE_STRING', package_string, description: 'Define to the full name and version of this package.')
config_h.set_quoted('PACKAGE_VERSION', package_version, description: 'Define to the version of this package.')
config_h.set_quoted('PACKAGE_URL', 'https://mate-desktop.org', description: 'Define to the home page for this package.')
config_h.set_quoted('GETTEXT_PACKAGE', package_name, description: 'Gettext package')
config_h.set_quoted('VERSION', package_version, description: 'Name of package')

# Compiler & Project arguments
add_project_arguments([
  '-DHAVE_CONFIG_H',
  '-I' + meson.build_root(),
  ], language: 'c')

# get suported warning flags
test_args = [
  '-fstack-protector-strong',
  '-Waggregate-return',
  '-Warray-bounds',
  '-Wcast-align',
  '-Wchar-subscripts',
  '-Wclobbered',
  '-Wdeclaration-after-statement',
  '-Wempty-body',
  '-Wextra',
  '-Wformat=2',
  '-Wformat-nonliteral',
  '-Wformat-security',
  '-Werror=format-security',
  '-Werror=format=2',
  '-Wformat-signedness',
  '-Wignored-qualifiers',
  '-Wimplicit-function-declaration',
  '-Winit-self',
  '-Winline',
  '-Wmissing-declarations',
  '-Wmissing-format-attribute',
  '-Wmissing-include-dirs',
  '-Wmissing-noreturn',
  '-Wmissing-parameter-type',
  '-Wmissing-prototypes',
  '-Wnested-externs',
  '-Wno-discarded-qualifiers',
  '-Wno-missing-field-initializers',
  '-Wno-strict-aliasing',
  '-Wno-suggest-attribute=format',
  '-Wno-unused-parameter',
  '-Wold-style-definition',
  '-Woverride-init',
  '-Wpacked',
  '-Wpointer-arith',
  '-Wredundant-decls',
  '-Wreturn-type',
  '-Wshadow',
  '-Wsign-compare',
  '-Wstrict-aliasing',
  '-Wstrict-prototypes',
  '-Wswitch-default',
  '-Wtype-limits',
  '-Wundef',
  '-Wuninitialized',
  '-Wunused-but-set-variable',
  '-Wwrite-strings',
  '-Wall',
  '-ansi',
  ]

cc = meson.get_compiler('c')

foreach arg: test_args
  if cc.has_multi_arguments(arg)
    add_project_arguments(arg, language : 'c')
  endif
endforeach

# byte order
if build_machine.endian() == 'big'
  config_h.set('WORDS_BIGENDIAN', 1)
endif

# Paths
rootdir = include_directories('.')

srcdir = meson.current_source_dir()
builddir = meson.current_build_dir()

prefix = get_option('prefix')
buildtype = get_option('buildtype')

bindir = join_paths(prefix, get_option('bindir'))
libdir = join_paths(prefix, get_option('libdir'))
datadir = join_paths(prefix, get_option('datadir'))
pkgdatadir = join_paths(datadir, package_name)

# Dependencies
glib_req = '>= 2.50.0'
gtk_req = '>= 3.22.0'
ice_req = '>= 1.0.0'
sm_req = '>= 1.0.0'

glib_dep = dependency('glib-2.0', version: glib_req)
gtk_dep = dependency('gtk+-3.0', version: gtk_req)
ice_dep = dependency('ice', version: ice_req)
sm_dep = dependency('sm', version: sm_req)

libegg_deps = [
  glib_dep,
  gtk_dep,
  ice_dep,
  sm_dep,
]

configure_file(
  output: 'config.h',
  configuration: config_h
)

subdir('libegg')

summary = [
  '',
  'mate-submodules-@0@:'.format(meson.project_version()),
  '',
  '	prefix:                   @0@'.format(prefix),
  '	source code location:     @0@'.format(srcdir),
  '	compiler:                 @0@'.format(cc.get_id()),
  '',
]

message('\n'.join(summary))

include_dirs = include_directories('.', 'libegg')
mate_submodules_dep = declare_dependency(include_directories: include_dirs, link_with: egg)
