Welcome to the Solarman Stick Logger wiki!  

_Here you can read about some of the need-to-knows, excessive integration features as well many general energy tips and tricks_

## 💡 Tips and Tricks  
If you are not living in a place where is energy cost calculated as sum of all three phases (e.g. Germany) but living in a place where is energy cost calculated for each phase individually (e.g. Czechia) in a three-phase systems then set the Zero Export value to at least 100 W. You will save some money! 😉

# ✍ Changes
_What you need to know before for example switching from Stephan Joubert's integration._
1. Any custom inverter definition profiles (arbitrarily named) has to be within 'inverter_definitions/custom/' directory to persist through integration updates, etc.
2. Sensors update interval is way more frequent but it does mainly affects sensors like current power, etc. And in a way so that you can always have the most recent and accurate information possible for your automations and live view. When comes to the actual data stored within HA that is controlled by recorder and its sampling rate. So update interval of 5 seconds or for example 60 seconds is no different when comes to amount of stored data in the database.
3. Don't be scared of changed entity names - entity_ids (HA is smart enough to keep history of all of your sensors and you can even transfer sensor's history under new name - entity_id).  
_More 'bout that [here](https://github.com/davidrapan/ha-solarman/wiki/Naming-Scheme#sensor-renaming-w-history)_

> [!WARNING]  
> Way more dangerous is when you load wrong profile (e.g. 'deye_hybrid.yaml' instead of 'deye_sg04lp3.yaml'). It will mess up with your values and thus history (you will have to correct all values manually using Developer Tools) so be careful with selecting appropriate profile under existing name (e.g. when you're re-adding device for some reason).

# 🎁 Features
- Implementation mainly focused on performance and reliability
- Discovery and not just during configuration but also as part of initialization (i.e. adapts to changed IP)
- Registers which will be part of a request are decided dynamically (when not set in the inverter profile)
  - Can be requested individually in specific intervals according to their 'update_interval' value set in the inverter profile file (defaults to 60 seconds)
- Attribute type of a sensor which can be attached to any other sensor
- Configuration items for Battery Nominal Voltage and Battery Life Cycle Rating for calculating SOH and life cycles of the battery
- Supports configuration of inverter (Battery, Zero Export power, Grid Export Surplus, Work Mode Programs, ...)
  - Number, Select, Switch and Time entity types for configuring the inverter
- Configuring of the inverter **won't interrupt fetching and has long enough timeout to overcome stick unresponsiveness**

## ⚙️ Custom Sensors  
_Which are calculated over data from the inverter_
- PV Power (combined power of all inputs)
- Losses (calculates device consumption + AC/DC conversion losses)
  - Power (current losses)
  - Today's Losses
  - Total Losses
- Battery (for devices which don't provide those through registers)
  - SOH
  - State ["charging", "idle", "discharging"]
  - Today's Battery Life Cycles
  - Total Battery Life Cycles

_More 'bout that [here](https://github.com/davidrapan/ha-solarman/wiki/Custom-sensors)_

## 🕑 Update Intervals

Are fully configurable down to a single sensor but cause register values are in nature requested in batches is possible that some will update more frequently just because value was present in the response so it's a no brainer to also update it in the sensor from HA's side.

> [!NOTE]  
> Solarman is a mess! 🤯  
> Even so the default update interval is set to 5 seconds, sometimes it goes up to ~25 seconds cause the stick don't want to talk with us. 😊  
> It's true that this upper bound is artificially set by timing parameters of the integration but it's already fine tunned and anything lower than that is just causing tremendous issues! 🙁

# 🚀 Miscellaneous

Some might wonder why Energy Dashboard shows different(higher) Load Consumption than sensor like for example "Today(Daily) Load Consumption. And it's because the Energy Dashboard does it's own calculations by summing up Imported(Bought) and Produced energy which also includes consumption of the inverter itself + some AC/DC losses along the way."  

_So for those curious enough here is some insight..._  

#### ⚡ Inverter power losses calculation [W]:
```
Power losses = Battery Power + PV1 Power + PV2 Power - Inverter Power
```

#### ⚡ Total losses calculation [kWh]:
```
Total losses = Total Energy Import(Bought) + Total Production + Total Battery Discharge - Total Energy Export(Sold) - Total Battery Charge - Total Load Consumption
```

#### ⚡ Today(Daily) losses calculation [kWh]:
```
Today(Daily) losses = Today(Daily) Energy Import(Bought) + Today(Daily) Production + Today(Daily) Battery Discharge - Today(Daily) Energy Export(Sold) - Today(Daily) Battery Charge - Today(Daily) Load Consumption
```

_To get value which is in Energy Dashboard as "Home Consumption" remove subtraction of Load Consumption from the above._  

# 🏭 Diagnostics

I was using during the development also this sensor bundle:
```
template:
  - trigger:
      - platform: time_pattern
        seconds: /1
    sensor:
      - name: "Update Ticker"
        unique_id: "update_ticker"
        state: "{{ '%0.6f' % as_timestamp(now()) }}"
        icon: "mdi:metronome-tick"
  - sensor:
      - name: "Inverter Device Since Last update"
        unique_id: "inverter_device_since_last_update"
        availability: "{{ has_value('binary_sensor.inverter_connection') }}"
        state: "{{ max((states('sensor.update_ticker') | float - as_timestamp(states.binary_sensor.inverter_connection.last_updated)) | round(0, 'ceil'), 0) }}"
        state_class: "Measurement"
        device_class: "Duration"
        unit_of_measurement: "s"
      - name: "Inverter Device Last update"
        unique_id: "inverter_device_last_update"
        availability: "{{ has_value('binary_sensor.inverter_connection') }}"
        state: "{{ (states.binary_sensor.inverter_connection.last_updated | as_local).strftime('%H:%M:%S') }} ❘ {{ '%02d' % states('sensor.inverter_device_since_last_update') | int(0) }} seconds ago"
        icon: "mdi:calendar-clock"
```
Which provides informantion about how long it is since last update (with resolution of seconds).  
Maybe it will be useful for some, but since the stability of the polling improved a lot it's not really needed.  