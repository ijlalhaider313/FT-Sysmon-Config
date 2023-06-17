# FT-sysmon-config: Yet another Sysmon config import file

This is a Microsoft Sysinternals Sysmon configuration file template whis has been forked from [SwiftOnSecurity](https://github.com/SwiftOnSecurity/sysmon-config)

Many of the changes made to this file are for tracking techniques used by modern malware or threat actors. It's important to note that some of the changes may increase logging on the host, when compared to the original sysmon config file that this was forked from. 

Used as the default Sysmon configuration file in [Enable-all-the-Logs!](https://github.com/bobby-tablez/Enable-All-The-Logs)

## Changes:
Below are a list of changes made since forking
### EVENT ID 1:
- Removed Conhost exclusion
- File events in MS Office Templates Directory (Emotet)
- File events in 'C:\ProgramData' directory (Common for malware stagers)
### EVENT ID 7:
- DLL loading from '\appdata\local'
- DLL loading from '\appdata\roaming'
- DLL loading from '\Downloads\'
- DLL loading from 'Non C drives'
### EVENT ID 11
- MS Office templates directory (Emotet)
- Include 'C:\ProgramData'
###  EVENT ID 12 & 13 & 14
- Include 'reg.exe'
- Include 'regedit.exe'
- Include 'wscript.exe'
- Include 'cscript.exe'
- Include 'C:\Windows\Temp'
- Include 'C:\Windows\Fonts'
- Include 'C:\Users\Public'
- Include '\appdata\local\'



## Use ##
### Install ###
Run with administrator rights
~~~~
sysmon.exe -accepteula -i ft-sysmonconfig-export.xml
~~~~

### Update existing configuration ###
Run with administrator rights
~~~~
sysmon.exe -c ft-sysmonconfig-export.xml
~~~~

### Uninstall ###
Run with administrator rights
~~~~
sysmon.exe -u
~~~~

**[See other forks of this configuration](https://github.com/SwiftOnSecurity/sysmon-config/network)**

## Required actions ##

### Prerequisites ###
Highly recommend using [Notepad++](https://notepad-plus-plus.org/) to edit this configuration. It understands UNIX newline format and does XML syntax highlighting, which makes this very understandable. I do not recommend using the built-in Notepad.exe.

### Customization ###
You will need to install and observe the results of the configuration in your own environment before deploying it widely. For example, you will need to exclude actions of your antivirus, which will otherwise likely fill up your logs with useless information.

The configuration is highly commented and designed to be self-explanatory to assist you in this customization to your environment.

### Design notes ###
This configuration expects software to be installed system-wide and NOT in the C:\Users folder. Various pieces of software install themselves in User directories, which are subject to extra monitoring. Where possible, you should install the system-wide version of these pieces of software, like Chrome. See the configuration file for more instructions.
