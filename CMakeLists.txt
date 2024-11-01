cmake_minimum_required(VERSION 3.12)

# Pull in PICO SDK (must be before project)
set(PICO_SDK_PATH $ENV{PICO_SDK_PATH})
include(${PICO_SDK_PATH}/pico_sdk_init.cmake)

project(pico2_jjy_receiver C CXX ASM)
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

# Initialize the SDK
pico_sdk_init()

add_executable(pico2_jjy_receiver)

target_sources(
    pico2_jjy_receiver PRIVATE 
    src/core0.cpp
    src/core1.cpp
)

target_include_directories(
    pico2_jjy_receiver PRIVATE
    src
)

target_link_libraries(
    pico2_jjy_receiver PRIVATE
    pico_stdlib
    pico_multicore
    hardware_dma
    hardware_pwm
    hardware_adc
    hardware_spi
)

pico_enable_stdio_usb(pico2_jjy_receiver 1)
pico_enable_stdio_uart(pico2_jjy_receiver 0)

pico_add_extra_outputs(pico2_jjy_receiver)
