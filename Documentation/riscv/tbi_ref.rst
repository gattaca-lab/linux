===================================
 Reference information for TBI/MTE
===================================

Alexey Baturo <baturo.alexey@gmail.com>, Apr 2020
Anatoly Parshintsev <kupokupokupopo@gmail.com>, Apr 2020

Introduction
------------

The purpose of this document is to provide a single source of references
to the existing commits dedicated to memory tagging support.
This includes MTE and TBI for ARM and ADI for SPARC.


Existing documentation
----------------------

* Documentation/sparc/adi.rst
* Documentation/arm64/tagged-address-abi.rst
* Documentation/arm64/tagged-pointers.rst
* ARM ARM (ARMv8 MTE + TBI detailed description)
* https://lazytyped.blogspot.com/2017/09/getting-started-with-adi.html
* https://lore.kernel.org/linux-arm-kernel/20200421142603.3894-1-catalin.marinas@arm.com/


Kernel code summary
-------------------

The purpose of this summary is to enumerate useful commits and provide a brief
description why these may be useful.

Date:   Fri Dec 6 14:18:01 2019
  98884281027d07b93f062b7c5e7aa01e76ba12c6 (Linus Torvalds, merge of Catalina's): Merge tag 'arm64-upstream' of git://git.kernel.org/pub/scm/linux/kernel/git/arm64/linux

Date:   Thu Dec 5 13:57:36 2019 +0000
  df325e05a682e9c624f471835c35bd3f870d5e8c (Catalin Marinas) arm64: Validate tagged addresses in access_ok() called from kernel threads

Date:   Tue Oct 15 21:04:18 2019 -0700
  597399d0cb91d049fcb78fb45c7694771b583bb7 (Will Deacon): arm64: tags: Preserve tags for addresses translated via TTBR1

Date:   Wed Sep 25 16:49:04 2019 -0700
  ce18d171cb7368557e6498a3ce111d7d3dc03e4d (Catalin Marinas): mm: untag user pointers in mmap/munmap/mremap/brk

Date:   Wed Sep 25 16:49:01 2019 -0700 (Patch series "arm64: untag user pointers passed to the kernel", v19.)
  6cf5354c1c4b74fd2e5527db084f163e9d4dae4e (Andrey Konovalov): vfio/type1: untag user pointers in vaddr_get_pfn
  78063a9dd9637c0450cf6eacc03f42eb1295917f : tee/shm: untag user pointers in tee_shm_registers
  e275faf367e3a3b9db06a71924b199f429d3d508 : media/v4l2-core: untag user pointers in videobuf_dma_contig_user_get
  4fdfae8d8f855d79b7d83fcd590b6ac7ed0099cf : drm/radeon: untag user pointers in radeon_gem_userptr_ioctl
  35f3fc87bebfb2fffc1a9cdaf661ee3f95c2a5f1 : drm/amdgpu: untag user pointers
  7d0325749a6c77b075424ab9de76bcb73a118430 : userfaultfd: untag user pointers
  ed8a66b83269c27f7181c95b477da5d33fecfbc4 : fs/namespace: untag user pointers in copy_mount_options
  5d65e7a7d8cd5c77baa1acf129a11b8b45ffee75 : mm: untag user pointers in get_vaddr_frames
  f9652594195fca8c3d8b8ee392ad0ff9f701bb20 : mm: untag user pointers in mm/gup.
  057d3389108eda8a20c7f496f011846932680d88 : mm: untag user pointers passed to memory syscalls
  903f433f8f7a33e292a319259483adece8cc6674 : lib: untag user pointers in strn*_user

Date:   Fri Aug 23 17:37:17 2019 +0100
  92af2b696119e491a95d77acdd8832b582d300d4 (Vincenzo Frascino): arm64: Relax Documentation/arm64/tagged-pointers.rst

Date:   Tue Jul 23 19:58:52 2019 +0200
  9ce1263033cd2ad393e2ff0df4a1c4ab4992c9df (Andrey Konovalov): selftests, arm64: add a selftest for passing tagged pointers to kernel

Date:   Tue Jul 23 19:58:39 2019 +0200
  63f0c60379650d82250f22e4cf4137ef3dc4f43d (Catalin Marinas): arm64: Introduce prctl() options to control the tagged user addresses ABI

Date:   Tue Jul 23 19:58:38 2019 +0200
  2b835e24b5c6f9c633ff51973581ee7ca7b3e8ec (Andrey Konovalov): arm64: untag user pointers in access_ok and __uaccess_mask_ptr

Date:   Thu Jul 11 20:59:19 2019
  6471384af2a6530696fc0203bafe4de41a23c9ef (Alexander Potapenko): mm: security: introduce init_on_alloc=1 and init_on_free=1 boot options

Date:   Thu Jul 11 20:56:41 2019 -0700
  Christoph Hellwig <hch@lst.de> (pack of 16 commits + more from others, Thu Jul 11)
  f455c854877dcce5d714b00203ea804bf601fb02 : mm: use untagged_addr() for get_user_pages_fast addresses
  26f4c328079d78d6cd0462c53c14ec0b69f4748e : mm: simplify gup_fast_permitted
  39656e83dab918861931ef96e5c41731b0899e56 : mm: lift the x86_32 PAE version of gup_get_pte to common code
  446f062bf06c81de85edd279ee179715c83a4270 : MIPS: use the generic get_user_pages_fast code
  2f85e7f948a2c9f7e1524397d1818191ff5abb03 : sh: add the missing pud_page definition
  3c9b9accad9f25a52438c790f76b08d79051d383 : sh: use the generic get_user_pages_fast code
  d85507901f6a0a4fbd04cbdd567f4798a695b6d3 : sparc64: add the missing pgd_page definition
  5875509d2f30eb8963163f255ded98095989142f : sparc64: define untagged_addr()
  7b9afb86b6328f10dc2cad9223d7def12d60e505 : sparc64: use the generic get_user_pages_fast code
  67a929e097b774c69253c8b61ef9eb8a42b463a3 : mm: rename CONFIG_HAVE_GENERIC_GUP to CONFIG_HAVE_FAST_GUP
  d3649f68b4336e7ef7aa264cf05ba1265feb0968 : mm: reorder code blocks in gup.c
  050a9adc64383aed3429a31432b4f5a7b0cdc8ac : mm: consolidate the get_user_pages* implementations
  817be129e6f254e5bd8c17b1da834c8f612dca28 : mm: validate get_user_pages_fast flags
  cbd34da7dc9afd521e0bea5e7d12701f4a9da7c7 : mm: move the powerpc hugepd code to mm/gup.c
  01a369160bbea43727aa2b99877f86ebddba9acc : mm: switch gup_hugepte to use try_get_compound_head
  520b4a4496f12b117b94f3ac7c493651881c5fe3 : mm: mark the page referenced in gup_hugepte
  aa712399c1e8245c375a5c44760de684ec2ebefb (Pingfan Liu): mm/gup: speed up check_and_migrate_cma_pages() on huge page
  b5d1c39f34d1c9bca0c4b9ae2e339fbbe264a9c7 (Andy Lutomirski): mm/gup.c: remove some BUG_ONs from get_gate_page()
  790c73690c2bbecb3f6f8becbdb11ddc9bcff8cc (Guenter Roeck): mm/gup.c: mark undo_dev_pagemap as __maybe_unused
  5fba4af4456b5d3f982d4ac1c879d16b36aaa0fb (Mike Rapoport): asm-generic, x86: introduce generic pte_{alloc,free}_one[_kernel]
  bc3ace9b520f97d5650d096a5f95cac3fa64e204 (Mike Rapoport): alpha: switch to generic version of pte allocation
  28bcf5937536062d96ee0b581a76a0b1b652eec6 (Mike Rapoport): arm: switch to generic version of pte allocation
  50f11a8a4620eee6b6831e69ab5d42456546d7d8 (Mike Rapoport): arm64: switch to generic version of pte allocation
  bd5ff066514c2dcffd443cfaa55580db0f19caf8 (Mike Rapoport): csky: switch to generic version of pte allocation
  14c0a39c9af9a25e0f94f9be89431c2debb34f2c (Mike Rapoport): m68k: sun3: switch to generic version of pte allocation
  b7902ce175476b767e6c614fded293faf906deee (Mike Rapoport): mips: switch to generic version of pte allocation
  f52a8e1a67cde67c33d5c2eabd6494dcab956677 (Mike Rapoport): nds32: switch to generic version of pte allocation
  fc7835c2f8ea800ded22f68bd782cd17a6dd83cd (Mike Rapoport): nios2: switch to generic version of pte allocation
  3f4a13085dd88cb806a2c64fb1286e9cf3a98cd0 (Mike Rapoport): parisc: switch to generic version of pte allocation
  d1b46fe50c8b0e0b4035c48ccd5f655aa7ceea16 (Mike Rapoport): riscv: switch to generic version of pte allocation
  f32848e16939e1407ad3413f7faa3e0a8ad802eb (Mike Rapoport): um: switch to generic version of pte allocation
  c2471e79a7ea0f48e3ae9253e1f3688a44cc944d (Mike Rapoport): unicore32: switch to generic version of pte allocation
  8b1e0f81fb6fcf3109465a168b2e2da3f711fa86 (Anshuman Khandual): mm/pgtable: drop pgtable_t variable from pte_fn_t functions

Date:   Wed May 3 16:37:47 2017 +0100
  276e93279a630657fff4b086ba14c95955912dfa (Kristina Martsenko): arm64: entry: improve data abort handling of tagged pointers
  7dcd9dd8cebe9fa626af7e2358d03a37041a70fb (Kristina Martsenko): aarm64: hw_breakpoint: fix watchpoint matching for tagged pointers
  81cddd65b5c82758ea5571a25e31ff6f1f89ff02 (Kristina Martsenko): aarm64: traps: fix userspace cache maintenance emulation on a tagged pointer

