LD = ld
OBJCOPY = objcopy
CC = cc
CFLAGS = -O2 -m16 -Wa,-32 -ffreestanding -fno-stack-protector -fno-pie

all: extboot.bin kvmvapic.bin linuxboot.bin linuxboot_dma.bin multiboot.bin

%.o: %.S
	$(CC) $(CFLAGS) -c -o $@ $<
%.o: %.c
	$(CC) $(CFLAGS) -c -o $@ $<

%.img: %.o
	$(LD) -Ttext 0 -e _start -m elf_i386 -s -o $@ $<

%.raw: %.img
	$(OBJCOPY) -O binary -j .text $< $@

%.bin: %.raw
	python ./signrom.py $< $@

clean:
	rm -f *.o *.d *.raw *.img *.bin *~

.PHONY: all clean
