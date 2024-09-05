cmake_minimum_required(VERSION 3.15)
project(counter_sdl)

set(CMAKE_CXX_STANDARD 14)
# Укажите путь к SDL2

set(SDL2_PATH "C:/SDL2_2_30_7")
set(SDL2_INCLUDE_DIR "${SDL2_PATH}/include")
set(SDL2_LIB_DIR "${SDL2_PATH}/lib/x86")

include_directories(${SDL2_INCLUDE_DIR})

# Укажите путь к исполняемым файлам
link_directories(${SDL2_LIB_DIR})

add_executable(counter_sdl main.cpp)

# Связывание SDL2 библиотеки с вашим проектом

target_link_libraries(counter_sdl SDL2main SDL2)