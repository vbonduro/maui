# maui

# Development

## Setup

tbd, list of commands I used:

Followed app template instructions[2].

```
rustup update
rustup target add thumbv8m.main-none-eabi
cargo install cargo-binutils
rustup component add llvm-tools
sudo apt install libssl-dev 
sudo apt install pkg-config
cargo install cargo-generate
cargo install cargo-binstall
cargo binstall probe-rs-tools
cargo install flip-link
```

To create the project:

Need to install SPM --- onetime setup on board

["0.18.0"](https://github.com/nrf-rs/nrf-hal/tree/master/nrf9160-hal#secure-vs-non-secure)

In order to west build and west flash I had to do this:

# Build and Flash SPM for Actinius Icarus Board

## 1. Download Zephyr SDK
```bash
cd ~
wget https://github.com/zephyrproject-rtos/sdk-ng/releases/download/v0.16.5/zephyr-sdk-0.16.5_linux-x86_64.tar.xz
```

## 2. Extract Zephyr SDK
```bash
cd ~
tar -xf zephyr-sdk-0.16.5_linux-x86_64.tar.xz
```

## 3. Run SDK Setup Script
```bash
cd ~/zephyr-sdk-0.16.5
./setup.sh
```

## 4. Install Python Dependencies
```bash
pip3 install pyelftools
pip3 install intelhex
```

## 5. Download nRF Command Line Tools
```bash
cd /tmp
wget https://nsscprodmedia.blob.core.windows.net/prod/software-and-other-downloads/desktop-software/nrf-command-line-tools/sw/versions-10-x-x/10-24-2/nrf-command-line-tools_10.24.2_amd64.deb
```

## 6. Install nRF Command Line Tools
```bash
sudo dpkg -i /tmp/nrf-command-line-tools_10.24.2_amd64.deb
sudo apt install /opt/nrf-command-line-tools/share/JLink_Linux_V794e_x86_64.deb --fix-broken
```

## 7. Build SPM Project
```bash
export ZEPHYR_TOOLCHAIN_VARIANT=zephyr
export ZEPHYR_SDK_INSTALL_DIR=~/zephyr-sdk-0.16.5
source /home/vince/git/github.com/ncs/zephyr/zephyr-env.sh
python3 -m west build -b actinius_icarus -d build --pristine -- -G"Unix Makefiles"
```

## 8. Flash SPM to Board
```bash
export ZEPHYR_TOOLCHAIN_VARIANT=zephyr
export ZEPHYR_SDK_INSTALL_DIR=~/zephyr-sdk-0.16.5
source /home/vince/git/github.com/ncs/zephyr/zephyr-env.sh
python3 -m west flash -d build
```

## Optional: Verify Flash
```bash
python3 -m west flash -d build --verify
```

## Build Results
- Flash: 23,988 bytes / 256 KB (9.15% used)
- SRAM: 8,640 bytes / 64 KB (13.18% used)
- Board: 802005300


# Resources

[1] Testing: https://ferrous-systems.com/blog/test-embedded-app/
[2] knurling: https://github.com/knurling-rs
[3] app template: https://github.com/knurling-rs/app-template 
