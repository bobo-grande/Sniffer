cmake_minimum_required(VERSION 3.15)
project(testclion1 C)
#c的版本，根据新建工程时的选择自动生成
set(CMAKE_C_STANDARD 99)

#设置工程的头文件路径及库路径变量
#因为我之前已经将这两个文件夹复制到了工程目录下，所以直接使用相对路径就可以，如果你没有复制，就写绝对路径
#64位机器上库文件路径为 ./Lib/x64，32位机器应该要修改为 ./Lib
set(INC_DIR ./Include)
set(LINK_DIR ./Lib/x64)

#将设置的变量加入配置
include_directories(${INC_DIR})
link_directories(${LINK_DIR})

add_executable(testclion1 main.c)

#将第三方库链接在一起
target_link_libraries(testclion1 wpcap)