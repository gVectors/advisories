# introduction

MP3Gain analyzes and adjusts mp3 files so that they have the same volume.

MP3Gain does not just do peak normalization, as many normalizers do. Instead, it does some statistical analysis to determine 
how loud the file actually sounds to the human ear.
Also, the changes MP3Gain makes are completely lossless. There is no quality lost in the change because the program adjusts 
the mp3 file directly, without decoding and re-encoding.

http://mp3gain.sourceforge.net

# affected programs & issues [to be updated]

MP3Gain - Version 1.5.2-r2

NULL Pointer Dereferences SEGFAULTS found in:  
  
mp4dump	- displays the entire atom/box structure of an MP4 file  
mp4encrypt - encrypts an MP4 file (multiple encryption schemes are supported)  
mp42ts - converts an MP4 file to an MPEG2-TS file.

# discovery [to be updated]

author: sec.9emin1@gmail.com  
discovered by: sec.9emin1@gmail.com  

The vulnerabilities were discovered using the American Fuzzy Lop (2.49b)  
http://lcamtuf.coredump.cx/afl/

# mp4dump [to be updated]
./mp4dump --format json mp4dump_poc
```
Program received signal SIGSEGV, Segmentation fault.
0x0000000000406e3f in AP4_AvccAtom::InspectFields(AP4_AtomInspector&) ()
(gdb) exploitable 
__main__:99: UserWarning: GDB v7.11 may not support required Python API
Description: Access violation near NULL on source operand
Short description: SourceAvNearNull (16/22)
Hash: 4504b8474090b84917f7bf9eaaf2a8ae.aa20c4da10ac89e4bfce72be5b05d8c5
Exploitability Classification: PROBABLY_NOT_EXPLOITABLE
Explanation: The target crashed on an access violation at an address matching the source operand of the current instruction. 
This likely indicates a read access violation, which may mean the application crashed on a simple NULL dereference to data 
structure that has no immediate effect on control of the processor.
Other tags: AccessViolation (21/22)
(gdb) bt
#0  0x0000000000406e3f in AP4_AvccAtom::InspectFields(AP4_AtomInspector&) ()
#1  0x000000000040228f in AP4_Atom::Inspect(AP4_AtomInspector&) ()
#2  0x000000000040a744 in AP4_AtomListInspector::Action(AP4_Atom*) const ()
#3  0x0000000000424a25 in AP4_SampleEntry::Inspect(AP4_AtomInspector&) ()
#4  0x000000000040a744 in AP4_AtomListInspector::Action(AP4_Atom*) const ()
#5  0x000000000042b965 in AP4_StsdAtom::InspectFields(AP4_AtomInspector&) ()
#6  0x000000000040228f in AP4_Atom::Inspect(AP4_AtomInspector&) ()
#7  0x000000000040164b in main ()
```

# progress [to be updated]

280717 - issue raised and vendor replied  
290717 - issue acknowledged and confirmation of fixing it in next release

