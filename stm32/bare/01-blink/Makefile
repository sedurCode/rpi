CC = arm-none-eabi-gcc
LD = arm-none-eabi-ld
BIN = arm-none-eabi-objcopy
STL = st-flash
CFLAGS = -mthumb -mcpu=cortex-m3 
#CFLAGS += -ggdb -O0 
CFLAGS += -nostdlib
CFLAGS += -I..
#CFLAGS = -mthumb -mcpu=cortex-m3 -ggdb -O0 -nostdlib --specs=nano.specs
LDFLAGS = -L.. -T linker.ld

all: app.bin 

main.o: main.c
	$(CC) $(CFLAGS) -c -o main.o main.c

app.elf: main.o 
	$(LD) $(LDFLAGS) -o app.elf main.o  -lblue

app.bin: app.elf
	$(BIN) -O binary app.elf app.bin
	arm-none-eabi-objdump -d app.elf >app.txt

clean:
	rm -f *.o *.elf *.bin app.txt

.flash: app.bin
	touch .flash

flash : .flash
	$(STL) write app.bin 0x8000000

erase:
	$(STL) erase

dump:
	arm-none-eabi-objdump -d app.elf
