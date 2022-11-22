**Deployment in BizTalk 2020**<br><br>
Deployment in BizTalk 2020 is based on PowerShell. Instead of creating MSI, you will create a build on the build server. Each biztalk release will have it's own PowerShell script, and this script will be responsible for all operations neccesary.

The common deploy script is owned by BizTalk opereations and as such all requests for changes / bugs improvements should be sent to them.
<br><br>

**Setting up your developing environemnt**<br>
---
**Installing certificates on local computer**<br>
Since the PowerShell scripts are stored on a network drive (G:), these scripts are signed with a certificate so that you can execute them from the network drive. (If they were not signed, you would have to copy them locally to execute them)

* Start > Run > mmc
* File > Add/Remove Snap-In…
* Select Certificates > Add
* Select My user account > OK
* Right-click “Trusted Root Certification Authorities” > All tasks > Import
* Browse to \\statoil.net\dfs\common\I\IT-FLK\Integrasjonsinfrastruktur\BizTalk Operations\Certificates\Powershell
* Select biztalkCARoot.cer
* Just leave default settings and click till certificate is installed
* Right-click “Personal” > All tasks > Import
* Browse to \\statoil.net\dfs\common\I\IT-FLK\Integrasjonsinfrastruktur\BizTalk Operations\Certificates\Powershell
* Select biztalkPowerShellCodeSigning.pfx
* Just leave default settings and click till certificate is installed (ask around for the password or just write "biztalk")
* For biztalkPowerShellCodeSigning-certificate under Personal
    * Double-click certificate
    * Choose Certification Path > Select Certification Path and verify that it looks like this:
    ![Certificate](C:\Users\RUMP.STATOIL-NET\Documents\mkdocs\CertificateSnip.png "Certificate")
    <br><br>

**Set policies on local computer**<br>
These steps must be done the first time deployment is performed from a client.

* Go to start menu > Accessories > Windows PowerShell
* Right-click “Windows PowerShell” and select “Run as administrator”
* Execute this command : Enable-WSManCredSSP -Role Client -DelegateComputer "*"
* Press 'y' then enter

If you recently have been given Elevated privileges, you should run the "Windows 10 Elevated Privileges installer" application in the Equinor Install applications list before running Windows Powershell.
<br><br>

**Executing a PowerShell deployment script**<br>
This script will deploy the application to all servers in a given environment

* Use your powershell (As administrator) command window and navigate to the folder where the script is located, i.e. cd “\\statoil.net\dfs\common\I\IT-FLK\Integrasjonsinfrastruktur\Projects\Utility\Library\Releases\Release 4.0\Deployment scripts”
* Execute the script entering the name of the script, i.e. Deploy.Utility.Library.ps1
 <br><br> 

 **Signing PowerShell script files**<br>
 This step is necessary to perform if you have created a new script, or made changes to an existing one. The reason for signing the powershell scripts is to be able to run them from a network folder.

To sign a powershell script, either use Project Checker, or use a command similar to the two examples below.

* Set-AuthenticodeSignature "\\statoil.net\dfs\common\I\IT-FLK\Integrasjonsinfrastruktur\BizTalk Operations\PowerShell\Deploy.Common.ps1" @(Get-ChildItem cert:\CurrentUser\My -codesigning | where {$_.Subject -match "BizTalk PowerShell"})[0]

* Set-AuthenticodeSignature "\\statoil.net\dfs\common\I\IT-FLK\Integrasjonsinfrastruktur\Projects\Utility\Scheduler\Releases\Release 1.0\Deploy.Utility.Scheduler.ps1" @(Get-ChildItem cert:\CurrentUser\My -codesigning | where {$_.Subject -match "BizTalk PowerShell"})[0]
<br><br>

**Ordering changes in the common script**<br>
The script is owned by operations and all changes have to be approved by them. Use a normal servicecenter request. There will be no application specific implementations in the script. All functions are generic. If your application requires something very specific either add it to you deploy script or add it as a manual task in the deploy infopath.
<br><br>

**The following function is requested but not implemented in the commom deployment script**<br>
* Creating SSO entries
* Adding entries in SSO
* Function for renaming sendports
<br><br>

