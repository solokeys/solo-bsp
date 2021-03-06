[![License](https://img.shields.io/badge/License-Apache%202.o-yellogreen.svg)](https://github.com/solokeys/solo-bsc/blob/master/LICENSE-APACHE) [![License](https://img.shields.io/badge/License-MIT-yellow.svg)](https://github.com/solokeys/solo-bsc/blob/master/LICENSE-MIT) [![Crates](https://img.shields.io/crates/v/solo-bsc.svg)](https://crates.io/crates/solo-bsc)

# solo-bsc
This is a (WIP!) [Rust](https://github.com/rust-embedded) board support package for the open source Solo security key.

This key [consists of](https://github.com/solokeys/solo-hw):
- an STM32L432KC microcontroller
- either a USB-A or USB-C connector
- a clicky dome button
- 3 LEDs
- an NCP114 voltage regulator
- and various resistors, capacitors, and Zener diodes

One specialty is that it has a [custom USB bootloader](https://solo.solokeys.io/building/), allowing easy updates. To use it, `FLASH ORIGIN` in [memory.x](https://github.com/solokeys/solo-bsc/blob/master/memory.x) needs to be set to `0x800_5000` instead of the conventional `0x800_0000`.
Alternatively, the ST DFU bootloader can be used.
Additionally, serial TX/RX and all SWD pins (SWDIO, SWCLK, SWO) are [kind of broken out](https://conorpp.com/3d-printing-a-programming-jig-and-embedding-pogo-pins-using-eagle-and-fusion-360).

## Quickstart
You need stable Rust 2018 edition, for details see the [embedded book](https://docs.rust-embedded.org/book/intro/install.html), in short:
```
curl https://sh.rustup.rs -sSf | sh
rustup target add thumbv7em-none-eabihf
cargo install cargo-binutils
rustup component add llvm-tools-preview
```

To build blinky, run `make blinky`. You end up with a `blinky.hex` file.

To flash it to your Solo Hacker:
- insert Solo and boot to Solo bootloader by pressing the button for ~2 seconds (it starts to blink)
- [setup Solotool](https://github.com/solokeys/solo/blob/master/README.md#solo-for-hackers) and make sure you can flash the original [`solo.hex`](https://github.com/solokeys/solo/releases/download/basic-hacker-build/solo.hex)
- run `tools/solotool.py /path/to/blinky.hex`
- watch the green LED blink :tada:

## License

Licensed under either of

- Apache License, Version 2.0 ([LICENSE-APACHE](LICENSE-APACHE) or
  http://www.apache.org/licenses/LICENSE-2.0)
- MIT license ([LICENSE-MIT](LICENSE-MIT) or http://opensource.org/licenses/MIT)

at your option.

### Contribution

Unless you explicitly state otherwise, any contribution intentionally submitted for inclusion in the
work by you, as defined in the Apache-2.0 license, shall be dual licensed as above, without any
additional terms or conditions.
