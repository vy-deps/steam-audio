project(steam-audio-example)

add_executable(steam-audio-example main.cpp)
target_link_libraries(steam-audio-example PRIVATE steam-audio)
set_target_properties(steam-audio-example PROPERTIES CXX_STANDARD 20 CXX_STANDARD_REQUIRED ON)
target_compile_definitions(steam-audio-example PRIVATE
  -DSTEAM_AUDIO_EXAMPLE_DIR="${CMAKE_CURRENT_LIST_DIR}"
  -D_CRT_SECURE_NO_WARNINGS)
steam_audio_copy_bin(steam-audio-example)
