**GLAS2SharePoint**

	BizTalk name: GLAS2SharePoint
	Alternative names: Transfer from GLAS to SharePoint
	Product: BizTalk and logic app

**Description**<br>
This Interface receives both MGAR and FLR files from client G drive location and move to BizTalk G drive prod location by task scheduler. BizTalk will pick those files and send to associated logic app.
<br>
<br>
**Important points**

* The Interface receives two files MGAR and FLR from Customer G drive location to our BizTalk receive location.
* A Task scheduler GLAS2SharePoint_TaskSchedular runs for every 5 minutes after triggered at 12:34 PM.

<br>
**Source System Details**<BR>
The receive location receives the files from customer G drive location and task scheduler “GLAS2Sharepoint” will move the file from customer G drive location to BizTalk G drive location.
<br>
<br>
**Destination System Details**<BR>
The send port sends the received files to Logic Apps
<br>
<br>
**Contacts**<BR>

`Main Contact:`
Ove Bjørnar Kuvåssæter,
Roald Maudal


`Developer:`<BR>
- Abdul Basit Ansari
- (BizTalk 2020 Migration) Pavan Kumar Pidugu (PKP)

**Queries and Requests**<BR>
If any errors occurs, either one of the receive or send location is unaccessible or BizTalk application ports has been turned off.
<br>
<br>
**BizTalk Errors**<BR>
In case of any errors, please check in BizTalk hub or log what caused the solution to fail. Verify the following:

* Check if appropriate hosts are running. If not running, start the hosts.
* Check if the endpoints is available/running. If any of the endpoints is unavailable contact appropriate resources. See contacts.
* Resume any message if it has been suspended.

`Custom Errors and Exceptions`
There is no custom errors in this solution.
