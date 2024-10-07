# ---------------------------------------------------
# CMakeLists.txt
#
# Author: Thomas Choquet <semoir.dense-0h@icloud.com>
# Date: 2024/10/07 09:49:07
# ---------------------------------------------------

cmake_minimum_required(VERSION 3.16)

add_executable(hello hello.c)
target_link_libraries(hello PRIVATE tinyfiledialogs)