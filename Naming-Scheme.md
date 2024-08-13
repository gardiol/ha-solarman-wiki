# Sensor renaming w/ history

_Get out of shackles of unperturbable past!_

Steps: 
1. Open sensors detail page
2. Click on Settings
3. Change Entity ID to match new one  
**First check if entity with that name doesn't already exist and if does delete it using STATISTICS tab in Developer tools!**  
_Example: Let's say that we want to rename sensor 'Battery SOC' to 'Battery'_  
_**Current Entity ID**: sensor.inverter_battery_soc_  
_**New Entity ID**: sensor.inverter_battery_
4. Click on UPDATE
5. (OPTIONAL) Repeat for any number of sensors
6. Remove device from the integration and then re-add it back again
_Using new inverter definition profile which match new naming scheme._

Or if you are doing this process before an update to a newer version of the integration which contains changes in naming just skip 6. step and do the update instead and do restart required by HA.