---
layout: post
title: How to compile Linux kernel on Ubuntu?
date: 2010-05-20 07:18:00.000000000 -07:00
categories: []
tags: []
status: publish
type: post
published: true

---
<div style="margin-bottom: 0in;"><span style="font-family: Arial; font-size: small;"><span style="font-size: 13px;">Following are the steps to compile a kernel source code on ubuntu-</span></span> </div>
<div style="margin-bottom: 0in;"></div>
<div style="margin-bottom: 0in;"><b>Steps:</b></div>
<div style="margin-bottom: 0in;"></div>
<ol>
<li>
<div style="margin-bottom: 0in;"><b>Change to root : </b><i>su</i></div>
</li>
</ol>
<div style="margin-bottom: 0in; margin-left: 0.25in;"></div>
<ol start="2">
<li>
<div style="margin-bottom: 0in;"><b>Update the package manager :  </b><i>apt-get update</i></div>
</li>
</ol>
<div style="margin-bottom: 0in;"></div>
<ol start="3">
<li>
<div style="margin-bottom: 0in;"><b>Get new make utility : </b><i>apt-get  install build-essential</i></div>
</li>
</ol>
<div style="margin-bottom: 0in;"></div>
<ol start="4">
<li>
<div style="margin-bottom: 0in;"><span style="color: red;"><b>Optional  -</b></span><b> To create dep :</b><span style="color: black;"><i> apt-get  install kernel-package libncurses5-dev fakeroot wget bzip2</i></span></div>
</li>
</ol>
<div style="margin-bottom: 0in; margin-left: 0.25in;"></div>
<ol start="5">
<li>
<div style="margin-bottom: 0in;"><b>Download linux source : </b><span style="color: black;"><i>cd  /usr/src</i></span></div>
</li>
</ol>
<div style="margin-bottom: 0in; margin-left: 0.5in;"><span style="color: black;"><i><br /></i></span><span style="color: black;"><i>wget </i></span><span style="color: blue;"><u><a href="http://www.kernel.org/pub/linux/kernel/v2.6/linux-2.6.18.1.tar.bz2"><i>http://www.kernel.org/pub/linux/kernel/v2.6/linux-2.6.18.1.tar.bz2</i></a></u></span></div>
<div style="margin-bottom: 0in; margin-left: 0.5in;"></div>
<div style="margin-bottom: 0in; margin-left: 0.5in;"><b>Download patches: </b>v2.6/testing/patch-2.6.27-rc1.bz2</div>
<div style="margin-bottom: 0in; margin-left: 0.5in;"><b>             </b>2.6.27-rc1-mm.bz2 </div>
<div style="margin-bottom: 0in; margin-left: 0.5in;"></div>
<ol start="6">
<li>
<div style="margin-bottom: 0in;"><b>Then we unpack the kernel  sources and create a symlink linux to the kernel sources directory</b>:</div>
</li>
</ol>
<div style="margin-bottom: 0in; margin-left: 0.5in;"></div>
<div style="margin-bottom: 0in; margin-left: 0.5in;"><span style="color: black;"><span lang="pt-BR"><i>tar x</i></span></span><span style="color: black;"><span lang="pt-BR"><i>vjf linux-2.6.18.1.tar.bz2</i></span></span></div>
<div style="margin-bottom: 0in; margin-left: 0.5in;"><span style="color: black;"><i>ln -s linux-2.6.18.1 linux</i></span></div>
<div style="margin-bottom: 0in; margin-left: 0.5in;"><span style="color: black;"><i>cd /usr/src/linux</i></span></div>
<div style="margin-bottom: 0in; margin-left: 0.5in;"></div>
<div style="margin-bottom: 0in; margin-left: 0.5in;"></div>
<ol start="7">
<li>
<div style="margin-bottom: 0in;"><span style="color: black;"><b>Apply  patches:</b></span></div>
</li>
</ol>
<div style="margin-bottom: 0in; margin-left: 0.5in;"><span style="color: black;"><i>bzip2 -dc </i></span><b>patch-2.6.27-rc1.bz2</b><span style="color: black;"><i> | patch -p1</i></span><span style="color: black;"><i>&nbsp;</i></span></div>
<div style="margin-bottom: 0in; margin-left: 0.5in;"><span style="color: black;"><i>bzip2 -dc </i></span><b>2.6.27-rc1-mm.bz2</b><span style="color: black;"><i> | patch -p1</i></span><span style="color: black;"><i>&nbsp;</i></span></div>
<div style="margin-bottom: 0in; margin-left: 0.5in;"></div>
<ol start="8">
<li>
<div style="margin-bottom: 0in;"><span style="color: black;"><b>Execute :</b></span><span style="color: black;">  </span><span style="color: black;"><i>make clean</i></span></div>
</li>
</ol>
<div style="margin-bottom: 0in;"><span style="color: black;">      </span><span style="color: black;"><i>make mrproper</i></span></div>
<div style="margin-bottom: 0in; margin-left: 0.5in;"></div>
<ol start="9">
<li>
<div style="margin-bottom: 0in;"><b>Configure kernel:</b></div>
</li>
</ol>
<div style="margin-bottom: 0in; margin-left: 0.5in;"><b> Copy already existing config file:</b></div>
<div style="margin-bottom: 0in; margin-left: 0.5in; text-indent: 0.5in;">  <span style="color: black;"><i>cp /boot/config-`uname -r` ./.config</i></span></div>
<div style="margin-bottom: 0in; margin-left: 0.5in; text-indent: 0.5in;"></div>
<div style="margin-bottom: 0in; margin-left: 0.5in; text-indent: 0.5in;"> <b>make menuconfig</b></div>
<div style="margin-bottom: 0in; margin-left: 1.5in;"><b>Go to Load an Alternate config file. Enter .config and enter.  Exit</b></div>
<div style="margin-bottom: 0in; margin-left: 1.5in;"></div>
<div style="margin-bottom: 0in; margin-left: 0.5in;"></div>
<ol start="10">
<li>
<div style="margin-bottom: 0in;"><b>Make kernel: </b><i>make &amp;&amp;  make modules_ install &amp;&amp; make install</i></div>
</li>
</ol>
<div style="margin-bottom: 0in; margin-left: 0.25in;"></div>
<div style="margin-bottom: 0in; margin-left: 0.5in;"><b>Check if depmod is already not done.</b></div>
<div style="margin-bottom: 0in; margin-left: 0.5in;"> <b>If not done then type:</b> <i>depmod 2.6.27-rc1-mm</i></div>
<div style="margin-bottom: 0in; margin-left: 0.5in;"></div>
<div style="margin-bottom: 0in; margin-left: 0.5in;"></div>
<ol start="11">
<li>
<div style="margin-bottom: 0in;"><b>To use initrd then get yaird:</b></div>
</li>
</ol>
<div style="margin-bottom: 0in; margin-left: 0.5in; text-indent: 0.5in;"> <i>apt-get install yaird</i></div>
<div style="margin-bottom: 0in;"></div>
<ol start="12">
<li>
<div style="margin-bottom: 0in;"><b>Execute:</b></div>
</li>
</ol>
<div style="margin-bottom: 0in;"> <i>mkinitrd.yaird –o /boot/initrd.img-2.6.27-rc1-mm1 2.6.27-rc1-mm1</i></div>
<div style="margin-bottom: 0in;"></div>
<div style="margin-bottom: 0in;"> If this doesn’t work then execute:</div>
<div style="margin-bottom: 0in;">  <span style="color: #303030;"><i>mkinitramfs </i></span><i>–o /boot/initrd.img-2.6.27-rc1-mm1 2.6.27-rc1-mm1</i></div>
<div style="margin-bottom: 0in;"></div>
<div style="margin-bottom: 0in;"> Update grub (/boot/grub/menu.lst):<i> update-grub</i></div>
<div style="margin-bottom: 0in;">  Check the menu.lst file and see the entry of new kernel</div>
<div style="margin-bottom: 0in;"></div>
<ol start="13">
<li>
<div style="margin-bottom: 0in;"><b>Reboot</b></div>
</li>
</ol>
