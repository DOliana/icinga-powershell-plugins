
# Invoke-IcingaCheckCPU

## Description

Checks cpu usage of cores.

Invoke-IcingaCheckCPU returns either 'OK', 'WARNING' or 'CRITICAL', based on the thresholds set.
e.g A system has 4 cores, each running at 60% usage, WARNING is set to 50%, CRITICAL is set to 75%. In this case the check will return WARNING.
More Information on https://github.com/Icinga/icinga-powershell-plugins

## Permissions

To execute this plugin you will require to grant the following user permissions.

### Performance Counter

* Processor(*)\% processor time

### Required User Groups

* Performance Monitor Users

## Arguments

| Argument | Type | Required | Default | Description |
| ---      | ---  | ---      | ---     | ---         |
| Warning | Object | false |  | Used to specify a Warning threshold. In this case an integer value. |
| Critical | Object | false |  | Used to specify a Critical threshold. In this case an integer value. |
| Core | String | false | * | Used to specify a single core to check for. For the average load across all cores use `_Total` |
| NoPerfData | SwitchParameter | false | False |  |
| Verbosity | Int32 | false | 0 | Changes the behavior of the plugin output which check states are printed: 0 (default): Only service checks/packages with state not OK will be printed 1: Only services with not OK will be printed including OK checks of affected check packages including Package config 2: Everything will be printed regardless of the check state 3: Identical to Verbose 2, but prints in addition the check package configuration e.g (All must be [OK]) |
| ThresholdInterval | String |  |  | Change the value your defined threshold checks against from the current value to a collected time threshold of the Icinga for Windows daemon, as described [here](https://icinga.com/docs/icinga-for-windows/latest/doc/service/10-Register-Service-Checks/). An example for this argument would be 1m or 15m which will use the average of 1m or 15m for monitoring. |

## Examples

### Example Command 1

```powershell
Invoke-IcingaCheckCPU -Warning 50 -Critical 75
```

### Example Output 1

```powershell
[OK]: Check package "CPU Load" is [OK]
| 'Core #0'=4,59%;50;75;0;100 'Core #1'=0,94%;50;75;0;100 'Core #2'=11,53%;50;75;0;100 'Core #3'=4,07%;50;75;0;100    
```

### Example Command 2

```powershell
Invoke-IcingaCheckCPU -Warning 50 -Critical 75 -Core 1
```

### Example Output 2

```powershell
[OK]: Check package "CPU Load" is [OK]
| 'Core #1'=2,61%;50;75;0;100    
```
