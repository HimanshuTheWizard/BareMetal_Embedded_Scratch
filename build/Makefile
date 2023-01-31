CC=arm-none-eabi-gcc
MACH=cortex-m4
INC_DIR = ../Include

CFLAGS= -c -mcpu=$(MACH) -mthumb -std=gnu11 -O0 -I$(INC_DIR)
LDFLAGS= -mcpu=$(MACH) -mthumb -mfloat-abi=soft --specs=nano.specs -T stm32_ls.ld -Wl,-Map=../Output/final.map


all:main.o led.o stm32_startup.o final.elf syscalls.o

main.o:../Src/Application/main.c
	$(CC) $(CFLAGS) -o ../Output/Src/$@ $^
	
led.o:../Src/Application/led.c
	$(CC) $(CFLAGS) -o ../Output/Src/$@ $^
	
stm32_startup.o:../Startup/stm32_startup.c
	$(CC) $(CFLAGS) -o ../Output/Startup/$@ $^
	
syscalls.o:../Src/SysLib/syscalls.c
	$(CC) $(CFLAGS) -o ../Output/Src/$@ $^
	
final.elf: ../Output/Src/main.o ../Output/Src/led.o ../Output/Startup/stm32_startup.o ../Output/Src/syscalls.o
	$(CC) $(LDFLAGS) -o ../Output/$@ $^
	
clean:
	rm -rf *.o *.elf *.map
	
load:
	openocd -f share/openocd/scripts/board/stm32f4discovery.cfg