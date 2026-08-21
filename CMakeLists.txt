cmake_minimum_required(VERSION 3.15)

project(stm32-h5-hal C)

file(GLOB HAL_SOURCES
    "STM32Cube_FW_H5_V1.7.0/Drivers/STM32H5xx_HAL_Driver/Src/*.c"
)

add_library(stm32-h5-hal ${HAL_SOURCES})

target_compile_options(stm32-h5-hal PRIVATE
    -mcpu=cortex-m33
    -mthumb
    -mfpu=fpv5-sp-d16
    -mfloat-abi=hard
)

target_compile_definitions(stm32-h5-hal PUBLIC
    USE_HAL_DRIVER
    STM32H533xx
)

target_include_directories(stm32-h5-hal PUBLIC
    "STM32Cube_FW_H5_V1.7.0/Drivers/CMSIS/Device/ST/STM32H5xx/Include"
    "STM32Cube_FW_H5_V1.7.0/Drivers/CMSIS/Include"
    "STM32Cube_FW_H5_V1.7.0/Drivers/STM32H5xx_HAL_Driver/Inc"
)

install(TARGETS stm32-h5-hal
    ARCHIVE DESTINATION lib
    LIBRARY DESTINATION lib
)

install(
    DIRECTORY
    STM32Cube_FW_H5_V1.7.0/Drivers/CMSIS/Include/
    DESTINATION include
)

install(
    DIRECTORY
    STM32Cube_FW_H5_V1.7.0/Drivers/CMSIS/Device/ST/STM32H5xx/Include/
    DESTINATION include
)

install(
    DIRECTORY
    STM32Cube_FW_H5_V1.7.0/Drivers/STM32H5xx_HAL_Driver/Inc/
    DESTINATION include
)