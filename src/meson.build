bin_conf = configuration_data()
bin_conf.set('GJS', find_program('gjs').full_path())
bin_conf.set('version', meson.project_version())
bin_conf.set('app_id', app_id)
bin_conf.set('prefix', prefix)
bin_conf.set('libdir', join_paths(get_option('prefix'), get_option('libdir')))
bin_conf.set('datadir', datadir)
bin_conf.set('pkgdatadir', pkgdatadir)

configure_file(
  input: 'bin.js',
  output: 're.sonny.Junction',
  configuration: bin_conf,
  install: true,
  install_dir: get_option('bindir')
)

blueprint_compiler = find_program(
  '/app/bin/blueprint-compiler',
  '../blueprint-compiler/blueprint-compiler.py',
  'blueprint-compiler'
)
gjspack = find_program('../troll/gjspack/bin/gjspack')
custom_target('gjspack',
  input: ['main.js'],
  output: app_id + '.src.gresource',
  command: [
    gjspack,
    '--appid=' + app_id,
    '--prefix', '/re/sonny/Junction',
    '--project-root', meson.source_root(),
    '--resource-root', meson.project_source_root() / 'src',
    '--blueprint-compiler', blueprint_compiler,
    '--no-executable',
    '@INPUT0@',
    '@OUTDIR@',
  ],
  install: true,
  install_dir: pkgdatadir,
  build_always_stale: true,
)
