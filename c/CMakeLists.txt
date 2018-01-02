cmake_minimum_required(VERSION 3.4.1)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -std=gnu99")

# Android 5.0 以上需要在此处设置 PIE
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -fPIE")
set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -fPIE -pie")

# 配置使用 NDK Standalone Toolchain 编译
set(NDK_STANDALONE_TOOLCHAIN /tmp/ndk-hm/arm-linux-androideabi)
set(CMAKE_SYSTEM_NAME Android)
set(CMAKE_SYSTEM_VERSION 21)
set(CMAKE_C_COMPILER ${NDK_STANDALONE_TOOLCHAIN}/bin/clang)
set(CMAKE_CXX_COMPILER ${NDK_STANDALONE_TOOLCHAIN}/bin/clang++)
set(CMAKE_FIND_ROOT_PATH ${NDK_STANDALONE_TOOLCHAIN})

# 使用 NDK 提供的头文件
add_definitions("--sysroot=${NDK_STANDALONE_TOOLCHAIN}/sysroot")

add_library(myso SHARED CTest.c)

set_target_properties(myso
                      PROPERTIES
                      LIBRARY_OUTPUT_DIRECTORY
                      "${CMAKE_CURRENT_SOURCE_DIR}/lib")

include_directories(/home/hm/JDK/jdk1.8.0_151/include /home/hm/JDK/jdk1.8.0_151/include/linux)

target_link_libraries(myso
                     log)

