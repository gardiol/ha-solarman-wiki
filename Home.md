Welcome to the Solarman Stick Logger wiki!  

_Here you can read about some of the excessive integration features as well many general energy tips and tricks_

# 🎁 Features
- Supports configuration of inverter (Battery, Grid Zero Export, Grid Export Surplus, Work Mode Programs, ...)
- Discovery and not just during configuration but also as part of initialization (i.e. adapts to changed IP)
- Registers which will be part of a request are decided dynamically (when not set in the inverter profile)
- Different registers can be requested in specific intervals according to their 'update_interval' value set in the inverter profile (definition file)
- Attribute type of a sensor which can be attached to any other sensor
- Switch, Number and Time entity types for configuring the inverter
- Configuration items for Battery Nominal Voltage and Battery Life Cycle Rating for calculating SOH and life cycles of the battery


### Custom sensors (which are calculated over data from the inverter)
- Battery SOH
- Battery State ["charging", "standby", "discharging"]
- Grid State ["On", "Off"]
- Today Battery Life Cycles
- Total Battery Life Cycles

## 💡 Tips and Tricks

If you are not living in a place where is energy cost calculated as sum of all three phases (e.g. Germany) but living in a place where is energy cost calculated for each phase individually (e.g. Czechia) in a three-phase systems then set the Zero Export value to at least 100 W. You will save some money! 😉