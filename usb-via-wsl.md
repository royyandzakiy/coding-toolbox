```bash
# in windows
usbipd list
usbipd attach --wsl --busid 5-3 # will remove device from windows
usbipd detach --busid 5-3

# in linux
lsusb
ls /dev/ttyACM*
minicom -D /dev/ttyACM0 -b 115200
```

```bash
# before attach (windows)
C:\Users\royya>usbipd list
Connected:
BUSID  VID:PID    DEVICE                                                        STATE
1-6    046d:c08b  G502 HERO, USB Input Device, Virtual HID Framework (VHF) ...  Not shared
1-8    3277:0029  USB2.0 HD UVC WebCam                                          Not shared
1-14   8087:0026  Intel(R) Wireless Bluetooth(R)                                Not shared
5-3    1366:1061  JLink CDC UART Port (COM10), JLink CDC UART Port (COM11),...  Not shared

# after attach (linux)
royya@tuff16:~/project-coding/iot/zephyr-ztest-emul-button-hal$ ls /dev/ttyACM*
/dev/ttyACM0  /dev/ttyACM1

royya@tuff16:~/project-coding/iot/zephyr-ztest-emul-button-hal$ lsusb
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 001 Device 005: ID 1366:1061 SEGGER J-Link # this shows up
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
```