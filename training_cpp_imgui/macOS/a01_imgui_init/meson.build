project(
  'my_init', ['c','cpp'],
  version : '0.1',
  default_options : [
    'buildtype=debugoptimized',
    'cpp_std=c++17',
    'warning_level=1',
  ])

compiler = meson.get_compiler('cpp')
sdl3Dep = dependency('sdl3')
threadDep = dependency('threads')
XrandrDep = dependency('Xrandr', required: false)

libsPath = '/opt/homebrew/include'
if not sdl3Dep.found()
  sdl3Dep = compiler.find_library('sdl3', dirs: libsPath)
endif
if not XrandrDep.found()
  XrandrDep = compiler.find_library('Xrandr', dirs: libsPath)
endif

my_project_name = meson.current_source_dir().split('/').get(-1)

src_files = [
  'src/main.cpp'
]

inc = include_directories('include')
executable(my_project_name, src_files,
          include_directories : inc,
          dependencies: [
                        sdl3Dep, threadDep
                        ])
