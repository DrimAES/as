# Makefile for mini3 study
# http://wiki.minix3.org/doku.php?id=developersguide:crosscompiling
# http://www.minix3.org/docs/Implementing.MINIX.On.The.Single.Chip.Cloud.Computer.pdf

ARCH ?= i386

default:all

$(CURDIR)/minix:
	@(git clone https://github.com/Stichting-MINIX-Research-Foundation/minix.git)
	@(cp -v $(CURDIR)/minix/etc/mk.conf /etc)

all:$(CURDIR)/minix
ifeq ($(ARCH), i386)
	@(cd minix && bash ./releasetools/x86_hdimage.sh)
endif
ifeq ($(ARCH), arm)
	@(cd minix && bash ./releasetools/arm_sdimage.sh)
endif

# modify minix boot menu in the releasetools/*image.sh, change the "default" one to the one with console=tty00
run:
ifeq ($(ARCH), i386)
	echo telnet 127.0.0.1 1103
	qemu-system-i386 -m 256 -hda minix/minix_x86.img -serial tcp:127.0.0.1:1103,server
endif
