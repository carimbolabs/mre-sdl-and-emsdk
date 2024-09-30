cmake_minimum_required(VERSION 3.20)

project(mre)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

set(SDL2_MAIN SDL2::SDL2main)

find_package(SDL2 CONFIG REQUIRED)

file(GLOB SOURCE_FILES "*.cpp")

add_executable(${PROJECT_NAME} ${SOURCE_FILES})

if (${CMAKE_SYSTEM_NAME} MATCHES "Emscripten")
  target_link_libraries(${PROJECT_NAME} "-s EVAL_CTORS=1")
  target_link_libraries(${PROJECT_NAME} "-s WASM_BIGINT=1")
  target_link_libraries(${PROJECT_NAME} "-s ALLOW_MEMORY_GROWTH=1")
  target_link_libraries(${PROJECT_NAME} "-s INITIAL_MEMORY=134217728")
  target_link_libraries(${PROJECT_NAME} "-s EXPORTED_RUNTIME_METHODS=['callMain']")

  target_compile_options(${PROJECT_NAME} PRIVATE -Wall -Wextra -Werror -pedantic -O1 -flto)
endif()

target_link_libraries(${PROJECT_NAME} SDL2::SDL2-static)
target_link_libraries(${PROJECT_NAME} SDL2::SDL2main)
