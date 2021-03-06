cmake_minimum_required(VERSION 2.8.8 FATAL_ERROR)
cmake_policy(VERSION 2.8.8)

# lua5.3
if (NOT LUA53_INCLUDE_DIRS)
    #add_subdirectory(../lua5.3 ${CMAKE_CURRENT_LIST_DIR})
endif(NOT LUA53_INCLUDE_DIRS)

list(APPEND ejoy2d_include_dirs
  ${CMAKE_CURRENT_LIST_DIR}/msvc/include
  ${CMAKE_CURRENT_LIST_DIR}/lib/render
  ${CMAKE_CURRENT_LIST_DIR}/lib
  ${CMAKE_CURRENT_LIST_DIR}/msvc/src/glew
  ${LUA53_INCLUDE_DIRS}/..
  )

##################################################################################################
#ejoy2d\ejoy2d.gyp:ejoy2d#target
set(my_target "ejoy2d")
set(TARGET ${my_target})
set(TOOLSET "target")

set(EJOY2D_INCLUDE_DIRS ${EJOY2D_INCLUDE_DIRS} ${CMAKE_CURRENT_LIST_DIR}/lib CACHE INTERNAL "ejoy2d include dir")
message("EJOY2D_INCLUDE_DIRS= ${EJOY2D_INCLUDE_DIRS}")

list(APPEND my_srcs
  lib/array.h
  lib/dfont.c
  lib/dfont.h
  lib/ejoy2dgame.c
  lib/ejoy2dgame.h
  lib/fault.c
  lib/fault.h
  lib/label.c
  lib/label.h
  lib/lejoy2dcore.c
  lib/lgeometry.c
  lib/lgeometry.h
  lib/list.h
  lib/lmatrix.c
  lib/lmatrix.h
  lib/lparticle.c
  lib/lrenderbuffer.c
  lib/lrenderbuffer.h
  lib/lshader.c
  lib/lsprite.c
  lib/material.h
  lib/matrix.c
  lib/matrix.h
  lib/opengl.h
  lib/particle.c
  lib/particle.h
  lib/platform_print.h
  lib/ppm.c
  lib/ppm.h
  lib/renderbuffer.c
  lib/renderbuffer.h
  lib/scissor.c
  lib/scissor.h
  lib/screen.c
  lib/screen.h
  lib/screenshot.c
  lib/screenshot.h
  lib/shader.c
  lib/shader.h
  lib/sprite.c
  lib/sprite.h
  lib/spritepack.c
  lib/spritepack.h
  lib/texture.c
  lib/texture.h
  #render
  lib/render/blendmode.h
  lib/render/block.h
  lib/render/carray.c
  lib/render/carray.h
  lib/render/log.c
  lib/render/log.h
  lib/render/render.c
  lib/render/render.h
  )
if(WIN32)
list(APPEND my_srcs
  #glew
  msvc/src/glew/GL/glew.h
  msvc/src/glew/GL/wglew.h
  msvc/src/glew/glew.c
  #win-lua
  msvc/include/lauxlib.h
  msvc/include/lua.h
  msvc/include/lua_path.h
  msvc/include/lualib.h
  msvc/include/stdbool.h
  #winfont
  mingw/winfont.c
)
else()

endif()

add_library(${my_target} STATIC ${my_srcs} )
set_property(TARGET ${my_target} APPEND PROPERTY INCLUDE_DIRECTORIES ${ejoy2d_include_dirs})
#target_compile_definitions(${my_target}
  #PUBLIC LUA_BUILD_AS_DLL=1
#)

target_link_libraries(${my_target}
  "lua5.3"
)
if(WIN32)
  set_target_properties(${my_target} PROPERTIES COMPILE_DEFINITIONS "EJOY2D_LUA=include;GLEW_STATIC")
  set_target_properties(${my_target} PROPERTIES COMPILE_FLAGS "/TP") #CXX
  target_link_libraries(${my_target} opengl32)
else()
  
endif()

unset(TOOLSET)
unset(TARGET)
unset(my_srcs)
unset(my_target)







