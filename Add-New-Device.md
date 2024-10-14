# Basic concepts

Adding a new device is as simple as creating a new profile YAML.
While you test & develop, it should be added under:

`/custom_components/solarman/inverter_definitions/custom`

It will be moved under:
`/custom_components/solarman/inverter_definitions/`

You should name your YAML file based on your Inverter brand and type like this:
`deye_sg04lp3.yaml`

The file name should start with the brand name followed by model type without specific rated power (e.g. 4.6~6K).


# Step 0: basic requirements

In order to add a new inverter to ha-solarman, you need:
- An inverter connected to a Solarman stick (wifi or wired)
- A suppoerted Solarman stick (v5)
- The **modbus** specification from the inverter producer

Solarman, the interconnection stick, basically acts as a **modbus** to wifi/ethernet converter adding on top of basic modbus a proprietary protocol. In order to interface with it you **need** your inverter modbus specifications.
In order to obtain such information, you should either look into your inverter producer web site, or directly ask your inverter support company for a modbus interface PDF file.

The modbus information you need is the list of read, and maybe also write, registers provided by the inverter over modbus.


# Step 1: writing the YAML

We are trying to standardize the entity names, because each vendor provides different names. To prevent eccessive confusion and provide logical name, try to follow the following guidelines:
- Total/Today Production
- Total/Today Energy Import/Export
- Total/Today Battery Charge/Discharge
- Load L1 Power/Voltage/Current
- Load Power for sum of all phases
- Battery for battery level
- Output L1 Power/Voltage/Current
- Power for sum of all output phases
- MPPTx values should be named PVx Power
- All **Total** energy sensors should be expressed in kWh.

In general, you can find all the examples which follow this standard in deye_sg04lp3.yaml profile. Please take a good look at it and use it as a starting point.
The file should also follow general structure of already present profiles.

Keep in mind that every inverted model is different and yours might support or not support specific funcitonalities like BMS, EPS and such. Do not blindly copy another model yaml file but adapt it to your device removing (or adding) functionalities as needed.
As an example, if your inverter do not expose BMS data, omit the associated entities.

Consider also the following details:
- Reactive Power has class: "reactive_power", uom: "var" 
- Active Power has class: "power", uom: "W" and if the sum of all inverter outputs, it should be called just **Power**
- Power Factor has class: "power_factor", uom: "%"

One more thing, you should to combine all the static info into a single sensor entity called **Device** using attributes. It's really not required but does clear out from the list values which are not changing with time.
A good example can be:
```
  - group: info
    update_interval: 300
    items:
      - name: "Device"
        rule: 5 # ASCII String
        registers:
          [
            0x1A00,
            0x1A01,
            0x1A02,
            0x1A03,
            0x1A04,
            0x1A05,
            0x1A06,
            0x1A07,
            0x1A08,
            0x1A09,
            0x1A0A,
            0x1A0B,
            0x1A0C,
            0x1A0D,
            0x1A0E,
            0x1A0F,
          ]
        icon: "mdi:information"
        attributes:
          [
            "Device Protocol Version",
            "Device Serial Number",
            "Master Software Version",
            "Master Software Build Date",
            "Slave Software Version",
            "Slave Software Build Date",
            "Device MPPTs",
            "Device Rated Voltage",
            "Device Rated Frequency",
            "Device Rated Power",
            "Device Phases",
            "Production Type",
            "EMS firmware Version",
            "EMS firmware Build Date",
            "DCDC firmware Version",
            "DCDC firmware Build Date",
          ]

      - name: "Device Protocol Version"
        attribute:
        rule: 7 # version
        remove: "0."
        registers: [0x1A1C]
        icon: "mdi:information"
 .... and so on ...
```

It's done using attribute: over entity which you want turn into attribute. And then with attributes: ["Name of entity", "Name of other entity", ...] in entity to which you want them to be attached. Can be seen in the sg04lp3 profile.


## Endianess issues

Modbus has a peculiar endianess and not all inverters do provide 32bit values with the proper register order. If you have very strange values, you might need to swap the two 16bit registers containing the 32bit value like the following example:
```
      - name: "Total Energy"
        class: "energy"
        state_class: "total_increasing"
        uom: "kWh"
        rule: 1
        registers: [0x1022, 0x1021]
        icon: "mdi:solar-power"
        sensors:
            scale: 0.001
        validation:
          min: 0.1
```

As you can see in this example, the two 16bit registers have been written as [0x1022, 0x1021] instead of [0x1021, 0x1022].

You can also combine multiple registers like the following example:
```
      - name: "Total Production" # aka "Total Energy" + "Decimals of total energy"
        class: "energy"
        state_class: "total_increasing"
        uom: "kWh"
        rule: 3
        registers: [0x1022, 0x1021, 0x104C]
        icon: "mdi:solar-power"
        sensors:
          - registers: [0x1022, 0x1021]
          - registers: [0x104C]
            scale: 0.001
        validation:
          min: 0.001
```
the above entity combine two modbus values into one (fixed part + decimals)

