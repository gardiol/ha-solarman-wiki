Welcome to the Solarman Stick Logger wiki!  

_Here you can read about some of the need-to-knows, excessive integration features as well many general energy tips and tricks_

# ✍ Changes
_What you need to know before for example switching from Stephan Joubert's integration._
1. Any custom inverter definition profile has to be within 'inverter_definitions/custom/' directory to persist through updates.
2. Updates are way more frequent but it does mainly affects sensors like current power, etc. And in a way that you always have the most accurate information. When comes to the actual data amount stored within HA that is controlled by recorder and its sampling rate.
3. Don't be scared of changed entity names (HA is smart enough to keep history of all your sensors and you can even transfer it under new names).

# 💡 Tips and Tricks
If you are not living in a place where is energy cost calculated as sum of all three phases (e.g. Germany) but living in a place where is energy cost calculated for each phase individually (e.g. Czechia) in a three-phase systems then set the Zero Export value to at least 100 W. You will save some money! 😉

# 🎁 Features
- Implementation mainly focused on performance and reliability
- Discovery and not just during configuration but also as part of initialization (i.e. adapts to changed IP)
- Registers which will be part of a request are decided dynamically (when not set in the inverter profile)
  - Can be requested individually in specific intervals according to their 'update_interval' value set in the inverter profile file (defaults to 60 seconds)
- Attribute type of a sensor which can be attached to any other sensor
- Configuration items for Battery Nominal Voltage and Battery Life Cycle Rating for calculating SOH and life cycles of the battery
- Supports configuration of inverter (Battery, Zero Export power, Grid Export Surplus, Work Mode Programs, ...)
  - Switch, Number and Time entity types for configuring the inverter

### ⚙️ Custom sensors  
_Which are calculated over data from the inverter_
- PV Power (combined power of all inputs)
- Losses (calculates device consumption + AC/DC conversion losses)
  - Power (current losses)
  - Today Losses
  - Total Losses
- Battery SOH
- Battery State ["charging", "standby", "discharging"]
- Grid State ["On", "Off"]
- Today Battery Life Cycles
- Total Battery Life Cycles

_More about that [here](https://github.com/davidrapan/ha-solarman/wiki/Custom-sensors)_

# 🕑 Update Intervals

Are fully configurable down to a single sensor but cause register values are in nature requested in batches is possible that some will update more frequently just because value was present in the response so it's a no brainer to also update it in the sensor from HA's side.

> [!NOTE]  
> Solarman is a mess! 🤯  
> Even so the default update interval is set to 5 seconds, sometimes it goes up to ~25 seconds cause the logging device don't want to talk with us. 😊  
> It's true that this upper bound is artificially set by timing parameters of the integration but it's already fine tunned and anything lower than that is just causing tremendous issues! 🙁