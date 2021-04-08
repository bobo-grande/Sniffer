#### Clion配置Winpcap开发环境
##### 1. 下载安装winpcap相关文件  
* 下载winpcap4.1.3：https://www.winpcap.org/install/default.htm，安装程序放到任意目录下，运行该安装程序即可  
* 下载winpcap开发包：https://www.winpcap.org/devel.htm，下载到任意目录，解压即可
##### 2. clion中配置
* 打开clion,新建一个c project `testclion1`(你可以任意命名，但要保证工程路径以及工程名不含中文)
* 将下载的的Winpcap开发包文件夹`WpdPack`中的`Include`和`Lib`文件夹复制到工程目录下（为了后面方便指定路径，你也可以不进行这一步，而在后面的CMakeLists.txt的配置中使用绝对路径）
##### 3. 配置CMakeLists.txt
* 使用clion新建工程时会自动在工程目录下生成`CMakeLists.txt`文件（如果没有，就自己新建一个）
* 你可以直接使用我的配置，把下面代码粘贴到`CMakeLists.txt`中。
```c
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
```
* 我在上面简单标注了一些信息，更多关于CMake的知识请自行学习。
##### 4. 运行
* 基于你的测试程序，可能会提示有某些函数找不到，这时，你需要在程序文件开头中加入如下注释
```c
#define HAVE_REMOTE
#define WPCAP
```
* 之后就可以build运行了。目录中提供了一份简单的测试程序`main.c`，用于列出你的网卡信息。