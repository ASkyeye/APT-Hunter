#APT-Hunter
APT-Hunter is Threat Hunting tool which made by purple team mindset to provide initial indication of compromise and decrease the time to uncover suspicious activity without the need to have complicated solution for parsing and detecting events like SIEM solutions and log collectors . If you are a Threat Hunter , Incident Responder or forensic investigator , i assure you will enjoy using this tool , why ? i will discuss the reason in this article and how it will make your life easy just it made mine . Kindly note this tool is heavily tested but still a beta version and may contain bugs .

#How to Use APT-Hunter

The first thing to do is to collect the logs if you didn’t and with powershell log collectors its easy to collect the needed logs automatically you just run the powershell scripts as administrator .

To collect the logs in EVTX format use : 
windows-log-collector-full-v3-EVTX.ps1 
 
To collect the logs in CSV format use : 
windows-log-collector-full-v3-CSV.ps1

APT-Hunter built using python3 so in order to use the tool you need to install the required libraries .
	
`python3 -m pip install -r Requirements.txt`

APT-Hunter is easy to use you just use the argument -h to print help to see the options needed .

` python3 APT-Hunter.py -h`
 
usage: APT-Hunter.py [-h] [-p PATH] [-o OUT] [-t {csv,evtx}]
                     [--security SECURITY] [--system SYSTEM]
                     [--scheduledtask SCHEDULEDTASK] [--defender DEFENDER]
                     [--powershell POWERSHELL] [--powershellop POWERSHELLOP]
                     [--terminal TERMINAL] [--winrm WINRM] [--sysmon SYSMON]
 
optional arguments:
  -h, --help            show this help message and exit
  -p PATH, --path PATH  path to folder containing windows event logs generated by the APT-Hunter-Log-Collector.ps1
  -o OUT, --out OUT     output file name
  -t {csv,evtx}, --type {csv,evtx}
                        csv ( logs from get-eventlog or windows event log GUI
                        or logs from Get-WinEvent ) , evtx ( EVTX extension
                        windows event log )
  --security SECURITY   Path to Security Logs
  --system SYSTEM       Path to System Logs
  --scheduledtask SCHEDULEDTASK
                        Path to Scheduled Tasks Logs
  --defender DEFENDER   Path to Defender Logs
  --powershell POWERSHELL
                        Path to Powershell Logs
  --powershellop POWERSHELLOP
                        Path to Powershell Operational Logs
  --terminal TERMINAL   Path to TerminalServices LocalSessionManager Logs
  --winrm WINRM         Path to Winrm Logs
  --sysmon SYSMON       Path to Sysmon Logs

-p : provide path to directory containing the extracted using the powershell log collectors ( windows-log-collector-full-v3-CSV.ps1 , windows-log-collector-full-v3-EVTX.ps1 ) .

-o : name of the project which will be used in the generated output sheets

-t : the log type if its CSV or EVTX

The remaining arguments if you want to analyze single type of logs.

Exmaples :

	
`python3 APT-Hunter.py  -t evtx  -p /opt/wineventlogs/  -o Project1`
 
`python3 APT-Hunter.py  -t csv  -p /opt/wineventlogs/  -o Project1`
 
`python3 APT-Hunter.py  -t evtx  --security evtx/security.evtx -o Project2`

The result will be available in two sheets :

Project1_Report.xlsx : this excel sheet will include all the events detected from every windows logs provided to APT-Hunter

Project1_TimeSketch.csv : This CSV file you can upload it to timesketch in order to have timeline analysis that will help you see the full picture of the attack .

