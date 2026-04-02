obj-m += minifuse_mod.o

all:
	make LLVM=1 CC=clang -C /lib/modules/$(shell uname -r)/build M=$(PWD) modules

clean:
	make LLVM=1 CC=clang -C /lib/modules/$(shell uname -r)/build M=$(PWD) clean
