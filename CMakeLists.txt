cmake_minimum_required(VERSION 3.18)

project(test)

file(DOWNLOAD
        "https://github.com/friendlyanon/test-cmake-ppa/archive/test.zip"
        "${PROJECT_BINARY_DIR}/test.zip")
file(ARCHIVE_EXTRACT INPUT "${PROJECT_BINARY_DIR}/test.zip"
        DESTINATION "${PROJECT_BINARY_DIR}/temp/")

file(GLOB_RECURSE tree
        LIST_DIRECTORIES YES
        RELATIVE "${PROJECT_BINARY_DIR}"
        "${PROJECT_BINARY_DIR}/**")
message(STATUS " --")
foreach(branch IN LISTS tree)
  if(NOT branch MATCHES "^CMakeFiles")
    message(STATUS "${branch}")
  endif()
endforeach()
message(STATUS " --")

file(GLOB dir LIST_DIRECTORIES YES "${PROJECT_BINARY_DIR}/temp/*")
file(RENAME "${dir}" "${PROJECT_BINARY_DIR}/test")

add_executable(cmake_test "${PROJECT_BINARY_DIR}/test/main.cpp")

enable_testing()
add_test(NAME cmake_test COMMAND cmake_test)
