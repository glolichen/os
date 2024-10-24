# LiOS

An experimental x86_64 operating system written from scratch in C.

## Currently Implemented

 * Bootstrapping to long mode
 * Interrupts (only keyboard implemented)
 * Printing to VGA (text mode only) and serial
 * Some basic memory management
   * Uses paging (obviously)
   * Linked list based page frame and virtual address allocator
   * Kernel heap allocator (using linked lists and bitmap)

## To Do

 * Support UEFI. Move away from VGA text mode. Instead draw each pixel manually... how amazing
 * Virtual address allocator can only use 1 4KiB page, which is only 128 linked list nodes. So if the memory gets too fragmented the allocator will completely break.
 * Filesystem and hard disk/solid state drive driver
 * Processes
 * ELF program loading and userspace programs
 * Userspace shell program

## Memory Layout

Sort of based on Linux.
 * 0xFFFFFFFF80000000-0xFFFFFFFFFFFFFFFF (highest 2GiB) is directly mapped to the first 2GiB of physical memory. Paging structures, and also DMA structures sometime in the future, are stored here.
 * 0xFFFFF00000000000-0xFFFFFFFF80000000 are used for other pieces of kernel memory. Page frames come from the rest of physical memory, outside of the first 2GiB. User page frames also come from here.
 * 0xFFFF800000000000-0xFFFFF00000000000 reserved for VGA frame buffer virtual address
 * Lower-half virtual memory for user processes.

## Sources

 * [OSDev Wiki](https://wiki.osdev.org)
 * [OSTEP book](https://pages.cs.wisc.edu/~remzi/OSTEP/)
 * [Intel](https://www.intel.com/content/www/us/en/developer/articles/technical/intel-sdm.html) and [AMD](https://www.amd.com/content/dam/amd/en/documents/processor-tech-docs/programmer-references/40332.pdf) manuals
 * [QEMU docs](https://www.qemu.org/docs/master/index.html)

(write bootable usb: `sudo dd if=iso/os.iso of=/dev/sda`)
