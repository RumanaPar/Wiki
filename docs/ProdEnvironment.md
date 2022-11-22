**Prod Environment**<br>

|                |                       |
| --------| -----------           |
Internal SOAP url| [https://bts.equinor.com](https://bts.equinor.com)
Database cluster| 
Database logshipping destination| 
BizTalk role| 
Configuration DB| EquinorConfigDb @ WS4319\PM19003,12001
BAM Portal| [http://ws4312.statoil.net:81/BAM/](http://ws4312.statoil.net:81/BAM/)
IIS log (internal services)| 


**Frontend Server 1**<br>

    Name: WS4312 (Master SSO, BAM)
    IP: 10.27.0.45


**Frontend Server 2**

    Name: WS4313 (Reporting, Scheduled Tasks)
    IP: 10.27.0.46

**Backend Server 1**

    Name: WS4314
    IP: 10.27.0.47

**Backend Server 2**

    Name: WS4315
    IP: 10.27.0.48


**Hardware**<br>

|                |                       |
| --------| -----------           |
CPU| Intel(R) Xeon(R) Platinum 8171M CPU @ 2.60GHz
RAM| 16.0 GB
Harddrive| 127.0 GB(C) + 31.9GB(D)