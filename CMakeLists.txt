cmake_minimum_required(VERSION 3.28.2)
project(planning)
set(CMAKE_CXX_STANDARD 17)

# 变量和目录设置
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/bin)
# 动态库和exe都指定到bin目录下面
# Linux下用到的是CMAKE_LIBRARY_OUTPUT_DIRECTORY
# 静态库是CMAKE_ARCHIVE_OUTPUT_DIRECTORY 只会定义库的位置 而不管可执行文件

# 生成动态库 与 包含 他所依赖的头文件的目录
aux_source_directory(${PROJECT_SOURCE_DIR}/src SRC_LISTS)
add_library(common 
SHARED
${SRC_LISTS}
)

target_include_directories(common
PUBLIC
${PROJECT_SOURCE_DIR}/include
)

# 生成可执行文件 与 包含 他所依赖的头文件的目录
add_executable(planning_main planning_main.cpp)

# 动态库是一个target
target_include_directories(planning_main
PUBLIC
${PROJECT_SOURCE_DIR}/include
)

# 可执行文件链接动态库
target_link_libraries(planning_main
PUBLIC
common
)