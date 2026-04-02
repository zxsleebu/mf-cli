obj-m += minifuse_mod.o

# Find the build directory for the currently running kernel
KDIR ?= /lib/modules/$(shell uname -r)/build

IS_LLVM := $(shell grep -q "CONFIG_CC_IS_CLANG=y" $(KDIR)/.config && echo 1 || echo 0)

ifeq ($(IS_LLVM), 1)
    KBUILD_FLAGS := LLVM=1 CC=clang
else
    KBUILD_FLAGS :=
endif

all:
	$(MAKE) $(KBUILD_FLAGS) -C $(KDIR) M=$(PWD) modules

clean:
	$(MAKE) $(KBUILD_FLAGS) -C $(KDIR) M=$(PWD) clean

# Optional helper targets for users
install: all
	install -D -m 644 minifuse_mod.ko /usr/lib/modules/$(shell uname -r)/extra/minifuse_mod.ko
	depmod -a

uninstall:
	rm -f /usr/lib/modules/$(shell uname -r)/extra/minifuse_mod.ko
	depmod -a
