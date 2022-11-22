**QA Environment**<br>

|                |                       |
| --------| -----------           |
Internal SOAP url| [https://btsqa.equinor.com](https://btsqa.equinor.com)
Database cluster| 
Database logshipping destination| 
BizTalk role| BizTalkProcess
Configuration DB| EquinorConfigDb @ WS4278\QM19001,12001
BAM Portal| [http://ws4295.statoil.net:81/BAM/](http://ws4295.statoil.net:81/BAM/)
IIS log (internal services)| 


**Frontend Server 1**<br>

    Name: WS4295 (Master SSO, BAM)
    IP: 10.27.0.41


**Frontend Server 2**

    Name: WS4296 (Reporting, Scheduled Tasks)
    IP: 10.27.0.42

**Backend Server 1**

    Name: WS4297
    IP: 10.27.0.43

**Backend Server 2**

    Name: WS4298
    IP: 10.27.0.44


**Hardware**<br>

|                |                       |
| --------| -----------           |
CPU| Intel(R) Xeon(R) Platinum 8171M CPU @ 2.60GHz
RAM| 16.0 GB
Harddrive| 127.0 GB(C) + 31.9GB(D)