# Introduction 

EclecticIQ PolyMon is a Windows software that leverages the [osquery](https://osquery.io/) tool and the EclecticIQ Extension to osquery, to provide a view into detailed information about process creations, network connections, file system changes and many other activities on the system. For a detailed list of activities captured [check here](https://github.com/eclecticiq/osq-ext-bin)

The software can be used for various threat monitoring and forensic purposes on a standalone system and does not mandate burden of having a server to manage the agents. It provides a graphical user interface that allows a user to navigate through the activities and events happening on the endpoint device.

# Installation (or Upgrade)

Download the **PolyMon_Setup.exe** or clone the repository. The software can be installed by right click and 'Run as Administrator' on the binary executable. The current version is supported only on Windows 10 x64 Platform.

![setup](https://user-images.githubusercontent.com/75771864/210490541-e75d1fc6-2838-4201-a40f-a25189231bdf.png)
  
![install-wel](https://user-images.githubusercontent.com/75771864/210490801-b1cd831c-4d9e-4d68-9c47-fabf0280c234.png)

The setup wizard guides through the rest of the process.

![install-wiz](https://user-images.githubusercontent.com/75771864/210490846-54005fec-17f1-4ae5-87e6-6d27ea1078a1.png)

You can choose to install Everything tool for Desktop Search feature (selected by default via checkbox).
If you choose not to install Everything tool for Desktop Search feature, the "Desktop Search" feature will remain DISABLED and cannot be ENABLED later.

![install-desktop-search](https://user-images.githubusercontent.com/75771864/210490886-7bb0f13a-43b2-4fc7-b6e2-e2c47761a703.PNG)

The tool can be provisioned with an optional [VirusTotal](https://www.virustotal.com/) free API key. Provisioning with VirusTotal key allows the tool to fetch the reputation of file hashes automatically from it and alert in case a malicious (or supicious) detection. API key can be later added or modified after install also.

![install-vt](https://user-images.githubusercontent.com/75771864/210490923-95f5cfde-230a-45f6-9d79-9d8dfa608faf.png)

At the end of the installation, the monitoring agent registers as a tray app and gets launched. Later you can close the tool window (it will keep running as tray app) or maximize the tool window by clicking on tray icon.

![install-complete](https://user-images.githubusercontent.com/75771864/210490977-b24bf1cf-8f7c-47f2-b1f8-7376d6344aeb.png)

![tray-icon](https://user-images.githubusercontent.com/75771864/210491006-d3e0b793-b9c8-423e-89fe-81942eed6706.png)

![options_about](https://user-images.githubusercontent.com/75771864/210491036-dbd7580d-cd1e-47ea-ab43-5e77eb4a2095.png)

# Configuration

PolyMon is built with a default set of configurations for the underlying osquery agent as well as the [EclecticIQ Extension](https://github.com/eclecticiq/osq-ext-bin). This provides an extremely low touch experience for the end user. The advanced users who wish to view/edit the configuration can do so by launching the PolyMon's front end application as shown below.

![mon-config](https://user-images.githubusercontent.com/75771864/210491076-ed595032-4952-49c8-9815-0fe887c7102e.png)

PolyMon configuration follows the similar syntax as provided for EclecticIQ Extension and osquery. 

![mon-config2](https://user-images.githubusercontent.com/75771864/210491088-22ece3be-97fa-4be0-9609-1b4593ae319e.png)

# Use cases 

PolyMon tool can be used for a variety of use cases.

## Detection and monitoring

Under the hood, the PolyMon tool leverages a combination of technologies to record, query and display these activities. The most important use case is to provide a view into the activities of your system that are often not visible to naked eyes. These activities provide interesting insights for a system which can be used to root cause issues like a system breach, application misbehavior or any other unwarranted activity. Additionally, the tool can be utilized to query the properties of an endpoint. Each type of activity (or endpoint property) is provided under a tab that describes the type of activity. Each tab is a wrapper on a table provided by osquery core agent or EclecticIQ Extension. The default tabs are the 'activity monitoring' tabs. These activities include "File Events", "Process Events", "DNS Lookup", "HTTP Events" among others. The "search" box and the options on the right pane can assist with filtering the data for customizing the views.

![proc-events](https://user-images.githubusercontent.com/75771864/210491125-967e613a-6dd5-4f3f-8e65-54be31f8d940.png)

![dns-events](https://user-images.githubusercontent.com/75771864/210491242-1bab79ae-f6c9-417a-9351-9ae7c9e201a3.png)

If the tool was provisioned with VirusTotal key, it would look up the reputation of file hashes from VirusTotal database, maintaining a rate quota associated with free API keys, and trigger an alert on a match found. 

![mon-data-vt-red](https://user-images.githubusercontent.com/75771864/210491275-a2008db0-453f-44c6-a9a9-2e5200995ed9.png)

![tray-notif](https://user-images.githubusercontent.com/75771864/210491294-3f3b3909-587f-400e-8863-552e10d60ed5.png)

The alert notifications can be turned off (or on) from the menu in the tray app. A global search option allows to look for a particular files hash as collected by the PolyMon agent. 

![tray-notif-manage](https://user-images.githubusercontent.com/75771864/210491313-311cfa4c-a745-4c19-96f5-9d5bb1a84157.png)

Please keep in the mind that PolyMon DOES NOT index the entire disk. File hashes for only those file events as configured in the 'Configuration' are captured in the PolyMon. For file hashes of already resident files, the 'query' option as shown in the next section can be utilized. 

## Front-end for osquery 

For the advanced osquery users, the tool can act as graphical front end (much like the osqueyi shell) and can be used to send custom SQL queries on various osquery tables. 

![mon-osquery2](https://user-images.githubusercontent.com/75771864/210491355-e64e9186-3fbe-43e7-8a98-55819332f096.png)

## Endpoint Profiling 

A combination of osquery queries are clubbed together to generate an endpoint profile. These queries are listed below: 

![mon-profile1](https://user-images.githubusercontent.com/75771864/210491379-02bcfe44-9d18-4405-a5d2-3f77f71b9a09.png)

The generated endpoint profile can be viewed as the HTML document.

![mon-profile-htm](https://user-images.githubusercontent.com/75771864/210491398-7f01f0fd-6416-45e7-a6a4-310e2e3854ab.png)

# New features and enhancements in v4.0.0.0

## System health monitoring with health display via riskmeter 

The tool constantly monitors system health based on a set of 15 parameters, shows health parameter status as "GOOD" or "NOT GOOD" and shows 
an overall system health via riskmeter. It also allows for exporting system health report for further analysis. The health report data having 
md5 hashes of files or services is highlighted in RED with VirusTotal hyperlink if the hash is found to be malicious via VirusTotal lookup.  
 
## CIS benchmarking and reporting
  
The tool can be used to do CIS benchmark analysis of the system on more than 500 benchmarks. Also, the benchmark report
can be exported in csv format for further analysis.
   
## Osquery service updated to version 5.2.2

plgx_osqueryd.exe service, the osquery daemon shipped with PolyMon is now updated to version 5.2.2. 

## New tables added in osquery 5.2.2 and EclecticIQ extension are added in dropdown list for "Other Tables"

![osquery-table](https://user-images.githubusercontent.com/75771864/210491435-29bc8cc6-e536-4d5b-a0a2-af232c6311a4.png)

All tables (without constraints) recently added by osquery (supported only on Windows) in 5.2.2 version have been updated in the list. 

## Rebranding to EclecticIQ PolyMon

The tool is updated with EclecticIQ logo, license and copyright info. 


# New features and enhancements in v1.0.40.6

## Integration with Everything tool (https://www.voidtools.com/) to enable Desktop Search for files and get file hashes.

![desktop-search-temp](https://user-images.githubusercontent.com/75771864/210491464-03bc1d71-d4fc-4143-ae1f-df6620a9c419.PNG)

PolyMon 1.0.40.6 comes integrated with the powerful desktop search engine **[Everything](https://www.voidtools.com/)**. 
This strengthens PolyMon's endpoint investigation capabilities. Everything search engine can be accessed via "Desktop Search" tab in the PolyMon UI.
Using the similar syntax as that of Everything, desktop search can be accomplished. Additionally, on clicking "Get File Hash" button,
PolyMon will fetch the hashes of searched files and display alongwith file names. These results can be exported into a csv file via Export button.
Just browse any location and provide file name, then click "Export". This combined functionality enables being able to search for file based on hashes
as well as names and folder locations. Everything tool is bundled with PolyMon and will get automatically installed. 
This poses some bit of limitations if the Everything tool was installed outside of PolyMon. Please check the **FAQ** section to understand the known issues and limitations.

## Search for IOCs - added support for searching IP address within EclecticIQ agent's event tables.

![ioc-search-ip](https://user-images.githubusercontent.com/75771864/210491484-4efbc6af-5a4d-4c79-9832-87a54b7de4fd.png)
   
   You can now search for any IP (or substring) which will display matches in Socket, SSL, DNS, DNS Response and HTTP events 
   in a single tab separated view.   

## Menu option to add/update VirusTotal key.

![vt-key-update](https://user-images.githubusercontent.com/75771864/210491517-d19aaa03-56c8-4c3b-be0e-4f480c567695.png)

   If you didnt opt to add VirusTotal key while installing previous version, no worries. 
   It can be updated now and will be activated immediately to fetch file hash reputations in File Events.

## Save Custom Query with tags for future use. 

![tags](https://user-images.githubusercontent.com/75771864/210491567-be7b7aca-d807-43c8-8fca-d09ee94bae90.png)

   Any custom query can be saved with a tag and will be displayed on the right side of the window. 
   You can double click any saved query and copy it to run again in future.

## Ability to export results in list view (csv format) with VirusTotal url links for hashes, domains, IPs. 

   Any list view can be exported into a csv formatted data for further analysis.
   VirusTotal url links will also be exported for columns having hashes, domains or IPs.

## Ability to Start/Stop/Restart EclecticIQ agent services via Tray menu. 

![tray-notif-manage](https://user-images.githubusercontent.com/75771864/210491611-a1c64cfa-d5dd-4070-9594-0405125a867e.png)

   You can Start/Stop/Restart EclecticIQ Agent services just by a click in PolyMon Tray Icon menu options.

## Osquery service updated to version 4.5.0

   plgx_osqueryd.exe service, the osquery daemon shipped with PolyMon is now updated to version 4.5.0. 

## New tables added in osquery 4.5.0 added in dropdown list for "Other Tables"

![osquery-table](https://user-images.githubusercontent.com/75771864/210491641-d88143d2-a55c-45f3-a1c2-4de8816eba85.png)

   All tables recently added by osquery (supported only on Windows) in 4.5.0 version have been updated in the list. 

## Endpoint Profile report enriched with host encryption and security status. 

![mon-profile-htm](https://user-images.githubusercontent.com/75771864/210491671-33ea3bc4-ce18-435b-a557-c097c483b3f0.png)
   
## UI enhancements

- Window maximize, minimize and resize allowed. (minimum screen resolution: 1024x768)
- Shortcut keys for dialogs such as Ctrl+R to launch "Run Custom Query" dialog. 
- Selected row in list view is highlighted
- View Row Data of list view on doubl click any row into a popup dialog (text in popup dialog can be copied by selecting text and Ctrl-C)
- List view columns with hash, domain or IP are clickable links to VirusTotal page for reputation details. 
- Rebranding with EclecticIQ company logo
- Show/Hide columns in list view on right click list view's top row having column names
![hide-columns](https://user-images.githubusercontent.com/75771864/210491732-04c5c123-9542-4ec0-8f68-37d4748b2d28.png)

# Uninstalling PolyMon

PolyMon can be uninstalled by removing the software from 'Programs and Features' or "Add/Remove" menu of the Windows control panel. 

![uninstall-1](https://user-images.githubusercontent.com/75771864/210491774-daa6a88d-b03b-4ad1-b41f-b7c7889677f6.png)

![uninstall-2](https://user-images.githubusercontent.com/75771864/210491801-889dc8d1-f46a-470d-9318-8f4290834253.png)

![uninstall-3](https://user-images.githubusercontent.com/75771864/210491814-b19e3246-79a0-4cf1-96a7-222be4c8f9ca.png)

Note: During uninstall, PolyMon will stop Everything service (and remove the service if Everything tool was installed with PolyMon).
Though the installer tries to cleanup all the files in case of failure, if it doesn't you can run polymon_cleanup.bat from command prompt with admin privileges to cleanup the installed files.

# FAQ 

Q: What is the osquery version bundled with PolyMon 

Ans: The current release of PolyMon is bundled with osquery version 5.2.2

Q. What is the version of EclecticIQ Extension bundled with PolyMon 

Ans: The current release of PolyMon is bundled with EclecticIQ Extension version 4.0.0.0

Q. Can PolyMon be deployed, and monitored, through a central server? 

Ans: No. PolyMon is meant for a single computer usage. For getting the same functionality across a fleet of endpoints to be managed centrally, use [EclecticIQ ER](https://github.com/eclecticiq/eiq-er-ce) solution. 

Q. Can PolyMon co-exist with osquery agent installed via other mechanism? 

Ans: It can, as long as the other osquery agent is not using EclecticIQ Extension at the same time. 

Q. I see some event tabs filled with data quicker than others. Why?

Ans: The tool pre-populates the data for some event types (File, Process, Socket, DNS, DNS Response, SSL and Image Load). For other event tabs, the data is fetched on-demand.

Q. Sometimes the UI hangs or shows 'Not responding'. Why?

Ans: This can happen if the query triggered is computing high volume of data. Waiting for a few seconds will resolve the issue.

Q. Can the tool work with a commercial VirusTotal API?

Ans: It can but the tool would still maintain the lookup rate of a free API (i.e. 4 per minute).

Q. I have a feature request (or a bug to report). How do I do so?

Ans: Easiest way would be to create an issue on github.

Q. What is the license for using, or distributing, PolyMon?

Ans. PolyMon is a freeware but licensed. All rights belong to EclecticIQ B.V. Please refer to the License file in the repository for detailed criteria. 

Q. I already have Everything tool installed. Do I still need to select option to install Everything tool via PolyMon installer for Desktop Search?

Ans: If Everything tool is already installed on your system while you are installing PolyMon, it will be ignored for enabling "Desktop Search".
	 This means, to enable Desktop Search feature, you have to select checkbox to install Everything tool for Desktop Search feature.

Q. What happens to Everything tool configuration if I have it already installed and again choose to install it with PolyMon for Desktop Search, and then uninstall PolyMon?

Ans: Since Everything tool was installed with PolyMon, Everything service will be removed on uninstall. But Everything service can be reinstalled from Everything tool UI options.

Q. What happens to Desktop Search feature if I choose to install Everything with PolyMon for Desktop Search, then install Everything tool via its installer, and uninstall
Everything tool via its installer or via "Add Remove Programs" control panel?

Ans: Uninstalling Everything tool via its installer or via "Add Remove Programs" control panel may remove Everything service also and Desktop Search feature may not be usable. To continue working with Desktop Search feature, open command prompt with admin privileges in "C:\Program Files\plgx_osquery\Everything" directory and run:
- Everything.exe -startup -admin
- Everything.exe -install-service
- Everything.exe -install-run-on-system-startup
