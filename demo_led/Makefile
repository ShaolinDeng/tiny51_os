CC	= sdcc --debug

all:clean demo_led.hex

flash:clean demo_led.hex
	stcgal -p /dev/tty.usbserial-1410 demo_led.hex

demo_led.hex:demo_led.ihx
	packihx demo_led.ihx > demo_led.hex

demo_led.ihx:demo_led.c task_scheduling_core.rel platform_interface.rel lcd1602.rel
	$(CC) demo_led.c task_scheduling_core.rel platform_interface.rel lcd1602.rel

task_scheduling_core.rel:../task_scheduling_core/task_scheduling_core.c
	$(CC) -c ../task_scheduling_core/task_scheduling_core.c

platform_interface.rel:../chip_platform/platform_interface.c
	$(CC) -c ../chip_platform/platform_interface.c

lcd1602.rel:../drivers/lcd1602.c
	$(CC) -c ../drivers/lcd1602.c

.PHONY:clean
clean:
	rm -rf *.bin *.hex *.asm *.ihx *.lk *.lst *.map *.mem *.rel *.rst *.sym *.adb *.omf *.cdb
