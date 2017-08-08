# introduction

CC File Transfer is free web based file transfer software built for people that need to transfer files PC to PC regularly. It helps you ashare files, photos, music and video with your friends. This file transfer program eliminates the hassles of FTP and limitations of email file transfer especially for transferring large files. The simple interface makes transferring files as easy as dragging and dropping files. It can transfer files over the Internet or LAN/home network even transfer files from Windows to Linux / Mac OS. 


http://qpdf.sourceforge.net

# affected programs & issues

QPDF - v6.0.0

STACK CORRUPTION found when executed with the following flags and via a crafted .PDF:

qpdf --stream-data=compress --object-streams=generate --encrypt test123 test123 40  -- in.pdf out.pdf

# discovery

author: sec.9emin1@gmail.com  
discovered by: sec.9emin1@gmail.com  

The vulnerabilities were discovered using the American Fuzzy Lop (2.49b)  
http://lcamtuf.coredump.cx/afl/

# qpdf gdb trace

./qpdf --stream-data=compress --object-streams=generate --encrypt test123 test123 40  -- in.pdf out.pdf
```
[Thread debugging using libthread_db enabled]
Using host libthread_db library "/lib/x86_64-linux-gnu/libthread_db.so.1".
WARNING: id:000000,sig:11,src:000010+000007,op:splice,rep:16: file is damaged
WARNING: id:000000,sig:11,src:000010+000007,op:splice,rep:16: can't find startxref
WARNING: id:000000,sig:11,src:000010+000007,op:splice,rep:16: Attempting to reconstruct cross-reference table

Program received signal SIGSEGV, Segmentation fault.
0x00007ffff7b55761 in QPDFObjectHandle::parseInternal(PointerHolder<InputSource>, std::__cxx11::basic_string<char, 
std::char_traits<char>, std::allocator<char> > const&, QPDFTokenizer&, bool&, QPDFObjectHandle::StringDecrypter*, QPDF*, bool, 
bool, bool) ()
   from /usr/lib/x86_64-linux-gnu/libqpdf.so.17
(gdb) exploitable 
Description: Possible stack corruption
Short description: PossibleStackCorruption (7/22)
Hash: b5da70c1923e3824f45ebafcfe77a71b.018fde94be00aea515ed79b00d59768a
Exploitability Classification: EXPLOITABLE
Explanation: GDB generated an error while unwinding the stack and/or the stack contained return addresses that were not mapped 
in the inferior's process address space and/or the stack pointer is pointing to a location outside the default stack region. 
These conditions likely indicate stack corruption, which is generally considered exploitable.
Other tags: DestAv (8/22), AccessViolation (21/22)
```

# progress
 
060817 - CVE Requested  
070817 - CVE Assigned
