# micropython_ir_camera
GY-mcu90640 st7735 128x160 esp32c3 micropython 

合宙ESP32C3  （含串口模块的）烧录固件 c3_uart.bin 

合宙ST7735 128x160 LCD  

GY-MCU90640  

### 准备

合宙ESP32C3  （含串口模块的）烧录固件 ：c3_uart.bin 

修改gy-mcu90640的波特率，默认为115200，4HZ，需要修改为460800，8HZ,且修改完断电就可以使用了。
|GY-MCU90640|合宙ESP32C3  |
|-|-|
|TX|8|
|RX|9|
|5v|5v|
|GND|GND|

执行下面代码

```
from machine import UART

u=UART(1,rx=8,tx=9,baudrate=115200,rxbuf=1544)


##修改为460800
u.write(b'\xa5\x15\x03\xbd')
# time.sleep(0.22)


##修改为8FPS
u.write(b'\xa5\x25\x04\xce')

#保存，断电重启即可，以后访问GY-MCU90640请把波特率设置为460800，预计120ms可以获得1FPS的数据，本代码中默认设置为150ms拉取一次数据。
u.write(b'\xa5\x65\x01\x0b')

```


### 使用

|GY-MCU90640|合宙ESP32C3  |合宙ST7735|
|-|-|-|
|TX|8||
|RX|9||
|5v|5v|5V|
|GND|GND|GND|
||2|sck|
||3|sda|
||10|res|
||7|cs|
||6|dc|
||11|bl(随意)|

logo.jpg 请自行生成，分辨率 87x16，若超过显示屏分辨率 会不显示，请谨慎选择分辨率。

