#check if this makefile is being processed from kbuild
ifeq ($(KERNELRELEASE),)

KERNEL_DIR ?= /lib/modules/$(shell uname -r)/build

all: 
	make -C ${KERNEL_DIR} M=$$PWD;

modules:
	make -C ${KERNEL_DIR} M=$$PWD $@;

modules_install:
	make -C ${KERNEL_DIR} M=$$PWD $@;

modules_clean:
	make -C ${KERNEL_DIR} M=$$PWD $@;

clean:
	rm -f *.o *~ *.ko *.mod.c Module.markers modules.order Module.symvers 

lib%.so: lib%.o
	$(CC) $(CFLAGS) -shared -o $@ $^;

lib%.o: lib%.c
	$(CC) $(CFLAGS) -fPIC -O2 -Wall -D_INIT=lib$*_init -c -o $@ $<;

install: modules_install 
	mkdir -p $(DESTDIR)/lib/xtables/
	cp  $(DESTDIR)/lib/xtables/

distdir:

distclean: clean

else
#kbuild variables for xtables coova module
obj-m += xt_coova.o
endif
