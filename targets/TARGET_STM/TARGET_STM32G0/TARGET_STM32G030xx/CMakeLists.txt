# Copyright (c) 2020 ARM Limited. All rights reserved.
# SPDX-License-Identifier: Apache-2.0

if(${MBED_TOOLCHAIN} STREQUAL "GCC_ARM")
    set(STARTUP_FILE TOOLCHAIN_GCC_ARM/startup_stm32g030xx.S)
    set(LINKER_FILE TOOLCHAIN_GCC_ARM/stm32g030xx.ld)
elseif(${MBED_TOOLCHAIN} STREQUAL "ARM")
    set(STARTUP_FILE TOOLCHAIN_ARM/startup_stm32g030xx.S)
    set(LINKER_FILE TOOLCHAIN_ARM/stm32g030xx.sct)
endif()

add_library(mbed-stm32g030xx INTERFACE)

target_sources(mbed-stm32g030xx
    INTERFACE
        ${STARTUP_FILE}
)

target_include_directories(mbed-stm32g030xx
    INTERFACE
        .
)

mbed_set_linker_script(mbed-stm32g030xx ${CMAKE_CURRENT_SOURCE_DIR}/${LINKER_FILE})

target_link_libraries(mbed-stm32g030xx INTERFACE mbed-stm32g0)
