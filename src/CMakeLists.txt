add_executable(pico_usb_dac
    main.c
)

target_compile_definitions(pico_usb_dac PRIVATE
    AUDIO_FREQ_MAX=48000

    # ours are zero based, so say so
    PICO_USBDEV_USE_ZERO_BASED_INTERFACES=1

    # need large descriptor
    PICO_USBDEV_MAX_DESCRIPTOR_SIZE=256

    PICO_USBDEV_ISOCHRONOUS_BUFFER_STRIDE_TYPE=1
    PICO_USBDEV_ENABLE_DEBUG_TRACE

    PICO_AUDIO_I2S_MONO_OUTPUT=0
    PICO_AUDIO_I2S_MONO_INPUT=0

    PICO_DEFAULT_UART_BAUD_RATE=9600
)

target_sources(pico_usb_dac PRIVATE
    main.c
)

target_link_libraries(pico_usb_dac PRIVATE
    pico_stdlib
    usb_device
    pico_audio_i2s
    pico_multicore
)

pico_add_extra_outputs(pico_usb_dac)

add_custom_command(TARGET pico_usb_dac
    POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy ${PROJECT_BINARY_DIR}/src/pico_usb_dac.uf2 ${PROJECT_SOURCE_DIR}/build_uf2/pico_usb_dac.uf2
)