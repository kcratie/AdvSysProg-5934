# Comment/uncomment the following line to disable/enable debugging
DEBUG = y


# Add your debugging flag (or not) to ccflags-y
ifeq ($(DEBUG),y)
  DEBFLAGS = -O -g -Dhw3_DEBUG # "-O" is needed to expand inlines
else
  DEBFLAGS = -O2
endif

ccflags-y += $(DEBFLAGS)
ccflags-y += -I$(LDDINC)

ifneq ($(KERNELRELEASE),)
# call from kernel build system

#hw3-objs := hw3.o

obj-m	:= hw3.o

else

KERNELDIR ?= /lib/modules/$(shell uname -r)/build
PWD       := $(shell pwd)

modules:
	$(MAKE) -C $(KERNELDIR) M=$(PWD) LDDINC=$(PWD)/../include modules

endif



clean:
	rm -rf *.o *~ core .depend .*.cmd *.ko *.mod.c .tmp_versions

depend .depend dep:
	$(CC) $(ccflags-y) -M *.c > .depend


ifeq (.depend,$(wildcard .depend))
include .depend
endif