Deployment instructions<br>
We will still use the existing infopath document. Normally it should just contain information on which deploy script to run and then start the application.
* The script does not support starting / stopping of applications and this will be a manual task to be performed by operations.
* Removing applications is also not implemented as this will be a manual task for operations.
<br><br>
#### Example of a deploymentscript<br>
add image<br>
Each application specific script will have a referance to a Common PowerShell script, containing lots of helper functions, such as:
#### Deploy.Common.ps1 methods<br>
---
#### Methods for handling BizTalk applications<br>
* CreateBTSApplication string $appName, string $appDescription, bool $isRemoteInstall (Default: "False")
    * Creates a new BizTalk application. Will not overwrite or re-create an existing application.
* AddApplicationReference string $appName , string $addReferenceToAppName
* RemoveApplicationReference string $appName, string $addReferenceToAppName ( Not implemented )
<br><br>

#### Operations for adding assemblies to the global assembly cache<br>
* GacOperation string $command, string $assembly
    * Note: Use GacAdd for standard installing
    * $command can be /i (install) /u uninstall /f force reinstall.
    * $assembly requires a full path where the file is to be found.
    * GacAdd string $assembly
    * Use this instead of GacOperation for adding assemblies unless you need special command options.
    <br><br>

#### Operations for adding resourcs to BizTalk applications<br>
* AddResource string $appName, string $resType, string $srcPath, string $destination
    * Use AddBizTalkAssembly / AddAssembly / AddBAMResource for common add operations. For non common operations use this one.
    * $resType: e.g. "System.BizTalk:BAM" / "System.BizTalk:BizTalkAssembly"
    * AddBizTalkAssembly string $appName, string $srcPath
    * AddAssembly string $appName, string $srcPath
    * AddBAMResource string $appName, string $srcPath

* ImportBinding string $appName, string $bindingFilePath
<br><br>

#### Methods for handling BAM / Trackingprofile deployment<br>
* BAM methods. Input is a BAM xml definition exported from excel.
    * DeployBAMConfig string $srcPath
    * UnDeployBAMConfig string $srcPath
    * UpdateBAMConfig string $srcPath
    * AddBAMUsers string $viewName, string $accountName
        * e.g. AddBAMUser "MarketingYieldCurv" "statoil-net\a_jmor"
* DeployTrackingProfile string $srcPath
<br><br>

#### Methods for handling orchestrations configuration<br> 
* SetOrchestrationStatus string $orchestrationName, string $assemblyVersion, string $status
* UnenlistOrchestration string $orchestrationName, string $assemblyVersion
* EnlistOrchestration string $orhcestrationName, string $assemblyVersion
<br><br>

#### Methods for handling file related operations <br>
* CreateLocalDiskFolder string $path
    * Only use this in very specific cases
    * Uses remoting and will create the same folder on all servers for the given environment
* CreateFolder string $path
    * Use this for creating network shares
* CopyFolder string $sourceFolder, string $targetFolder
    * Copies all files and subfolders from one folder to the targetfolder
    * Supports remoting and will copy for all servers in the given environment.
* CopyFile string $sourceFile, string $targetFolder
* SetAccess string $path, string$Account, string $Permission
<br><br>

#### Methods for running database scripts <br>
* RunDatabaseScript string $script, string $databaseServer
    * RunStatoilConfigDatabaseScript string $script
    * RunIntegrationCustomerDatabaseScript(string $script)
<br><br>

#### Methods for handling web tasks <br>
* CreateWebApplication string$webSiteName string$appPool string$sourceFolder
    * Creates or overwrites(if existing) website. Also copies files from sourceFolder to the created folder for the webapp. (Warning! Method deletes folder for website if it exists!)
<br><br>

#### Misc. methods<br> 
* RestartHost string $hostName
* CreateEnvironmentVariable string $envarName, string $envarValue
* CreateScheduledTask string$taskDefinitionFilePath, string$scheduledTaskName
    * Tip: Create schedule locally and export to xml file.
    * Filepath should follow same naming convention and location as for bindingfiles (use .ScheduleInfo.xml) as ending instead.
    <br><br>

#### Queries about QA / production setup<br>
The [operations team](www.) will be able to provide information about the setup in QA / production as required.





 