cmake_minimum_required(VERSION 3.10)
project(uds-c)

# 设置C标准
set(CMAKE_C_STANDARD 99)

# 设置构建类型为Debug，确保调试信息保留
set(CMAKE_BUILD_TYPE Debug)

# 添加编译选项以防止优化掉调试输出
add_compile_options(-O0 -g -Wall -Wextra -DDEBUG=1)

# 添加包含目录
include_directories(src)
include_directories(deps/isotp-c/deps/bitfield-c/src)
include_directories(deps/isotp-c/src)

# 收集所有源文件
file(GLOB_RECURSE UDS_SOURCES "src/**/*.c")
file(GLOB_RECURSE ISOTP_SOURCES "deps/isotp-c/src/**/*.c")
file(GLOB_RECURSE BITFIELD_SOURCES "deps/isotp-c/deps/bitfield-c/src/**/*.c")

# 创建库
add_library(uds STATIC 
    ${UDS_SOURCES}
    ${ISOTP_SOURCES}
    ${BITFIELD_SOURCES}
)

# 可选：创建动态库
add_library(uds_shared SHARED 
    ${UDS_SOURCES}
    ${ISOTP_SOURCES}
    ${BITFIELD_SOURCES}
)
set_target_properties(uds_shared PROPERTIES OUTPUT_NAME uds)