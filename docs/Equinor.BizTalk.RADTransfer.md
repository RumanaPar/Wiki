**Equinor.BizTalk.RADTransfer**

	BizTalk name: Equinor.BizTalk.RADTransfer
	Product: BizTalk and logic app						



**Description:**<br>
This Interface receives the file from customer G drive location and a task scheduler moves the file to BizTalk G drive location in receive location and sends the file the file to data factory.
<br>
<br>

**Important points**

* The Interface receives the files from Customer G drive location to our BizTalk receive location.
* A Task scheduler RADTransfer_TaskSchedular runs to move the file from customer G drive location to BizTalk G drive location.

<br>
**VSTS Details**

	Release Version: 1.0
	VSTS Path: $/BizTalk/Equinor.BizTalk.RADTransfer/Code/Release 1.0

<br>
**Changes / Redesign During Migration:**<BR>
Changed the logic app to Data factory at the send port.

<br>
**Source System Details**<BR>
This Interface receives the file from customer g drive location and a task scheduler “RADTransfer” moves the file from customer G drive location to BizTalk G drive location.

<br>
**Destination System Details**<BR>
This send port sends the file to Data factory.

<br>
**Contacts**

`Main Contact:`
Stefan Klaus(sklau)


`Developer:`<br>
- Abdul Basit Ansari<BR>
- (BizTalk 2020 Migration) Pavan Kumar Pidugu (PKP)