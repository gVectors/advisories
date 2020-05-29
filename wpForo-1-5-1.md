# introduction

Quoting from the WordPress Plugin site (https://wordpress.org/plugins/wpforo/)...  
>wpForo Forums is the best WordPress forum plugin. Full-fledged yet easy and light forum solution for your WordPress website. Comes with modern and responsive forum layouts and styles. This WordPress forum plugin brings everything you need to run an efficient and professional community. Powerful and beautiful forum with unique features.

The forum plugin suffers from a privilege escalation vulnerability, whereby any registered forum user can escalate his privilege to become the forum administrator without any form of user interaction.

Details are provided on relase summary:
(https://wpforo.com/community/wpforo-announcements/wpforo-1-5-2-is-released/)  

In future, any vulnerabilities discovered in this number one forum plugin will most likely, very probably, be disclosed and dropped as a 0-day

# affected programs & issues

Privilege Escalation in wpForo 1.5.1 and possibly all previous version

# discovery

author: sec.9emin1@gmail.com  
discovered by: sec.9emin1@gmail.com  

The vulnerabilities were discovered by reviewing the source code and verifying it with BurpSuite

# vulnerable-file.php
```
Technical details will be released here on 021218

```
# progress

020918 - issue raised and vendor replied  
020918 - issue acknowledged and will be implementing a fix  
060918 - Version 1.5.2 released - Issue is now resolved  
