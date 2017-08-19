# introduction

MP3Gain analyzes and adjusts mp3 files so that they have the same volume.

MP3Gain does not just do peak normalization, as many normalizers do. Instead, it does some statistical analysis to determine 
how loud the file actually sounds to the human ear.
Also, the changes MP3Gain makes are completely lossless. There is no quality lost in the change because the program adjusts 
the mp3 file directly, without decoding and re-encoding.

http://mp3gain.sourceforge.net

# affected programs & issues 

MP3Gain - Version 1.5.2-r2

Memory Access Violation & Memory Stack Corruption  
found in:  
  
MP3Gain command line tool  

# discovery 

author: sec.9emin1@gmail.com  
discovered by: sec.9emin1@gmail.com  

The vulnerabilities were discovered using the American Fuzzy Lop (2.49b)  
http://lcamtuf.coredump.cx/afl/

# mp3gain 
## Memory Access Violation 
./mp3gain -p -r -e -x -s r mp3crash_poc
```
Program received signal SIGSEGV, Segmentation fault.
0x080698d9 in III_dequantize_sample (xr=<optimized out>, scf=0xbfff2818, gr_infos=<optimized out>, 
    sfreq=<optimized out>, part2bits=<optimized out>) at mpglibDBL/layer3.c:904
904              v = gr_infos->pow2gain[((*scf++) + (*pretab++)) << shift];
(gdb) exploitable 
Description: Access violation on source operand
Short description: SourceAv (19/22)
Hash: 53e2786f63890aa4a79b56d54ed326d8.53e2786f63890aa4a79b56d54ed326d8
Exploitability Classification: UNKNOWN
Explanation: The target crashed on an access violation at an address matching the source operand of the current instruction. 
This likely indicates a read access violation.
Other tags: AccessViolation (21/22)
(gdb) bt
#0  0x080698d9 in III_dequantize_sample (xr=<optimized out>, scf=0xbfff2818, gr_infos=<optimized out>, 
    sfreq=<optimized out>, part2bits=<optimized out>) at mpglibDBL/layer3.c:904
#1  0x08066ad6 in do_layer3 (mp=<optimized out>, pcm_point=<optimized out>) at mpglibDBL/layer3.c:1646
#2  0x08062e21 in decodeMP3 (mp=<optimized out>, in=<optimized out>, isize=<optimized out>, done=<optimized out>)
    at mpglibDBL/interface.c:643
#3  0x0804efb8 in main (argc=<optimized out>, argv=<optimized out>) at mp3gain.c:2262
```

# mp3gain 
## Memory Stack Corruption 
./mp3gain -p -r -e -x -s r mp3crash_poc2
```
Program received signal SIGSEGV, Segmentation fault.
0x08057111 in WriteMP3GainAPETag (filename=<optimized out>, info=<optimized out>, fileTags=<optimized out>, 
    saveTimeStamp=<optimized out>) at apetag.c:616
616        fseek(outputFile,fileTags->tagOffset,SEEK_SET);
(gdb) exploitable 
__main__:99: UserWarning: GDB v7.11 may not support required Python API
Description: Possible stack corruption
Short description: PossibleStackCorruption (7/22)
Hash: b5b60e68cab3fb81c1df4bea9baf53e2.d783abac785bfb7b9ba4b9010fb738ac
Exploitability Classification: EXPLOITABLE
Explanation: GDB generated an error while unwinding the stack and/or the stack contained return addresses that were not mapped 
in the inferior's process address space and/or the stack pointer is pointing to a location outside the default stack region. 
These conditions likely indicate stack corruption, which is generally considered exploitable.
Other tags: SourceAv (19/22), AccessViolation (21/22)
(gdb) bt
#0  0x08057111 in WriteMP3GainAPETag (filename=<optimized out>, info=<optimized out>, fileTags=<optimized out>, 
    saveTimeStamp=<optimized out>) at apetag.c:616
#1  0x37333630 in ?? ()
#2  0x38323134 in ?? ()
#3  0x35353837 in ?? ()
#4  0x33313138 in ?? ()
#5  0x36363633 in ?? ()
#6  0x32353233 in ?? ()
#7  0x38303939 in ?? ()
#8  0x34303931 in ?? ()
#9  0x39323032 in ?? ()
#10 0x34343431 in ?? ()
#11 0x34303631 in ?? ()
#12 0x34333339 in ?? ()
#13 0x32343333 in ?? ()
#14 0x37313733 in ?? ()
#15 0x37333632 in ?? ()
#16 0x33323432 in ?? ()
#17 0x30313337 in ?? ()
#18 0x30393837 in ?? ()
#19 0x37303535 in ?? ()
#20 0x33393132 in ?? ()
```

# progress [to be updated]

150817 - discovery, no point of contact can be found  
170817 - issue raised to mitre cve team  
180817 - issue acknowledged  

