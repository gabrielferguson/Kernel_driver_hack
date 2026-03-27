# 如果 KERNELRELEASE 已经定义，说明这是从内核的 Makefile 调用的
ifneq ($(KERNELRELEASE),)
	obj-m += my_driver.o
	my_driver-objs := memory.o process.o hide_proc.o hide_kill.o entry.o anti_ptrace_detection.o cvector.o thread.o single_step.o spawn_suspend.o register.o mmu_breakpoint.o syscall_trace.o touch_input.o touch_injector.o mmap_hijack.o vma_less.o hw_breakpoint.o

	EXTRA_CFLAGS += -O2 -Wno-error=incompatible-pointer-types -Wno-error=unused-function
	my_driver-objs += inline_hook/p_lkrg_main.o
	my_driver-objs += inline_hook/p_hmem.o
	my_driver-objs += inline_hook/p_hook.o
	my_driver-objs += inline_hook/utils/p_memory.o
	my_driver-objs += inline_hook/p_transit_stubs.o
else
# 否则，这是从命令行直接调用的
	KDIR ?= /lib/modules/$(shell uname -r)/build
	PWD := $(shell pwd)

all:
	$(MAKE) -C $(KDIR) M=$(PWD) modules

clean:
	$(MAKE) -C $(KDIR) M=$(PWD) clean
endif
