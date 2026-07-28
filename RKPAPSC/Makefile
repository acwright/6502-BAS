TARGET = RKPAPSC
EIGHTTHREE = RKPAPSC

.PHONY: all clean

all: build cf

build: $(TARGET).txt
	bastok $(TARGET).txt

view:
	hexdump -C $(TARGET).prg

cf:
	cffs create $(TARGET).img --size 1M
	cffs add $(TARGET).img $(TARGET).prg --name $(EIGHTTHREE).PRG

clean:
	rm -f $(TARGET).prg
	rm -f $(TARGET).img
