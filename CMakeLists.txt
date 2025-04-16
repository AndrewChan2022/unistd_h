cmake_minimum_required(VERSION 3.15)
project(unistd VERSION 1.0.0 LANGUAGES C CXX)

# Define the header-only library
add_library(unistd INTERFACE)
add_library(unistd::unistd ALIAS unistd)

# Specify the include directories for the library
target_include_directories(unistd INTERFACE
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>
)

# Install the header file
install(FILES include/unistd.h
    DESTINATION include
)

# Install the library target and export it
install(TARGETS unistd
    EXPORT UnistdTargets
    INCLUDES DESTINATION include
)

# Generate and install the CMake package configuration files
include(CMakePackageConfigHelpers)

# Create the package configuration file
file(WRITE ${CMAKE_CURRENT_BINARY_DIR}/UnistdConfig.cmake.in "
@PACKAGE_INIT@

include(\"\${CMAKE_CURRENT_LIST_DIR}/UnistdTargets.cmake\")
check_required_components(unistd)
")

configure_package_config_file(
    ${CMAKE_CURRENT_BINARY_DIR}/UnistdConfig.cmake.in
    ${CMAKE_CURRENT_BINARY_DIR}/UnistdConfig.cmake
    INSTALL_DESTINATION share/unistd/cmake
)

# Create the version configuration file
write_basic_package_version_file(
    ${CMAKE_CURRENT_BINARY_DIR}/UnistdConfigVersion.cmake
    VERSION ${PROJECT_VERSION}
    COMPATIBILITY SameMajorVersion
)

# Install the package configuration files
install(FILES
    ${CMAKE_CURRENT_BINARY_DIR}/UnistdConfig.cmake
    ${CMAKE_CURRENT_BINARY_DIR}/UnistdConfigVersion.cmake
    DESTINATION share/unistd/cmake
)

# Install the export file
install(EXPORT UnistdTargets
    FILE UnistdTargets.cmake
    NAMESPACE unistd::
    DESTINATION share/unistd/cmake
)