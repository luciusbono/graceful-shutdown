# graceful-shutdown.ps1
A Powershell script that mimics the GUI shutdown command but does not restart running apps. 

**WARNING - This script was written mostly with AI, use at your own risk**

When modern Windows is shut down via the GUI the last interactive user is automatically logged in and the session is locked via what I believe to be [Winlogon automatic restart sign-on (ARSO)](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/manage/component-updates/winlogon-automatic-restart-sign-on--arso-) although this behavior is not well documented. 

`shutdown.exe` has the `/sg` flag which will mimic this behavior, but it also automatically relaunches running apps, regardless of whether or not this feature is enabled in Windows or not. 

Some apps expect this "warm boot", and don't behave properly until the user logs in - and some cranky users, like me, don't want their running apps restored - but luckily there is an undocumented flag in the `ExitWindowsEx` function of the `win32 API` called `EWX_ARSO` that seems to recreate the behavior of initiating a shutdown from the GUI without restarting running apps.

I use this script with [Sleep-On-LAN](https://github.com/SR-G/sleep-on-lan) to remotely shut my Windows machine down. 

This script will provide the same shutdown reasons as `shutdown.exe` when no reason parameter is passed. If this bothers you, I'm sorry - this was a quick fix to a very specific problem that only I probably have. 
