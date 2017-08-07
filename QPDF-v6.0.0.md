# introduction

QPDF is a command-line program that does structural, content-preserving transformations on PDF files. It could have been 
called something like pdf-to-pdf. It also provides many useful capabilities to developers of PDF-producing software or for 
people who just want to look at the innards of a PDF file to learn more about how they work.

QPDF is capable of creating linearized (also known as web-optimized) files and encrypted files. It is also capable of 
converting PDF files with object streams (also known as compressed objects) to files with no compressed objects or to generate 
object streams from files that don't have them (or even those that already do). QPDF also supports a special mode designed to 
allow you to edit the content of PDF files in a text editor. For more details, please see the documentation links below.

QPDF includes support for merging and splitting PDFs through the ability to copy objects from one PDF file into another and to 
manipulate the list of pages in a PDF file. The QPDF library also makes it possible for you to create PDF files from scratch. 
In this mode, you are responsible for supplying all the contents of the file, while the QPDF library takes care off all the 
syntactical representation of the objects, creation of cross references tables and, if you use them, object streams, 
encryption, linearization, and other syntactic details.

QPDF is not a PDF content creation library, a PDF viewer, or a program capable of converting PDF into other formats. In 
particular, QPDF knows nothing about the semantics of PDF content streams. If you are looking for something that can do that, 
you should look elsewhere. However, once you have a valid PDF file, QPDF can be used to transform that file in ways perhaps 
your original PDF creation can't handle. For example, programs generate simple PDF files but can't password-protect them, web-
optimize them, or perform other transformations of that type.

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
