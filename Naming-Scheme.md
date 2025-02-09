# Sensor renaming w/ history

_Get out of shackles of unperturbable past!_

Steps: 
1. Open sensor's detail page and click on ⚙️ Settings in top right corner
2. Change Entity ID to match new one (Ignore any 's in new sensor name! It's usually just a display name and not projected into an ID)  
**First check if entity with that name doesn't already exist and if does delete it using STATISTICS tab in Developer tools!**  
_Example: Let's say that we want to rename sensor 'Battery SOC' to 'Battery'_  
_**Current Entity ID**: sensor.inverter_battery_soc_  
_**New Entity ID**: sensor.inverter_battery_
3. Click on UPDATE
4. (OPTIONAL) Repeat for any number of sensors
5. Remove device from the integration and then re-add it back again  
_Using new inverter definition profile which match new naming scheme._

If you are doing this process before an update to a newer version of the integration which contains changes in naming proceed with restart as required by HA before the step number 5.

Or if you already upgraded and want to restore the history there is a chance you will have to rollback to previous entity names by loading up the device with older inverter profile. Do the history transfer by following the steps and then go back to the newer version of profile.

**There is also [Detailed guide](https://github.com/davidrapan/ha-solarman/discussions/127#discussioncomment-10561824) or [⚠️ Alternative method](https://github.com/davidrapan/ha-solarman/discussions/183), _use this at your own risk_ from [@philmassie](https://github.com/philmassie)**