desktop_conf = configuration_data()
desktop_conf.set('app_id', app_id)


desktop_file = i18n.merge_file(
  'desktop',
  input: configure_file(
           input: '@0@.desktop.in'.format(app_id),
           output: '@0@.desktop.in'.format(app_id),
           configuration: desktop_conf
         ),
  output: '@0@.desktop'.format(app_id),
  install: true,
  install_dir: desktopdir,
  po_dir: po_dir,
  type: 'desktop'
)

desktop_utils = find_program('desktop-file-validate', required: false)
if desktop_utils.found()
  test('Validate desktop file', desktop_utils,
    args: [desktop_file]
  )
endif

appstream_file = i18n.merge_file(
  input: 'com.gitlab.nvlgit.Balss.appdata.xml.in',
  output: 'com.gitlab.nvlgit.Balss.appdata.xml',
  po_dir: '../po',
  install: true,
  install_dir: join_paths(get_option('datadir'), 'appdata')
)

appstream_util = find_program('appstream-util', required: false)
if appstream_util.found()
  test('Validate appstream file', appstream_util,
    args: ['validate', appstream_file]
  )
endif

install_data('com.gitlab.nvlgit.Balss.gschema.xml',
  install_dir: join_paths(get_option('datadir'), 'glib-2.0/schemas')
)

compile_schemas = find_program('glib-compile-schemas', required: false)
if compile_schemas.found()
  test('Validate schema file', compile_schemas,
    args: ['--strict', '--dry-run', meson.current_source_dir()]
  )
endif

subdir('icons')