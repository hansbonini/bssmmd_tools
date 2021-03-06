# compute default library install dir
set (_DEFAULT_LIBRARY_INSTALL_DIR lib)
if (EXISTS "${CMAKE_INSTALL_PREFIX}/lib32/" AND CMAKE_SIZEOF_VOID_P EQUAL 4)
set (_DEFAULT_LIBRARY_INSTALL_DIR lib32)
elseif (EXISTS "${CMAKE_INSTALL_PREFIX}/lib64/" AND CMAKE_SIZEOF_VOID_P EQUAL 8)
set (_DEFAULT_LIBRARY_INSTALL_DIR lib64)
endif ()

# the library install dir
set(LIBRARY_INSTALL_DIR "${_DEFAULT_LIBRARY_INSTALL_DIR}" CACHE PATH "Installation directory for libraries")

# make the library install dir an absolute path (can be important e.g. when using CONFIGURE_FILE to embed
# the library installation directory into a file)
if(NOT IS_ABSOLUTE "${LIBRARY_INSTALL_DIR}")
set(LIBRARY_INSTALL_DIR "${CMAKE_INSTALL_PREFIX}/${LIBRARY_INSTALL_DIR}")
endif()

add_library(kosinski_static STATIC kosinski.cc)
SET_TARGET_PROPERTIES(kosinski_static PROPERTIES OUTPUT_NAME kosinski)
add_library(kosinski_shared SHARED kosinski.cc)
SET_TARGET_PROPERTIES(kosinski_shared PROPERTIES OUTPUT_NAME kosinski)
add_library(enigma_static STATIC enigma.cc)
SET_TARGET_PROPERTIES(enigma_static PROPERTIES OUTPUT_NAME enigma)
add_library(enigma_shared SHARED enigma.cc)
SET_TARGET_PROPERTIES(enigma_shared PROPERTIES OUTPUT_NAME enigma)
add_library(nemesis_static STATIC nemesis.cc)
SET_TARGET_PROPERTIES(nemesis_static PROPERTIES OUTPUT_NAME nemesis)
add_library(nemesis_shared SHARED nemesis.cc)
SET_TARGET_PROPERTIES(nemesis_shared PROPERTIES OUTPUT_NAME nemesis)
add_library(saxman_static STATIC GetFileSize.cpp S-Compressor.cpp S-Decompressor.cpp)
SET_TARGET_PROPERTIES(saxman_static PROPERTIES OUTPUT_NAME saxman)
add_library(saxman_shared SHARED GetFileSize.cpp S-Compressor.cpp S-Decompressor.cpp)
SET_TARGET_PROPERTIES(saxman_shared PROPERTIES OUTPUT_NAME saxman)

install(TARGETS kosinski_static enigma_static nemesis_static saxman_static ARCHIVE DESTINATION ${LIBRARY_INSTALL_DIR})
install(TARGETS kosinski_shared enigma_shared nemesis_shared saxman_shared LIBRARY DESTINATION ${LIBRARY_INSTALL_DIR})
