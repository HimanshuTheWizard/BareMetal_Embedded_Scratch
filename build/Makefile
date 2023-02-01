CC=arm-none-eabi-gcc
MACH=cortex-m4
INC_DIR = ../Include

OUTPUT_DIR = ../Output
OUTPUT_SRC = $(OUTPUT_DIR)/Src
OUTPUT_STARTUP_SRC = $(OUTPUT_DIR)/Startup

SRC_DIR = ../Src
APPL_SRC = $(SRC_DIR)/Application
SYSCALL_SRC = $(SRC_DIR)/SysLib

STARTUP_SRC = ../Startup

CFLAGS= -c -mcpu=$(MACH) -mthumb -std=gnu11 -O0 -I$(INC_DIR)
LDFLAGS= -mcpu=$(MACH) -mthumb -mfloat-abi=soft --specs=nano.specs -T stm32_ls.ld -Wl,-Map=../Output/final.map


all:main.o led.o stm32_startup.o syscalls.o final.elf

main.o:$(APPL_SRC)/main.c
	$(CC) $(CFLAGS) -o $(OUTPUT_SRC)/$@ $^
	
led.o:$(APPL_SRC)/led.c
	$(CC) $(CFLAGS) -o $(OUTPUT_SRC)/$@ $^
	
stm32_startup.o:$(STARTUP_SRC)/stm32_startup.c
	$(CC) $(CFLAGS) -o $(OUTPUT_STARTUP_SRC)/$@ $^
	
syscalls.o:$(SYSCALL_SRC)/syscalls.c
	$(CC) $(CFLAGS) -o $(OUTPUT_SRC)/$@ $^
	
final.elf: $(OUTPUT_SRC)/main.o $(OUTPUT_SRC)/led.o $(OUTPUT_STARTUP_SRC)/stm32_startup.o $(OUTPUT_SRC)/syscalls.o
	$(CC) $(LDFLAGS) -o $(OUTPUT_DIR)/$@ $^
	
clean:
	rm -rf $(OUTPUT_SRC)/*.o $(OUTPUT_STARTUP_SRC)/*.o $(OUTPUT_DIR)/*.elf $(OUTPUT_DIR)/*.map
	