# 指定最低CMake版本
cmake_minimum_required(VERSION 3.17)

# 项目名称
project(learning-cxx)

# 设置C++标准
set(CMAKE_CXX_STANDARD 11)

# 包含根目录
include_directories(${PROJECT_SOURCE_DIR})

# 查找exercises目录下所有的cpp文件
file(GLOB_RECURSE EXERCISE_SOURCES
        exercises/*/main.cpp
)

# 为每个练习创建可执行文件
foreach(SOURCE_FILE ${EXERCISE_SOURCES})
    # 获取包含main.cpp的父目录名作为可执行文件名
    get_filename_component(PARENT_DIR ${SOURCE_FILE} DIRECTORY)
    get_filename_component(TARGET_NAME ${PARENT_DIR} NAME)

    # 替换特殊字符为下划线
    string(REPLACE "&" "_and_" SAFE_TARGET_NAME ${TARGET_NAME})

    # 添加可执行文件
    add_executable(${SAFE_TARGET_NAME} ${SOURCE_FILE})
endforeach()