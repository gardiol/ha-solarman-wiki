_Custom sensor examples._

# PV Power [W]
**Description**: Sensor can be also defined as a sum of multiple registers so this is how to sum PV1 power + PV2 power + ...
```
- name: PV Power
  description: Combined power of all inputs
  realtime:
  class: power
  state_class: measurement
  uom: W
  rule: 1
  digits: 0
  registers: [0x02A0, 0x02A1, 0x02A2, 0x02A3]
  sensors:
    - registers: [0x02A0]
    - registers: [0x02A1]
    - registers: [0x02A2]
    - registers: [0x02A3]
  icon: mdi:solar-power-variant
```

# Power losses [W]
**Description**: Calculates power losses of the installation (Device consumption + AC/DC conversion losses)
```
- name: Power losses
  description: Includes consumption of the inverter device itself as well AC/DC conversion losses
  class: power
  state_class: measurement
  uom: W
  rule: 1
  digits: 0
  registers: [0x024E, 0x02A0, 0x02A1, 0x02A2, 0x02A3, 0x027C, 0x02B6]
  uint: enforce
  sensors:
    - signed:
      registers: [0x024E]
    - registers: [0x02A0]
    - registers: [0x02A1]
    - registers: [0x02A2]
    - registers: [0x02A3]
    - subtract:
      signed:
      registers: [0x027C, 0x02B6]
```

# Today Losses [kWh]
**Description**: Calculates today's energy losses from Today(Daily) sensors of the inverter
```
- name: Today Losses
  description: Includes today's consumption of the inverter device itself as well AC/DC conversion losses
  class: energy
  state_class: total_increasing
  uom: kWh
  rule: 1
  digits: 1
  registers: [0x0208, 0x0211, 0x0203, 0x0209, 0x020E, 0x0202]
  sensors:
    - scale: 0.1
      registers: [0x0208]
    - scale: 0.1
      registers: [0x0211]
    - scale: 0.1
      registers: [0x0203]
    - subtract:
      scale: 0.1
      registers: [0x0209]
    - subtract:
      scale: 0.1
      registers: [0x020E]
    - subtract:
      scale: 0.1
      registers: [0x0202]
```

# Total Losses [kWh]
**Description**: Calculates total energy losses from Total sensors of the inverter
```
- name: Total Losses
  description: Includes total consumption of the inverter device itself as well AC/DC conversion losses
  class: energy
  state_class: total_increasing
  uom: kWh
  rule: 3
  digits: 1
  registers:
    [
      0x020A,
      0x020B,
      0x0216,
      0x0217,
      0x0206,
      0x0207,
      0x020C,
      0x020D,
      0x020F,
      0x0210,
      0x0204,
      0x0205,
    ]
  sensors:
    - scale: 0.1
      registers: [0x020A, 0x020B]
    - scale: 0.1
      registers: [0x0216, 0x0217]
    - scale: 0.1
      registers: [0x0206, 0x0207]
    - subtract:
      scale: 0.1
      registers: [0x020C, 0x020D]
    - subtract:
      scale: 0.1
      registers: [0x020F, 0x0210]
    - subtract:
      scale: 0.1
      registers: [0x0204, 0x0205]
```

# Today Consumption [kWh]
**Description**: Calculates today's energy consumption
```
- name: Today Consumption
  alt: Daily Consumption
  description: Includes today's house consumption as well inverter consumption and AC/DC conversion losses
  class: energy
  state_class: total_increasing
  uom: kWh
  rule: 1
  digits: 1
  registers: [0x0208, 0x0211, 0x0203, 0x0209, 0x0202]
  sensors:
    - scale: 0.1
      registers: [0x0208]
    - scale: 0.1
      registers: [0x0211]
    - scale: 0.1
      registers: [0x0203]
    - subtract:
      scale: 0.1
      registers: [0x0209]
    - subtract:
      scale: 0.1
      registers: [0x0202]
```

# Total Consumption [kWh]
**Description**: Calculates total energy consumption
```
- name: Total Consumption
  description: Includes total house consumption as well inverter consumption and AC/DC conversion losses
  class: energy
  state_class: total_increasing
  uom: kWh
  rule: 3
  digits: 1
  registers:
    [
      0x020A,
      0x020B,
      0x0216,
      0x0217,
      0x0206,
      0x0207,
      0x020C,
      0x020D,
      0x0204,
      0x0205,
    ]
  sensors:
    - scale: 0.1
      registers: [0x020A, 0x020B]
    - scale: 0.1
      registers: [0x0216, 0x0217]
    - scale: 0.1
      registers: [0x0206, 0x0207]
    - subtract:
      scale: 0.1
      registers: [0x020C, 0x020D]
    - subtract:
      scale: 0.1
      registers: [0x0204, 0x0205]
```

# Battery Power ∇ [W]
**Description**: Inverts value of Battery Power (for cases where in/out separation needed). Also includes an example of entity_id differentiation (cause of the '∇')
```
- name: Battery Power ∇
  entity_id: battery_power_inverted
  class: power
  state_class: measurement
  uom: W
  scale: 1
  rule: 2
  inverted: True
  registers: [0x024E]
```