## Custom sensors

You need to add some custom sensors, that will summarize variuos quantities for you, the following ones are a guideline.

Power losses:
```
      - name: "Power losses"
        description: "Includes consumption of the inverter device itself as well AC/DC conversion losses"
        class: "power"
        state_class: "measurement"
        uom: "W"
        scale: 0.1
        rule: 3
        registers: [0x1049, 0x1048, 0x200A, 0x2009, 0x1038, 0x1037]
        uint: enforce
        sensors:
          - registers: [0x1049, 0x1048]
          - registers: [0x200A, 0x2009]
          - operator: subtract
            signed:
            registers: [0x1038, 0x1037]
```

Total losses:
```
      - name: "Total Losses"
        description: "Includes total consumption of the inverter device itself as well AC/DC conversion losses"
        class: "energy"
        state_class: "total_increasing"
        ensure_increasing:
        uom: "kWh"
        rule: 3
        digits: 2
        scale: 0.01
        registers:
          [
            0x1307,
            0x1306,
            0x1022,
            0x1021,
            0x104C,
            0x2010,
            0x200F,
            0x1309,
            0x1308,
            0x1311,
            0x1310,
            0x200E,
            0x200D,
          ]
        uint: enforce
        sensors:
          - registers: [0x1307, 0x1306]
          - registers: [0x1022, 0x1021]
            scale: 1
          - registers: [0x104C]
            scale: 0.001
          - registers: [0x2010, 0x200F]
            validation:
              max: 4294967
          - operator: subtract
            registers: [0x1309, 0x1308]
          - operator: subtract
            registers: [0x1311, 0x1310]
          - operator: subtract
            registers: [0x200E, 0x200D]
            validation:
              max: 4294967
        validation:
          min: 1
```

Today losses:
```
      - name: "Today Losses"
        alt: "Daily Losses"
        friendly_name: "Today's Losses"
        description: "Includes today's consumption of the inverter device itself as well AC/DC conversion losses"
        class: "energy"
        state_class: "total_increasing"
        ensure_increasing:
        uom: "kWh"
        rule: 1
        scale: 0.01
        digits: 1
        registers:
          [
            0x1333,
            0x1332,
            0x1028,
            0x1027,
            0x2010,
            0x200F,
            0x1335,
            0x1334,
            0x1337,
            0x1336,
            0x200C,
            0x200B,
          ]
        uint: enforce
        sensors:
          - registers: [0x1333, 0x1332]
          - registers: [0x1028, 0x1027]
            scale: 0.001
          - registers: [0x2010, 0x200F]
          - operator: subtract
            registers: [0x1335, 0x1334]
          - operator: subtract
            registers: [0x1337, 0x1336]
          - operator: subtract
            registers: [0x200C, 0x200B]
```

## entity validation and range

You should add proper range and validation to entities, so that invalid values will not pollute your device history.

**range** is used to limit the input value from the inverted, while **validation** is used to validate the parsed entity data after applying scaling and unit of measure conversions.

Exmaple:
```
      - name: "EPS Total energy" # aka "Accumulated energy to EPS"
        class: "energy"
        state_class: "total_increasing"
        uom: "kWh"
        scale: 0.01
        rule: 3
        registers: [0x1363, 0x1362]
        range:
          max: 0xFFFFFFF9
        validation:
          min: 0.01
```

This entity value is sent by the inverter ad 10Wh increments, and an invalid value (EPS not present) is sent as 0xFFFFFFFA. Thus, the value is first filtered out with a maximum range of 0xFFFFFFF9 (0xFFFFFFFA-1) then scaled 
to kWh by a demultiplication factor of 0.01 (10Wh * 0.01 = 1kWh) and finally validated with a minimum valid of 0.01kWh.

## Write only and read/write entities

You can add them, if your inverter support them, but in this case you **must** also test them yourself. If you don't feel confident with this, just leave them out. For Home Assistant energy dashboard to operate, you only need the read-only reigsters anyway.


# Step 2: testing the YAML

Before submitting the new yaml, please test it yourself. You need to make sure that:
- all info entities show valid values
- all non-existent ufnctionalities shows "Unknown" or "0" as value (no strange values!)
- The sensors can be added to the energy dashboard and they properly represent your PV and grid data

As a guideline, open up your Solarman app and check the data between that and Home Assistant. Keep in mind that **total** values are periodically reset, so the total values shown in Solarman will not match Home Assistant values.


# Step 3: the Pull Request

When done, open a pull request on GitHub. Clone the ha_solarman repo in your account, add the new yaml file, commnit and open the PR on this project.








