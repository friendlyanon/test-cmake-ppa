cmake_minimum_required(VERSION 3.18)

project(test)

file(DOWNLOAD
        "https://github.com/friendlyanon/test-cmake-ppa/archive/test.zip"
        "${PROJECT_BINARY_DIR}/test.zip")
file(MAKE_DIRECTORY "${PROJECT_BINARY_DIR}/temp/")
execute_process(
        WORKING_DIRECTORY "${PROJECT_BINARY_DIR}/temp"
        COMMAND "${CMAKE_COMMAND}" -E tar xvf "../test.zip")

execute_process(COMMAND tree -I CMakeFiles "${PROJECT_BINARY_DIR}")

file(GLOB dir LIST_DIRECTORIES YES "${PROJECT_BINARY_DIR}/temp/*")
file(RENAME "${dir}" "${PROJECT_BINARY_DIR}/test")

add_executable(cmake_test "${PROJECT_BINARY_DIR}/test/main.cpp")

enable_testing()
add_test(NAME cmake_test COMMAND cmake_test)
