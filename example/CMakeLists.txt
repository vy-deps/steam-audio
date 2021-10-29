project(steamaudio.example)

add_executable(steamaudio.example main.cpp)
target_link_libraries(steamaudio.example PRIVATE steamaudio)
set_target_properties(steamaudio.example PROPERTIES CXX_STANDARD 20 CXX_STANDARD_REQUIRED ON)
target_compile_definitions(steamaudio.example PRIVATE
  -DSTEAM_AUDIO_EXAMPLE_DIR="${CMAKE_CURRENT_LIST_DIR}"
  -D_CRT_SECURE_NO_WARNINGS)
steam_audio_copy_bin(steamaudio.example)
