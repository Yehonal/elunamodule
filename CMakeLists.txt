file(GLOB sources "${CMAKE_CURRENT_SOURCE_DIR}/lualib/src/*.c" "${CMAKE_CURRENT_SOURCE_DIR}/lualib/src/*.h")
list(REMOVE_ITEM sources "${CMAKE_CURRENT_SOURCE_DIR}/lualib/src/lua.c")
list(REMOVE_ITEM sources "${CMAKE_CURRENT_SOURCE_DIR}/lualib/src/luac.c")

set(lua_STAT_SRCS
  ${sources}
)

add_library(lualib STATIC ${lua_STAT_SRCS})

include_directories(
  "${CMAKE_CURRENT_SOURCE_DIR}/lualib/src"
)

add_subdirectory(src)
