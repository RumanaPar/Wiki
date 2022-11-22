**HumanResources.SAP2ARIS**

	BizTalk name: HumanResources.SAP2ARIS
	Alternative names: HR SAP2ARIS
	BAM View Name: HR SAP2ARIS
	BAM Activity Name: SAP2ARIS FILE TRANSFER
	System database: SAP BIZTALK APPLICATIONS 3 (CONTINUED)
	Product: BUSINESS SUPPORT WORKPLACE
	Task: HUMAN RESOURCES
	Application level: 1

**Description:**<br>
This solution handles employee info files, contacts and similar from SAP HR.
BizTalk's job is to transfer these files to ARIS.
<br>
<br>
**Business Specific Area/Domain:**<br>
SAP HR
<br>
<br>
**Important points**

* This is a passthru solution sending files from one fileshare to another and will only fail if BizTalk is down or destination location is down. If any suspended resumable messages, just try to resume them.
* The files should be transferred every Saturday
* Information classification: Internal
* QoP: Integrity - No need for integrity check. Classified as Internal
* QoS: Best Effort recipient or sender responsible for error handling
* Flow pattern:
	Scheduled transfer every Saturday
	Expected size of files: Maximum 10 Mb
* Latency - Can be set up to run this several hours ahead of job start in ARIS, so this can be set up according to maximum transfer time
* Tracking: No need
* Criticality: Not critical, can rerun the next day

<br>
**VSTS Details:**

	Release version: 2.0
	VSTS path: $/BizTalk/HumanResources/SAP2ARIS/Code/Release 2.0

<br>
**Changes/Redesigning During Migration:**<br>
NA

<br>
**Application Endpoints Configurations:**
The data is received from a statoil file location(where SSIS will drop the files) and sent to ARIS File Share Locations.

<br>
**Source System Details:**
The application receives 6 different types of files from SSIS every Saturday

<br>
**Destination System Details:**<br>
ARIS File Share Location

<br>
**Third Party Dependencies:**<br>
NA

<br>
**Firewall and Port Settings:**<br>
NA

<br>
**Azure API:**<br>
NA

<br>
**ServiceNow Tickets:**<br>
CHG0226273

<br>
**Capacity management:**<br>
Peak memory usage is below 100MB, and will probably not exceed this limit within the next 3 years

<br>
**Contacts:**
**Main Contact:**<br>
`ARIS:`<br>
Elin Nordmark Blegen<br>
Magnus Fonnes, lead architect human resources<br>
Espen Hatleskog<br>

`SAP:`<br>
Assignment Group: SAP - HR<br>
Knut Rogde

`Customer:`
Espen Hatleskog


`Developer:`<br>
- Kjell André Hjelleset<br>
- (BizTalk 2020 Migration) Rumana Parven(RUMP)



`Other contacts:`
Palle Ram Narasimha Reddy(pan@equinor.com) - SSIS


**Challenges Faced During Migration:**<br>
The ARIS file share location was not correct i.e. the server specified in the send port was no more in use. So, the application was tested in QA using a dummy file location after discussion with the customer.

<br>
**Error Handling:**<br>

`Queries and Requests:`
If any errors occurs, either one of the receive or send location is unaccessible or BizTalk application ports has been turned off.<br>
`BizTalk Errors:`
In case of any errors, please check in BizTalk hub or log what caused the solution to fail. Verify the following:

* Appropriate hosts is running. If not running, start host.
* Endpoints is available/running. If any of the endpoints is unavailable contact appropriate resources. See contacts.
* If customer contacts us because no files is received, check that SSIS is running as it should.
* Resume any message if it has been suspended.

`Custom Errors and Exceptions:`
There is no custom errors in this solution.

**Administration:**<br>
`Configuration:`
Make sure endpoint fileshares is accesible for the host users<br>

`GlobalVariables:`
No Global Variables

`Enhancements/ Comments / Suggestions:`






	




