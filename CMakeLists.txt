# CMake 最低版本要求
cmake_minimum_required(VERSION 3.10)

# 项目名 + 语言
project(TinyWebServer CXX)

# C++ 标准
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# 编译选项:默认 Debug,可切 Release
if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Debug)
endif()
set(CMAKE_CXX_FLAGS_DEBUG "-g")
set(CMAKE_CXX_FLAGS_RELEASE "-O2")

# 可执行文件名
set(SERVER_NAME server)

# 源文件列表
set(SOURCES
    main.cpp
    webserver.cpp
    config.cpp
    http/http_conn.cpp
    timer/lst_timer.cpp
    log/log.cpp
    CGImysql/sql_connection_pool.cpp
)

# 生成可执行文件
add_executable(${SERVER_NAME} ${SOURCES})

# 头文件包含路径(子模块用 #include "xxx/xxx.h" 形式)
target_include_directories(${SERVER_NAME} PRIVATE
    ${CMAKE_SOURCE_DIR}
)

# 链接库:pthread + mysqlclient
target_link_libraries(${SERVER_NAME} PRIVATE
    pthread
    mysqlclient
)

# 安装规则(可选)
install(TARGETS ${SERVER_NAME} DESTINATION bin)
