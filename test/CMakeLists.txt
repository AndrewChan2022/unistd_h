cmake_minimum_required(VERSION 3.21)

project(testunistd LANGUAGES C)

add_executable(testunistd example.c)

# add to windows env path or manually add to CMAKE_PREFIX_PATH
list(APPEND CMAKE_PREFIX_PATH ${CMAKE_CURRENT_SOURCE_DIR}/../windowsbuild/unistd)
find_package(unistd REQUIRED)
list_package_targets(unistd)
target_link_libraries(testunistd PRIVATE unistd::unistd)

# target_include_directories(testunistd PRIVATE ${CMAKE_SOURCE_DIR})
