project('com.github.spheras.desktopfolder', ['vala', 'c'],
    version: '1.0.6'
)

gnome = import('gnome')
i18n = import('i18n')

asresources = gnome.compile_resources(
    'as-resources', 'data/css.gresource.xml',
    source_dir: 'data',
    c_name: 'as'
)

add_project_arguments(['--vapidir', join_paths(meson.current_source_dir(), 'vapi')], language: 'vala')

conf = configuration_data()
conf.set_quoted('GETTEXT_PACKAGE', meson.project_name())
configure_file(output: 'config.h', configuration: conf)
config_h_dir = include_directories('.')

c_args = [
  '-include', 'config.h',
  '-DWNCK_I_KNOW_THIS_IS_UNSTABLE'
]

#We need to add the math library if required
cc = meson.get_compiler('c')
m_dep = cc.find_library('m', required : false)

#Source files
src = [
       'src/LanguageText.vala',
       'src/Resources.vala',
       'src/Application.vala',
       'src/utils/Util.vala',
       'src/utils/shortcut/Shortcut.vala',
       'src/utils/shortcut/CustomShortcutSettings.vala',
       'src/utils/menu/MenuItemColor.vala',
       'src/utils/menu/MenuItemSeparator.vala',
       'src/utils/clipboard/ClipboardFile.vala',
       'src/utils/clipboard/ClipboardManager.vala',
       'src/utils/dragndrop/DragNDrop.vala',
       'src/utils/dragndrop/DndHandler.vala',
       'src/utils/dragndrop/DndView.vala',
       'src/utils/dragndrop/DndBehaviour.vala',
       'src/utils/RenameDialog.vala',
       'src/utils/EditableLabel.vala',
       'src/widgets/DesktopWindow.vala',
       'src/widgets/FolderWindow.vala',
       'src/widgets/ItemView.vala',
       'src/settings/PositionSettings.vala',
       'src/settings/FolderSettings.vala',
       'src/settings/ItemSettings.vala',
       'src/settings/NoteSettings.vala',
       'src/settings/PhotoSettings.vala',
       'src/logic/DesktopManager.vala',
       'src/logic/FolderManager.vala',
       'src/logic/ItemManager.vala',
       'src/Dialogs/ProgressDialog.vala',
       'src/Dialogs/PanelPropertiesWindow.vala'
      ]

executable(
    'com.github.spheras.desktopfolder',
    src,
    asresources,
    c_args: c_args,
    dependencies: [
        dependency('gio-unix-2.0'),
        dependency('gee-0.8'),
        dependency('glib-2.0'),
        dependency('gobject-2.0'),
        dependency('gtk+-3.0'),
        dependency('cairo'),
        dependency('json-glib-1.0'),
        dependency('gdk-pixbuf-2.0'),
        dependency('libwnck-3.0'),
        dependency('gtksourceview-3.0'),
        m_dep
    ],
    install : true
)

meson.add_install_script('meson/post_install.py')

subdir('data')
subdir('po')
