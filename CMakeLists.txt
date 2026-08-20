cmake_minimum_required(VERSION 3.10)
project(WebServer CXX)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# DEBUG 选项，与原 makefile 的 DEBUG 一致（默认 ON）
option(DEBUG "Enable debug build" ON)
if(DEBUG)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -g")
else()
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O2")
endif()

# 源文件
set(SERVER_SOURCES
    main.cpp
    webserver.cpp
    config.cpp
    timer/lst_timer.cpp
    http/http_conn.cpp
    log/log.cpp
    CGImysql/sql_connection_pool.cpp
)

# 头文件搜索路径
include_directories(
    ${CMAKE_SOURCE_DIR}
    ${CMAKE_SOURCE_DIR}/timer
    ${CMAKE_SOURCE_DIR}/http
    ${CMAKE_SOURCE_DIR}/log
    ${CMAKE_SOURCE_DIR}/CGImysql
    ${CMAKE_SOURCE_DIR}/lock
    ${CMAKE_SOURCE_DIR}/threadpool
)

# 可执行文件
add_executable(server ${SERVER_SOURCES})

# 链接库
target_link_libraries(server
    pthread
    mysqlclient
)
