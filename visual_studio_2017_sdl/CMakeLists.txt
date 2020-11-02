cmake_minimum_required(VERSION 3.10)
project(lvgl)
set(CMAKE_C_STANDARD 11)#C11
set(CMAKE_CXX_STANDARD 17)#C17
set(CMAKE_CXX_STANDARD_REQUIRED ON)

#头文件路径
include_directories(
    ${TOOLCHAIN_INC_DIR} 
    "./"
    "./SDL2/include"
)
file(GLOB_RECURSE INCLUDES "lv_drivers/*.h" "lv_examples/*.h"  "lvgl/*.h"  "./*.h" )
file(GLOB_RECURSE SOURCES  "lv_drivers/*.c" "lv_examples/*.c"  "lvgl/src/*.c" )

SET(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin) 
#关闭警告
add_compile_options(-Wno-unused-private-field -Wno-unused-variable -Wno-deprecated-declarations -Wno-unused-function -Wno-implicit-function-declaration)
LINK_DIRECTORIES(
        "SDL2/lib/x64"
"C:/Program Files (x86)/Windows Kits/10/Lib/10.0.18362.0/um/x64" 
"C:/Program Files (x86)/Microsoft Visual Studio/2019/Community/VC/Tools/MSVC/14.24.28314/lib/x64"
"C:/Program Files (x86)/Microsoft Visual Studio/2019/Community/VC/Tools/MSVC/14.24.28314/atlmfc/lib/x64"
"C:/Program Files (x86)/Microsoft Visual Studio/2019/Community/VC/Auxiliary/VS/lib/x64"
"C:/Program Files (x86)/Windows Kits/10/lib/10.0.18362.0/ucrt/x64"
"C:/Program Files (x86)/Microsoft Visual Studio/2019/Community/VC/Auxiliary/VS/UnitTest/lib"
"C:/Program Files (x86)/Windows Kits/NETFXSDK/4.7.2/lib/um/x64")
add_executable(main main.c ${SOURCES} ${INCLUDES})
target_link_libraries(main PRIVATE SDL2 SDL2main )
add_custom_target (run COMMAND ${EXECUTABLE_OUTPUT_PATH}/main)
