rz_main_sources = [
  'main.c',
  'rz-agent.c',
  'rz-bin.c',
  'rizin.c',
  'rz-diff.c',
  'rz-find.c',
  'rz-gg.c',
  'rz-hash.c',
  'rz-run.c',
  'rz-sign.c',
  'rz-asm.c',
  'rz-ax.c'
]

rz_main_deps = [
  rz_util_dep,
  rz_demangler_dep,
  rz_magic_dep,
  rz_socket_dep,
  rz_flag_dep,
  rz_cons_dep,
  rz_hash_dep,
  rz_crypto_dep,
  rz_il_dep,
  rz_io_dep,
  rz_reg_dep,
  rz_bp_dep,
  rz_syscall_dep,
  rz_parse_dep,
  rz_asm_dep,
  rz_egg_dep,
  rz_search_dep,
  rz_analysis_dep,
  rz_debug_dep,
  rz_config_dep,
  rz_bin_dep,
  rz_sign_dep,
  rz_core_dep,
  rz_diff_dep,
]

rz_main = library('rz_main', rz_main_sources,
  include_directories: [platform_inc],
  c_args: library_cflags,
  dependencies: rz_main_deps,
  install: true,
  implicit_include_directories: false,
  install_rpath: rpath_lib,
  link_args: library_linkflags,
  soversion: rizin_libversion,
  name_suffix: lib_name_suffix,
  name_prefix: lib_name_prefix,
)

rz_main_dep = declare_dependency(link_with: rz_main,
                                include_directories: [platform_inc],
                                dependencies: rz_main_deps)
meson.override_dependency('rz_main', rz_main_dep)

pkgconfig_mod.generate(rz_main,
  subdirs: 'librz',
  version: rizin_version,
  name: 'rz_main',
  filebase: 'rz_main',
  requires: [
    'rz_core',
    'rz_demangler',
    'rz_asm',
    'rz_sign',
    'rz_diff',
    'rz_syscall'
  ],
  description: 'rizin foundation libraries',
  variables: [
    'datdir=@0@'.format(rizin_datdir_rz),
  ],
)

if not is_static_libs_only
  conf = configuration_data()
  conf.set('RZ_VERSION', rizin_version)
  conf.set('RIZIN_MODULE', rz_main.name())
  conf.set('RIZIN_MODULE_DEPS', ' '.join(['rz_core']))
  conf.set('PACKAGE_RELATIVE_PATH', cmake_package_relative_path)
  conf.set('INSTALL_INCDIR', rizin_incdir)
  conf.set('INSTALL_LIBDIR', rizin_libdir)
  conf.set('INSTALL_PLUGDIR', rizin_plugins)
  conf.set('rizin_libname', rz_main.name())
  cmake_mod.configure_package_config_file(
    name: conf.get('rizin_libname'),
    input: '../RzModulesConfig.cmake.in',
    install_dir: rizin_cmakedir / conf.get('rizin_libname'),
    configuration: conf,
  )
endif
