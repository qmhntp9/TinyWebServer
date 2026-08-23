cmake_minimum_required(VERSION 3.10)
project(TinyWebServer)

# C++ 标准
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# 默认 Debug,可改 Release
if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Debug)
endif()

# 编译选项
if(CMAKE_BUILD_TYPE STREQUAL "Debug")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -g -O0")
else()
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O2")
endif()

# 源文件
set(SOURCES
    main.cpp
    config.cpp
    webserver.cpp
    http/http_conn.cpp
    timer/lst_timer.cpp
    log/log.cpp
    CGImysql/sql_connection_pool.cpp
)

# 可执行文件
set(SERVER_NAME server)
add_executable(${SERVER_NAME} ${SOURCES})

# 链接库
target_link_libraries(${SERVER_NAME} PRIVATE
    pthread
    mysqlclient
)

# 头文件包含路径(让 #include "xxx/xxx.h" 能找到)
target_include_directories(${SERVER_NAME} PRIVATE
    ${CMAKE_SOURCE_DIR}
)
