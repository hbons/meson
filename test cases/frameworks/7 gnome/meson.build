project('gobject-introspection', 'c')

cc = meson.get_compiler('c')

add_global_arguments('-DMESON_TEST', language : 'c')
if cc.get_id() == 'intel'
  # Ignore invalid GCC pragma warnings from glib
  # https://bugzilla.gnome.org/show_bug.cgi?id=776562
  add_global_arguments('-wd2282', language : 'c')
endif

py3 = import('python3').find_python()
pycode = '''import os, sys
if "MESON_UNIT_TEST_PRETEND_GLIB_OLD" in os.environ:
  sys.exit(0)
sys.exit(1)
'''

pretend_glib_old = false
res = run_command(py3, '-c', pycode)
if res.returncode() == 0
  pretend_glib_old = true
endif

gnome = import('gnome')
gio = dependency('gio-2.0')
giounix = dependency('gio-unix-2.0')
glib = dependency('glib-2.0')
gobj = dependency('gobject-2.0')
gir = dependency('gobject-introspection-1.0')
gmod = dependency('gmodule-2.0')

# Test that static deps don't error out when static libraries aren't found
glib_static = dependency('glib-2.0', static : true)

subdir('resources-data')
subdir('resources')
subdir('gir')
subdir('schemas')
subdir('gdbus')
subdir('mkenums')
subdir('genmarshal')
