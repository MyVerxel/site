---
title: "ESP"
date: 1400-010-21T10:57:27
draft: true
---

منبع:
[SOURCE](https://docs.espressif.com/projects/esp8266-rtos-sdk/en/latest/get-started/index.html)

## Setup Toolchain :

 - [install tool chin](https://docs.espressif.com/projects/esp8266-rtos-sdk/en/latest/get-started/linux-setup.html)

linux :
 
```python
sudo apt-get install gcc git wget make libncurses-dev flex bison gperf python python-serial
```

```python
wget https://dl.espressif.com/dl/xtensa-lx106-elf-gcc8_4_0-esp-2020r3-linux-amd64.tar.gz
mkdir -p esp
cd esp
tar -xzf Downloads/xtensa-lx106-elf-linux64-1.22.0-100-ge567ec7-5.2.0.tar.gz

#/home/ali/Desktop/esp/xtensa-lx106-elf/xtensa-lx106-elf/bin
# add to .bashrc
PATH=$PATH:/home/ali/Desktop/esp/xtensa-lx106-elf/xtensa-lx106-elf/bin
alias get_lx106='export PATH="$PATH:/home/ali/Desktop/esp/xtensa-lx106-elf/xtensa-lx106-elf/bin"'
```

set permition:

```python
sudo usermod -a -G dialout $USER
sudo chmod -R 777 /dev/ttyUSB0
```

## GET SDK

 - [Get ESP8266_RTOS_SDK](https://docs.espressif.com/projects/esp8266-rtos-sdk/en/latest/get-started/index.html#get-esp8266-rtos-sdk)

```python
cd esp
git clone --recursive https://github.com/espressif/ESP8266_RTOS_SDK.git
```

