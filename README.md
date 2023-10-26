# tiny51_os
## 编译器安装
- sudo apt-get install sdcc
- sdcc 在各种平台上都有，所以这部分真的是超级爽的。

## 使用帮助
因为我是用Mac上开发的，所以可以看看我的这篇文章

https://mp.weixin.qq.com/s/ZzN3_c5IVqDCRGJhWJxMzw

## 烧录
可以直接使用make flash进行烧录，但是要指定下自己的串口

# 例子

## demo_led



```shell
cd demo_led
make flash
```

提示 根据时间的串口 修改Makefile 中 -p 
```shell 
ls /dev/tty.usb*           
      /dev/tty.usbserial-1410
```

[编译烧录](doc/demo_led.jpg)


# 基础技术讲解
当我们使用12MHZ的晶振时，单片机的机器周期是1us，对于机器周期，我们把它看成单片机里的最小时间单位。
1ms/1us=1000，也就是要计数1000个数，故T0初值=65535-1000+1（因为计数器在65536时才算溢出）=64536。
转换成16进制就是0xFC18，高八位0xFC，低八位0x18分别赋值。然后，1s=1000ms，只要加一个程序内部的自增变量（interrupt_cnt），每溢出一次自加1，当该变量加到了1000时，就代表经过了一秒钟了
