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
6. Remove device from integration
7. Add device into integration  
Using new inverter profile (inverter definition file) which match new naming scheme