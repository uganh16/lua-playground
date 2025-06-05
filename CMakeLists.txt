cmake_minimum_required(VERSION 3.16)
project(lua-playground LANGUAGES C CXX)

file(GLOB LUA_SOURCES "${CMAKE_SOURCE_DIR}/vendor/lua/*.c")
list(REMOVE_ITEM LUA_SOURCES
  "${CMAKE_SOURCE_DIR}/vendor/lua/lua.c"
  "${CMAKE_SOURCE_DIR}/vendor/lua/luac.c"
  "${CMAKE_SOURCE_DIR}/vendor/lua/onelua.c"
)
add_library(lua STATIC ${LUA_SOURCES})
target_include_directories(lua PUBLIC
  "${CMAKE_SOURCE_DIR}/vendor/lua"
)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_executable(lua-playground "${CMAKE_SOURCE_DIR}/src/main.cc")
target_link_libraries(lua-playground PRIVATE lua)
