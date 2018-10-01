# WMI
How to create custom WMI Namespace and Classes. 

This will create a WMI Namespace called `EvilCorp` and 2 custom WMI classes `Evil_InstalledProducts` and `Evil_InstalledProducts32`

## Why
- Alternative to opening Add/Remove Programs on remote computers
- Can query a 2000+ server, multi-OS, multi-continent server-estate in under 30 mins (using runspaces, PoshRsJobs/Invoke-Parallel).
- Please stop using Win32_Product. This is a much better alternative.

## Steps
- Save the MOF Files
- Rename `EvilCorp` to `YourCORP`
- Execute the following commands
```
mofcomp regevent64.mof
mofcomp regevent32.mof
mofcomp Evil_InstalledProducts.mof
```

## Steps
```
Get-WmiObject -ComputerName $env:COMPUTERNAME -Namespace root\EvilCorp -Class Evil_InstalledProducts | select *
Get-CimInstance -ComputerName $env:COMPUTERNAME -Namespace root\EvilCorp -Class Evil_InstalledProducts | select *

```

## Notes
- Can be rolled out remotely. Copy the MOF Files to target and `Invoke-Command` the `mofcomp`, or alternatively use PsTools.
- Isolates corp WMI Classes in a separate namespace.
