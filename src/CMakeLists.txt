#
# Copyright (C) 2010 - 2016 Eluna Lua Engine <http://emudevs.com/>
# This program is free software licensed under GPL version 3
# Please see the included DOCS/LICENSE.md for more information
#

# Copyright (C)
#
# This file is free software; as a special exception the author gives
# unlimited permission to copy and/or distribute it, with or without
# modifications, as long as this notice is preserved.
#
# This program is distributed in the hope that it will be useful, but
# WITHOUT ANY WARRANTY, to the extent permitted by law; without even the
# implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

if( USE_COREPCH )
  # include_directories(${CMAKE_CURRENT_BINARY_DIR})
endif()

file(GLOB sources_localdir *.cpp *.h)

# Manually set sources for Debugging directory as we don't want to include WheatyExceptionReport in eluna project
# It needs to be included both in authserver and worldserver for the static global variable to be properly initialized
# and to handle crash logs on windows
# set(sources_Debugging Debugging/Errors.cpp Debugging/Errors.h)

#
# Build eluna sourcelist
#

# if (USE_COREPCH)
#   set(eluna_STAT_PCH_HDR PrecompiledHeaders/elunaPCH.h)
#   set(eluna_STAT_PCH_SRC PrecompiledHeaders/elunaPCH.cpp)
# endif()

set(eluna_STAT_SRCS
  ${eluna_STAT_SRCS}
  ${sources_localdir}
  # Debugging/Errors.h
)

include_directories(
  ${CMAKE_BINARY_DIR}
  ${CMAKE_SOURCE_DIR}/modules/worldengine/deps/recastnavigation/Detour
  ${CMAKE_SOURCE_DIR}/modules/worldengine/deps/SFMT
  ${CMAKE_SOURCE_DIR}/modules/worldengine/deps/sockets/include
  ${CMAKE_SOURCE_DIR}/modules/worldengine/deps/utf8cpp
  ${CMAKE_SOURCE_DIR}/src
  ${CMAKE_CURRENT_SOURCE_DIR}
  ${CMAKE_SOURCE_DIR}/src/game/Entities/Object
  ${ACE_INCLUDE_DIR}
  ${MYSQL_INCLUDE_DIR}
  ${OPENSSL_INCLUDE_DIR}
)

add_library(eluna STATIC
  ${eluna_STAT_SRCS}
  ${eluna_STAT_PCH_SRC}
)

target_link_libraries(eluna
  ${ACE_LIBRARY}
  shared
)

# Generate precompiled header
if (USE_COREPCH)
  # add_cxx_pch(eluna ${eluna_STAT_PCH_HDR} ${eluna_STAT_PCH_SRC})
endif ()

