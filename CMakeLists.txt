cmake_minimum_required(VERSION 3.1)
project(wrf)
set(CMAKE_C_STANDARD 99)
include(CheckSymbolExists)
check_symbol_exists(epoll_create "sys/epoll.h" EPOLL_EXISTS)
if (EPOLL_EXISTS)
    set(EPOLL_ENABLE 1 CACHE INTERNAL "enable epoll")

else ()
    set(EPOLL_ENABLE "" CACHE INTERNAL "not enable epoll")
endif ()

configure_file(${CMAKE_CURRENT_SOURCE_DIR}/config.h.cmake
        ${CMAKE_CURRENT_SOURCE_DIR}/lib/config.h)

add_executable(http_server01 http_server01.c)
target_link_libraries(http_server01 wrf)

add_executable(http_server_test http_server_test.c)
target_link_libraries(http_server_test wrf)
add_subdirectory(lib/)
