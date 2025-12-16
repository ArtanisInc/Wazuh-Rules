

# Windows Sysmon
> System Monitor (Sysmon) is a Windows system service and device driver that, once installed on a system, remains resident across system reboots to monitor and log system activity to the Windows event log. It provides detailed information about process creations, network connections, and changes to file creation time.

_We highly recommend Sysmon for your Wazuh deployment as it provides robust amounts of endpoint telemetery. Sysmon must be installed seperately and your Wazuh Agent must be instructed to collect the Sysmon logs from Event Viewer._




## [Sysmon Install Script](https://github.com/socfortress/Wazuh-Rules/blob/main/Windows_Sysmon/sysmon_install.ps1)
## [Sysmon Config Used (noisy)](https://github.com/olafhartong/sysmon-modular)
## [Sysmon Config (less noisy)](https://github.com/SwiftOnSecurity/sysmon-config)






