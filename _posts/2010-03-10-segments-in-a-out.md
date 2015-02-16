---
layout: post
title: Segments in a.out
date: 2010-03-10 23:09:00.000000000 -08:00
categories: []
tags: []
status: publish
type: post
published: true

---
<p><span style="  ;font-family:'Times New Roman';font-size:medium;">
<div style="background-image: initial; background-attachment: initial; background-origin: initial; background-clip: initial; background-color: rgb(255, 255, 255); font: normal normal normal 13px/19px Georgia, 'Times New Roman', 'Bitstream Charter', Times, serif; padding-top: 0.6em; padding-right: 0.6em; padding-bottom: 0.6em; padding-left: 0.6em; margin-top: 0px; margin-right: 0px; margin-bottom: 0px; margin-left: 0px; background-position: initial initial; background-repeat: initial initial; ">
<div style="text-align: justify;">Ever wondered whenever you compile a C code, what the hell is written in the object .out file. Well, lets dig into the object file and see what it contains.</div>
<div></div>
<div style="text-align: justify;"></div>
<div style="text-align: justify;">Now whenever you write a C code, it basically contains the code (functions etc) which you want to execute and the data (global, local etc) on which you are executing those functions. So what the compiler (and linker) does is (in reality, it does hell lot of stuff but just to make things simple-), it takes the code and the data and put them into segments.</div>
<div></div>
<div style="text-align: justify;"></div>
<div style="text-align: justify;">Various Segments in object file a.out:</div>
<div></div>
<div style="text-align: justify;"><span mce_name="strong" mce_style="font-weight: bold;" style="font-weight: bold; "><br /></span></div>
<div style="text-align: justify;"><span mce_name="strong" mce_style="font-weight: bold;" style="font-weight: bold; ">Note: These segments are not the one used in the hardware, these are simply part of an object file.</span></div>
<div style="text-align: justify;"><span mce_name="strong" mce_style="font-weight: bold;" style="font-weight: bold; "><br /></span></div>
<div></div>
<div style="text-align: justify;"><span mce_name="strong" mce_style="font-weight: bold;" style="font-weight: bold; ">Data segment</span> : contains the global and static variables which are initialized.</div>
<div style="text-align: justify;"><span mce_name="strong" mce_style="font-weight: bold;" style="font-weight: bold; ">BSS segment </span>: contains the global and static variables which are not initialized.</div>
<div style="text-align: justify;"><span mce_name="strong" mce_style="font-weight: bold;" style="font-weight: bold; ">Text segment</span> : Contains the code</div>
<div></div>
<div style="text-align: justify;"></div>
<div style="text-align: justify;">The main importance of dividing the binary file into these segments is that the loader just need to take these segments and map it in memory.</div>
<div></div>
<div style="text-align: justify;"><span mce_name="strong" mce_style="font-weight: bold;" style="font-weight: bold; "><br /></span></div>
<div style="text-align: justify;"><span mce_name="strong" mce_style="font-weight: bold;" style="font-weight: bold; ">BSS</span>: This segment in the object file actually do not contain anything except the size of the BSS segment needed as the variables are still initialized so no need to mirror those variables in the segment. This size value will be later used by the loader to reserve that much amount of memory for the segment.</div>
<div></div>
<div style="text-align: justify;"><span mce_name="strong" mce_style="font-weight: bold;" style="font-weight: bold; "><br /></span></div>
<div style="text-align: justify;"><span mce_name="strong" mce_style="font-weight: bold;" style="font-weight: bold; ">How segments are laid out in memory::</span></div>
<div style="text-align: justify;">The segments conveniently map into objects that the runtime linker can load directly! The loader just takes each segment image in the file and puts it directly into memory. The segments essentially become memory areas of an executing program, each with a dedicated purpose.</div>
<div></div>
<div style="text-align: justify;"></div>
<div style="text-align: justify;">The <span mce_name="strong" mce_style="font-weight: bold;" style="font-weight: bold; ">text segment</span> contains the program instructions. The loader copies that directly from the file into memory (typically with the mmap() system call), and need never worry about it again, as program text typically never changes in value nor size. Some operating systems and linkers can even assign appropriate permissions to the different sections in segments, for example, text can be made read-andexecute-only, some data can be made read-write-no-execute, other data made read-only, and so on. </div>
<div style="text-align: justify;"></div>
<div style="text-align: justify;">The <b>data segment</b> contains the initialized global and static variables, complete with their assigned values.</div>
<div></div>
<div style="text-align: justify;"></div>
<div style="text-align: justify;">The size of the <b>BSS segment</b> is then obtained from the executable, and the loader obtains a block of this size, putting it right after the data segment. This block is zeroed out as it is put in the program's address space. The entire stretch of data and BSS is usually just referred to jointly as the data segment at this point. This is because a segment, in OS memory management terms, is simply a range of consecutive virtual addresses, so adjacent segments are coalesced. The data segment is typically the largest segment in any process.</div>
<div></div>
<div style="text-align: justify;"></div>
<div style="text-align: justify;">We still need some memory space for <b>local variables</b>, temporaries, parameter passing in function calls, and the like. A <b>stack segment</b> is allocated for this. We also need heap space for dynamically allocated memory. This will be set up on demand, as soon as the first call to malloc() is made.</div>
<div></div>
<div style="text-align: justify;"><span mce_name="strong" mce_style="font-weight: bold;" style="font-weight: bold; "><br /></span></div>
<div style="text-align: justify;"><span mce_name="strong" mce_style="font-weight: bold;" style="font-weight: bold; ">Note</span> that the lowest part of the virtual address space is unmapped; that is, it is within the address space of the process, but has not been assigned to a physical address, so any references to it will be illegal. This is typically a few Kbytes of memory from address zero up. It catches references through null pointers, and pointers that have small integer values.</div>
</div>
<p></span></p>
