cmake_minimum_required(VERSION 3.8)
project(libaesgm LANGUAGES C)

add_library(aesgm
    #sources
    ${CMAKE_CURRENT_SOURCE_DIR}/aescrypt.c
    ${CMAKE_CURRENT_SOURCE_DIR}/aeskey.c
    ${CMAKE_CURRENT_SOURCE_DIR}/aes_modes.c
    ${CMAKE_CURRENT_SOURCE_DIR}/aes_ni.c
    ${CMAKE_CURRENT_SOURCE_DIR}/aestab.c
    #headers
    ${CMAKE_CURRENT_SOURCE_DIR}/aescpp.h
    ${CMAKE_CURRENT_SOURCE_DIR}/aes.h
    ${CMAKE_CURRENT_SOURCE_DIR}/aes_ni.h
    ${CMAKE_CURRENT_SOURCE_DIR}/aesopt.h
    ${CMAKE_CURRENT_SOURCE_DIR}/aestab.h
    ${CMAKE_CURRENT_SOURCE_DIR}/aes_via_ace.h
    ${CMAKE_CURRENT_SOURCE_DIR}/brg_endian.h
    ${CMAKE_CURRENT_SOURCE_DIR}/brg_types.h
)

target_include_directories(aesgm
    INTERFACE
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
    $<INSTALL_INTERFACE:include/libaesgm>
)

if(WIN32 AND BUILD_SHARED_LIBS)
    target_compile_definitions(aesgm PRIVATE DLL_EXPORT)
endif()

install(TARGETS aesgm
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
)
install(
    FILES
    ${CMAKE_CURRENT_SOURCE_DIR}/aes.h
    ${CMAKE_CURRENT_SOURCE_DIR}/aes_ni.h
    ${CMAKE_CURRENT_SOURCE_DIR}/aes_via_ace.h
    ${CMAKE_CURRENT_SOURCE_DIR}/aescpp.h
    ${CMAKE_CURRENT_SOURCE_DIR}/aesopt.h
    ${CMAKE_CURRENT_SOURCE_DIR}/aestab.h
    ${CMAKE_CURRENT_SOURCE_DIR}/brg_endian.h
    ${CMAKE_CURRENT_SOURCE_DIR}/brg_types.h
    DESTINATION include
)
