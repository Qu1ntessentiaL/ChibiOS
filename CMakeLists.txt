cmake_minimum_required(VERSION 3.15)

set(LIBRARY_NAME chibios-nil)
set(CHCONF_H_DIR ${CMAKE_SOURCE_DIR}/src/nil)

#Найти все C-файлы в директории
file(GLOB_RECURSE ALL_C_SOURCES
        "os/nil/src/*.c"
        "os/oslib/src/*.c"
)

# Исключить некоторые файлы
# list(REMOVE_ITEM ALL_C_SOURCES
#         os/nil/src/example.c
# )

add_library(${LIBRARY_NAME} STATIC
        os/common/ports/AVR/chcore.c
        ${ALL_C_SOURCES}
)

target_include_directories(${LIBRARY_NAME} PUBLIC
        ${CHCONF_H_DIR}
        os/nil/include/
        os/common/ports/AVR/
        os/common/ports/AVR/compilers/GCC
        os/common/portability/GCC/
        os/license/
        os/oslib/include/
)
