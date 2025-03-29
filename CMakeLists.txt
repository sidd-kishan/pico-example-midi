cmake_minimum_required(VERSION 3.31)

set(PICO_BOARD pico_w)
#set(PICO_NO_PICOTOOL true)
set(PICO_SDK_PATH ../../pico-webserver-2.0/pico-sdk)
include(pico_sdk_import.cmake)

project(test_project C CXX ASM)

set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)
pico_sdk_init()

add_executable(pico-example-midi
  pico-example-midi.c
  usb_descriptors.c
)

pico_enable_stdio_usb(pico-example-midi 0)
pico_enable_stdio_uart(pico-example-midi 1)

target_include_directories(pico-example-midi PRIVATE ${CMAKE_CURRENT_LIST_DIR})

pico_add_extra_outputs(pico-example-midi)
target_link_libraries(pico-example-midi PRIVATE pico_stdlib tinyusb_device tinyusb_board)
