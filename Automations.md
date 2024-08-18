_Change 'entity_ids' in following automations accordingly_ 😉

# Inverter Grid Charging Program
**Description**: On Solar forecast change and During T2 set Program 1 SOC  
**Requirements**: Program 1 Time set to match T2  
**Dependency**: Solcast PV Forecast
```
alias: Inverter Grid Charging Program
description: Charge battery during T2 on bad solar forecast
trigger:
  - platform: time
    at: sensor.sun_next_dawn
  - platform: template
    value_template: >-
      {% if states('sensor.solcast_pv_forecast_forecast_today') | float > 0
      %}true{% endif %}
condition:
  - condition: time
    after: "03:00:00"
    before: "06:00:00"
  - condition: state
    entity_id: input_select.grid_metrics_tariff
    state: T2
action:
  - choose:
      - conditions:
          - condition: numeric_state
            entity_id: sensor.solcast_pv_forecast_forecast_today
            above: 50
        sequence:
          - metadata: {}
            data:
              value: "20"
            target:
              entity_id: number.inverter_program_1_soc
            action: number.set_value
      - conditions:
          - condition: numeric_state
            entity_id: sensor.solcast_pv_forecast_forecast_today
            above: 40
        sequence:
          - metadata: {}
            data:
              value: "25"
            target:
              entity_id: number.inverter_program_1_soc
            action: number.set_value
      - conditions:
          - condition: numeric_state
            entity_id: sensor.solcast_pv_forecast_forecast_today
            above: 30
        sequence:
          - metadata: {}
            data:
              value: "50"
            target:
              entity_id: number.inverter_program_1_soc
            action: number.set_value
      - conditions:
          - condition: numeric_state
            entity_id: sensor.solcast_pv_forecast_forecast_today
            below: 25
        sequence:
          - metadata: {}
            data:
              value: "90"
            target:
              entity_id: number.inverter_program_1_soc
            action: number.set_value
      - conditions:
          - condition: numeric_state
            entity_id: sensor.solcast_pv_forecast_forecast_today
            below: 15
        sequence:
          - metadata: {}
            data:
              value: "98"
            target:
              entity_id: number.inverter_program_1_soc
            action: number.set_value
    default:
      - metadata: {}
        data:
          value: "70"
        target:
          entity_id: number.inverter_program_1_soc
        action: number.set_value
mode: single
```

# Inverter Grid Charging Reset
**Description**: At start of every day reset Program 1/3/5 SOC
```
alias: Inverter Grid Charging Reset
description: Resets Program 1/3/5 SOC to default values inverter control
trigger:
  - platform: time
    at: "00:00:00"
condition: []
action:
  - action: number.set_value
    metadata: {}
    data:
      value: "30"
    target:
      entity_id: number.inverter_program_1_soc
  - action: number.set_value
    metadata: {}
    data:
      value: "90"
    target:
      entity_id: number.inverter_program_3_soc
  - action: number.set_value
    metadata: {}
    data:
      value: "60"
    target:
      entity_id: number.inverter_program_5_soc
mode: single
```

# Inverter Grid Export Surplus
**Description**: Control energy surplus export according current spot price  
**Dependency**: Czech Energy Spot Prices
```
alias: Inverter Grid Export Surplus
description: Export Surplus when non negative spot price
trigger:
  - platform: template
    value_template: "{% if has_value('sensor.current_spot_electricity_price') %}true{% endif %}"
condition: []
action:
  - choose:
      - conditions:
          - condition: numeric_state
            entity_id: sensor.current_spot_electricity_price
            below: 0
          - condition: state
            entity_id: switch.inverter_grid_export_surplus
            state: "on"
        sequence:
          - service: switch.turn_off
            metadata: {}
            data: {}
            target:
              entity_id: switch.inverter_grid_export_surplus
      - conditions:
          - condition: numeric_state
            entity_id: sensor.current_spot_electricity_price
            above: 0
          - condition: state
            entity_id: switch.inverter_grid_export_surplus
            state: "off"
        sequence:
          - service: switch.turn_on
            metadata: {}
            data: {}
            target:
              entity_id: switch.inverter_grid_export_surplus
mode: single
```