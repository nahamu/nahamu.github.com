---
layout: post
title: Serving SmartOS from your PXE server
---

# {{ page.title }}
<p class="meta">2011-08-17</p>
(Quick and Dirty Edition)

## Assumptions
 1. This guide assumes that you already have a PXE (TFTP) server set up.
 1. This guide assumes that you use [pxelinux](http://syslinux.zytor.com/wiki/index.php/PXELINUX)
 1. This guide assumes that you only want to boot SmartOS.  Please adjust accordingly.
 1. This guide assumes that you know how to do all sorts of other things as well...

## Instructions
 1. Download the ISO from [smartos.org](http://smartos.org/)
 1. Extract the entire `platform` subtree from the ISO.
 1. Download a tarball of [SYSLINUX](http://syslinux.zytor.com/wiki/index.php/Download) and get the `mboot.c32` binary out of it.
 1. In the tftp root directory, create a directory named <code>smartos</code>
 1. Copy the `platform` directory you got from the ISO into the `smartos` directory
 1. Copy the `mboot.c32` binary into the `smartos` directory
 1. Update your `pxelinux.cfg/default` file with this content:
 <pre>
default smartos
prompt 1
timeout 50
label smartos
kernel smartos/mboot.c32
append smartos/platform/i86pc/kernel/amd64/unix -B console=text,standalone=true,noimport=true,root_shadow='$5$2HOHRnK3$NvLlm.1KQBbB0WjoP7xcIwGnllhzp2HnT.mDO7DpxYA' --- smartos/platform/i86pc/amd64/boot_archive
</pre>

##References
 1. [Ryan's Guide to a disk install of SmartOS](http://www.ryan.net/smartos-disk-blogpost/real_disk_smartos.html)
 1. [mboot.c32 documentation](http://syslinux.zytor.com/wiki/index.php/Mboot.c32)
