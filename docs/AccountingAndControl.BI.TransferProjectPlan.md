**AccountingAndControl.BI.TransferProjectPlan**

	BizTalk name: AccountingAndControl.BI.TransferProjectPlan
    BAM View Name: PlnDataToCenturies,ProjPlanTransProce
	System database: CVP
    Service Name: BW Project Plan Data						



**Description**<BR>
 Every day Project Plan Data is received from BW which is then sent to STEA and CVP. Please refer to Integration specification document for more details.
 <br>
 <br>

**Business Specific Area/Domain**<BR>
SAP BW
<BR>
<BR>

**Important points**

* Ordered delivery: No<br>
* Frequency: a one time a day<br>
* Load: 1 reports per day
* Time range will always have to start with 23:00:00 (End of the day)

<br>
**VSTS Details**

	Release version: 2.0
    VSTS path: $/BizTalk/AccountingAndControlling/TransferProjectPlan/Release 2.0

<br>
**Changes / Redesign During Migration**<BR>
NA

<br>
**Application Endpoints Configuration**<BR>
The data is received from SAP BW using an sftp port which is then routed to STEA and CVP systems.

<br>
**Source System Details**<BR>
SAP BW (The application Receives Meridio ProjectID info from SAP BW using SFTP)

<br>
**Destination System Details**<BR>
STEA and CVP Systems

<br>
**Third Party Dependencies**<BR>
NA

<br>
**Firewall and Port Settings**<BR>
NA

<br>
**Azure API**

    Dev: https://api-dev.gateway.equinor.com/centuriesfunctionapp/v1/integrateplndatatocenturies<br>
    Test: https://api-test.gateway.equinor.com/centuriesfunctionapp/v1/integrateplndatatocenturies<br>
    Prod: https://api.gateway.equinor.com/centuriesfunctionapp/v1/integrateplndatatocenturies

<br>
**ServiceNow Tickets**<BR>
CHG0226696

<br>
**Contacts**

<table style="width:100%">
  <tr>
    <th>Technical Contacts</th>
    <th>Functional Contacts/Stakeholders</th>
    <th>Additional Contacts</th>
  </tr>
  <tr>
    <td></td>
    <td>1.Arne Solås (arsola@equinor.com)<br>2.Mads Dyrlid Rødal (MADRO@equinor.com)(Centuries DB)<br>3.Steinar Ellingsen (stelli@equinor.com)(STEA)</td>
    <td>Lakshmi Medisetty (BW)</td>
  </tr>
</table>

`Main Contact:`
Arne Solås, Mads Dyrlid Rødal(Centuries DB), Steinar Ellingsen(STEA)<br>
`Primary and Secondary Customer:`
Arne Solås, Mads Dyrlid Rødal(Centuries DB), Steinar Ellingsen(STEA)


`Developer:`<BR>
- 1.0 Kunal Jadhav(KUNJ)<BR>
- 2.0 (BizTalk 2020 Migration) Rumana Parven(RUMP)<BR>
<table style="width:100%">
  <tr>
    <th>Version</th>
    <th>Developer</th>
  </tr>
  <tr>
    <td>1.0</td>
    <td>Kunal Jadhav(kunj@equinor.com)</td>
  </tr>
  <tr>
    <td>2.0</td>
    <td>Rumana Parven(rump@equinor.com)</td>
  </tr>
</table>

`Other contacts:`
Lakshmi Medisetty (BW)

<br>
**Error Handling**<BR>
Error would be logged in BAM

<br>
**Challenges Faced During Migration**<BR>
Increased the close, open and send timeout for the Oracle DB send port because a timeout exception was getting thrown.

<br>
**Administration**<BR>
If you want to reprocess the failed file from the back up location then follow below steps.<BR> 1. Change the pipeline in the receive location 'AccountingAndControl.BI.TransferProjectPlan.ReceiveProjectPlan.RoutedFromSFTP' to the pipeline same as that of another receive location 'AccountingAndControl.BusinessIntelligence.TransferProjectID.ReceiveProjectID.SAPBW.SFTP'<BR> 2. In the pipeline properties set Encoding = unicode in the stage 1 (Decode stage).<BR> 3. Peocess the failed file from this receive location 4. After processing the failed data, change the pipeline back to XmlReceive pipeline in receive location 'AccountingAndControl.BI.TransferProjectPlan.ReceiveProjectPlan.RoutedFromSFTP'.

<br>
**GlobalVariables**<BR>
No Global Variables

<br>
**Enhancements/ Comments / Suggestions**

