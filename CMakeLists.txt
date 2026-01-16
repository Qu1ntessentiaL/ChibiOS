cmake_minimum_required(VERSION 3.15)

set(LIBRARY_NAME chibios-nil)
set(CHCONF_H_DIR ${CMAKE_SOURCE_DIR}/src/nil)

#Найти все C-файлы в директории
file(GLOB_RECURSE ALL_C_SOURCES "os/nil/src/*.c")

# Исключить некоторые файлы
list(REMOVE_ITEM ALL_C_SOURCES
        os/nil/src/example.c
)

add_library(${LIBRARY_NAME} STATIC
        os/common/ports/ARMv6-M/compilers/GCC/chcoreasm.S
        os/common/ports/ARMv6-M/chcore.c
        ${ALL_C_SOURCES}
)

target_include_directories(${LIBRARY_NAME} PUBLIC
        ${CHCONF_H_DIR}
        os/nil/include/
        os/common/ports/ARM-common/
        os/common/ports/ARMv6-M/
        os/common/portability/GCC/
        os/common/startup/ARMCMx/devices/STM32F0xx
        os/license/
        os/oslib/include/
)

# target_link_libraries(${LIBRARY_NAME} PUBLIC cmsis)

# target_compile_definitions(${LIBRARY_NAME} PUBLIC
#         -DSTM32F030x6
# )