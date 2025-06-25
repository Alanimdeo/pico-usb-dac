# Pico USB DAC

Simple USB DAC with I2S output for Raspberry Pi Pico.

## Usage

1. `git clone` this repository
1. `git submodule update --init --recursive`
1. `mkdir build && cd build`
1. `cmake ..`
1. `make -j4`
1. Flash `build_uf2/pico_usb_dac.uf2` to your Raspberry Pi Pico.
