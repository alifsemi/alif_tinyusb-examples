cmake_minimum_required(VERSION 3.20)

# Set TinyUSB library location
set(TINYUSB_LOCATION ${CMAKE_CURRENT_SOURCE_DIR}/../../../lib/tinyusb)
# Set FreeRTOS build
set(RTOS freertos)
# Set app name
set(PROJECT hid_composite_freertos)

# Add native TinyUSB example
add_subdirectory(${TINYUSB_LOCATION}/examples/device/${PROJECT} ${PROJECT})
# Set project name
project(${PROJECT}_wrapper)

# Generate *.bin and *.hex file
add_custom_target(generate_binaries ALL
  COMMAND ${CMAKE_OBJCOPY} -O binary $<TARGET_FILE:${PROJECT}> ${PROJECT}.bin
  COMMAND ${CMAKE_OBJCOPY} -O ihex   $<TARGET_FILE:${PROJECT}> ${PROJECT}.hex
  DEPENDS ${PROJECT}
)
