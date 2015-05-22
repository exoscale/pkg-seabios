LD = ld
OBJCOPY = objcopy
CC = cc

all: $(subst .S,.bin,$(wildcard *.S))

%.o: %.S
	$(CC) -c -o $@ $<

%.img: %.o
	$(LD) -Ttext 0 -e _start -s -o $@ $<

%.raw: %.img
	$(OBJCOPY) -O binary -j .text $< $@

%.bin: %.raw
	python ./signrom.py $< $@

clean:
	rm -f *.o *.d *.raw *.img *.bin *~

.PHONY: all clean
