#1.cmake verson，指定cmake版本 
cmake_minimum_required(VERSION 3.2)

#2.project name，指定项目的名称，一般和项目的文件夹名称对应
project(chat_application)

#C11标准，现在一般都用这个
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED TRUE)
#5.set environment variable，设置环境变量，编译用到的源文件全部都要放到这里，否则编译能够通过，但是执行的时候会出现各种问题，比如"symbol lookup error xxxxx , undefined symbol"
set(TEST_MATH ${DIR_SRCS})

#3.head file path，头文件目录
include_directories(include)

#4.source directory，源文件目录
aux_source_directory(src DIR_SRCS)


find_package(Threads)
find_package(GTK2 2.6 REQUIRED gtk)

if (GTK2_FOUND)
    include_directories(${GTK2_INCLUDE_DIRS})
    # add_executable(main main.c)
    # target_link_libraries(main ${GTK2_LIBRARIES})
endif ()

#Release模式编译更快，也可以使用Debug模式试一下
if(NOT CMAKE_BUILD_TYPE)
  SET(CMAKE_BUILD_TYPE Release)
endif()

#6.add executable file，添加要编译的可执行文件
add_executable(${PROJECT_NAME} ${DIR_SRCS})

#7.add link library，添加可执行文件所需要的库，比如我们用到了libm.so（命名规则：lib+name+.so），就添加该库的名称
TARGET_LINK_LIBRARIES(${PROJECT_NAME} ${GTK2_LIBRARIES})








