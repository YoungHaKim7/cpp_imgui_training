project(
  'my_init', ['c', 'cpp'],
  version : '0.1',
  default_options : [
    'buildtype=debugoptimized',
    'cpp_std=c++17',
    'warning_level=1',
    'werror=false',
  ]
)

# Compiler and base dependencies
compiler = meson.get_compiler('cpp')
thread_dep = dependency('threads')
glfw_dep = dependency('glfw3')
opengl_dep = dependency('gl')

# ImGui source files
imgui_sources = [
  'imgui/imgui.cpp',
  'imgui/imgui_demo.cpp',
  'imgui/imgui_draw.cpp',
  'imgui/imgui_widgets.cpp',
  'imgui/imgui_impl_glfw.cpp',
  'imgui/imgui_impl_opengl3.cpp'
]

# Build ImGui as static library
libimgui = static_library(
  'imgui',
  files(imgui_sources),
  cpp_args: [
    '-DIMGUI_IMPL_OPENGL_LOADER_GLAD',
    '-w'
  ],
  dependencies: [glfw_dep, opengl_dep],
  include_directories: include_directories('include'),
  install: false
)

# ImGui dependency declaration
imgui_dep = declare_dependency(
  link_with: libimgui,
  include_directories: include_directories('include'),
  dependencies: [glfw_dep, opengl_dep]
)

# Project sources
src_files = [
  'src/main.cpp',
  'src/glad.c'  # Add Glad implementation
]

# Include directories
inc = include_directories(['include', 'include/glad'])

# Build executable
executable(
  meson.project_name(),
  src_files,
  include_directories: inc,
  dependencies: [
    thread_dep,
    glfw_dep,
    opengl_dep,
    imgui_dep,
    compiler.find_library('dl', required: true)  # For Linux DL library
  ],
  cpp_args: ['-DGLFW_INCLUDE_NONE']  # Prevent GLFW from including OpenGL headers
)
