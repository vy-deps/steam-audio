cmake_minimum_required(VERSION 3.21.0)

project(steam-audio)
add_library(steam-audio SHARED IMPORTED)

target_include_directories(steam-audio INTERFACE ${CMAKE_CURRENT_LIST_DIR}/include)

if(WIN32)
  set_target_properties(steam-audio PROPERTIES
    IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/lib/windows-x64/phonon.dll
    IMPORTED_IMPLIB ${CMAKE_CURRENT_LIST_DIR}/lib/windows-x64/phonon.lib)
elseif(UNIX AND NOT APPLE)
  set_target_properties(steam-audio PROPERTIES
    IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/lib/linux-x64/libphonon.so)
else()
  message(FATAL_ERROR "not implemented for current platform")
endif()

macro(steam_audio_copy_bin target)
  add_custom_command(TARGET ${target} POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_if_different
    $<TARGET_FILE:steam-audio> $<TARGET_FILE_DIR:${target}>)
endmacro(steam_audio_copy_bin)

add_subdirectory(example)
