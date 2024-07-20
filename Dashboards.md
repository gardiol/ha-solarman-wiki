# Horseshoe gauges
![wiki_1_1](https://github.com/user-attachments/assets/323eb0fd-9409-49fb-9577-12b6241d7faf)

_Change 'entitys' in following snippet accordingly_ 😉

**Dependency**: Flexible Horseshoe Card for Lovelace, card-mod, Solcast PV Forecast integration (for 'REMAINING')
```
  - title: Energy
    path: energy
    icon: mdi:flash
    type: sections
    sections:
      - type: grid
        cards:
          - type: custom:flex-horseshoe-card
            view_layout:
              grid-area: g3
            entities:
              - entity: sensor.inverter_grid_power
                unit: W
                decimals: 0
                name: Grid
              - entity: sensor.inverter_grid_l1_power
                decimals: 0
                unit: W
              - entity: sensor.inverter_grid_l1_voltage
                decimals: 1
                unit: V
              - entity: sensor.inverter_grid_l2_power
                decimals: 0
                unit: W
              - entity: sensor.inverter_grid_l2_voltage
                decimals: 1
                unit: V
              - entity: sensor.inverter_grid_l3_power
                decimals: 0
                unit: W
              - entity: sensor.inverter_grid_l3_voltage
                decimals: 1
                unit: V
              - entity: sensor.inverter_inverter_frequency
                decimals: 2
                unit: Hz
              - entity: sensor.grid_metrics_total_cost
                decimals: 2
                unit: CZK
                name: Price per kWh
              - entity: sensor.grid_today_energy_sold
                unit: kWh
                name: Export
              - entity: sensor.grid_today_energy_bought
                unit: kWh
                name: Import
            show:
              horseshoe_style: autominmax
            layout:
              hlines:
                - id: 0
                  xpos: 50
                  ypos: 40
                  length: 70
                  styles:
                    - stroke: rgb(59, 60, 62);
                - id: 1
                  xpos: 50
                  ypos: 60
                  length: 70
                  styles:
                    - stroke: rgb(59, 60, 62);
              vlines:
                - id: 0
                  xpos: 37
                  ypos: 50
                  length: 18
                  styles:
                    - stroke: rgb(59, 60, 62);
                    - stroke-linecap: square;
                - id: 1
                  xpos: 63
                  ypos: 50
                  length: 18
                  styles:
                    - stroke: rgb(59, 60, 62);
                    - stroke-linecap: square;
              states:
                - id: 0
                  entity_index: 0
                  xpos: 50
                  ypos: 34
                  styles:
                    - font-size: 3em;
                    - opacity: 0.9;
                - id: 1
                  entity_index: 1
                  xpos: 34
                  ypos: 49
                  styles:
                    - font-size: 1.2em;
                    - text-anchor: end;
                - id: 2
                  entity_index: 2
                  xpos: 34
                  ypos: 56
                  styles:
                    - font-size: .9em;
                    - text-anchor: end;
                - id: 3
                  entity_index: 3
                  xpos: 51
                  ypos: 49
                  styles:
                    - font-size: 1.2em;
                - id: 4
                  entity_index: 4
                  xpos: 51
                  ypos: 56
                  styles:
                    - font-size: .9em;
                - id: 5
                  entity_index: 5
                  xpos: 66
                  ypos: 49
                  styles:
                    - font-size: 1.2em;
                    - text-anchor: start;
                - id: 6
                  entity_index: 6
                  xpos: 66
                  ypos: 56
                  styles:
                    - font-size: .9em;
                    - text-anchor: start;
                - id: 7
                  entity_index: 7
                  xpos: 50
                  ypos: 16
                  styles:
                    - font-size: .8em;
                - id: 8
                  entity_index: 8
                  xpos: 50
                  ypos: 75
                  styles:
                    - font-size: 2em;
                - id: 9
                  entity_index: 9
                  xpos: 100
                  ypos: 5
                  styles:
                    - text-anchor: end;
                    - font-size: 1.1em;
                - id: 10
                  entity_index: 10
                  xpos: 0
                  ypos: 5
                  styles:
                    - text-anchor: start;
                    - font-size: 1.1em;
              names:
                - id: 0
                  entity_index: 0
                  xpos: 50
                  ypos: 95
                  styles:
                    - font-size: 1.2em;
                - id: 1
                  entity_index: 8
                  xpos: 50
                  ypos: 80
                  styles:
                    - font-size: 0.5em;
                - id: 2
                  entity_index: 9
                  xpos: 100
                  ypos: 9
                  styles:
                    - font-size: 0.5em;
                    - text-anchor: end;
                - id: 3
                  entity_index: 10
                  xpos: 0
                  ypos: 9
                  styles:
                    - font-size: 0.5em;
                    - text-anchor: start;
            horseshoe_scale:
              min: 0
              max: 12000
              width: 6
            color_stops:
              '0': '#488fc2'
              '2000': '#488fc2'
            card_mod:
              style: |
                ha-card {
                  --ha-card-background: var(--card-background-color);
                  color: var(--primary-color); 
                }
      - type: grid
        cards:
          - type: custom:flex-horseshoe-card
            view_layout:
              grid-area: g1
            entities:
              - entity: sensor.inverter_pv_power
                decimals: 0
                unit: W
                name: Solar
              - entity: sensor.inverter_pv1_power
                decimals: 0
                unit: W
                name: East
              - entity: sensor.inverter_pv2_power
                decimals: 0
                unit: W
                name: West
              - entity: sensor.inverter_pv1_voltage
                decimals: 1
                unit: V
              - entity: sensor.inverter_pv2_voltage
                decimals: 1
                unit: V
              - entity: sensor.inverter_pv1_current
                decimals: 1
                unit: A
              - entity: sensor.inverter_pv2_current
                decimals: 1
                unit: A
              - entity: sensor.inverter_today_production
                unit: kWh
                name: Production
              - entity: sensor.solcast_pv_forecast_forecast_remaining_today
                unit: kWh
                name: Remaining
            show:
              horseshoe_style: autominmax
            layout:
              hlines:
                - id: 0
                  xpos: 50
                  ypos: 40
                  length: 70
                  styles:
                    - stroke: rgb(59, 60, 62);
              vlines:
                - id: 0
                  xpos: 50
                  ypos: 60
                  length: 39
                  styles:
                    - stroke: rgb(59, 60, 62);
              states:
                - id: 0
                  entity_index: 0
                  xpos: 50
                  ypos: 34
                  styles:
                    - font-size: 3em;
                    - opacity: 0.9;
                - id: 1
                  entity_index: 1
                  xpos: 44
                  ypos: 55
                  styles:
                    - font-size: 1.6em;
                    - text-anchor: end;
                - id: 2
                  entity_index: 2
                  xpos: 56
                  ypos: 55
                  styles:
                    - text-anchor: start;
                    - font-size: 1.6em;
                - id: 3
                  entity_index: 3
                  xpos: 44
                  ypos: 65
                  styles:
                    - text-anchor: end;
                    - font-size: 1.3em;
                - id: 4
                  entity_index: 4
                  xpos: 56
                  ypos: 65
                  styles:
                    - text-anchor: start;
                    - font-size: 1.3em;
                - id: 5
                  entity_index: 5
                  xpos: 44
                  ypos: 75
                  styles:
                    - text-anchor: end;
                    - font-size: 1.3em;
                - id: 6
                  entity_index: 6
                  xpos: 56
                  ypos: 75
                  styles:
                    - text-anchor: start;
                    - font-size: 1.3em;
                - id: 7
                  entity_index: 7
                  xpos: 0
                  ypos: 5
                  styles:
                    - text-anchor: start;
                    - font-size: 1.1em;
                - id: 8
                  entity_index: 8
                  xpos: 100
                  ypos: 5
                  styles:
                    - text-anchor: end;
                    - font-size: 1.1em;
              icons:
                - id: 0
                  entity_index: 0
                  xpos: 50
                  ypos: 15
                  align: center
                  icon_size: 1.2
                  styles:
                    - color: orange;
              names:
                - id: 0
                  entity_index: 0
                  xpos: 50
                  ypos: 95
                  styles:
                    - font-size: 1.2em;
                - id: 1
                  entity_index: 1
                  xpos: 15
                  ypos: 45
                  styles:
                    - text-anchor: start;
                    - font-size: 0.5em;
                - id: 2
                  entity_index: 2
                  xpos: 85
                  ypos: 45
                  styles:
                    - text-anchor: end;
                    - font-size: 0.5em;
                - id: 3
                  entity_index: 7
                  xpos: 0
                  ypos: 9
                  styles:
                    - text-anchor: start;
                    - font-size: 0.5em;
                - id: 4
                  entity_index: 8
                  xpos: 100
                  ypos: 9
                  styles:
                    - font-size: 0.5em;
                    - text-anchor: end;
            horseshoe_scale:
              min: 0
              max: 12000
              width: 6
            color_stops:
              '0': orange
              '2000': orange
            card_mod:
              style: |
                ha-card {
                  --ha-card-background: var(--card-background-color);
                  color: var(--primary-color); 
                }
          - type: custom:flex-horseshoe-card
            view_layout:
              grid-area: g2
            entities:
              - entity: sensor.inverter_battery_power
                decimals: 0
                unit: W
                name: Battery
              - entity: sensor.inverter_battery_voltage
                decimals: 2
                unit: V
              - entity: sensor.inverter_battery_current
                decimals: 2
                unit: A
              - entity: sensor.inverter_battery
                decimals: 0
                unit: '%'
              - entity: sensor.inverter_battery_state
              - entity: sensor.inverter_today_battery_life_cycles
                decimals: 1
              - entity: sensor.inverter_battery_soh
                decimals: 1
              - entity: sensor.inverter_battery_temperature
                decimals: 1
                unit: °C
              - entity: sensor.inverter_today_battery_discharge
                unit: kWh
                name: Discharge
              - entity: sensor.inverter_today_battery_charge
                unit: kWh
                name: Charge
            show:
              horseshoe_style: autominmax
            layout:
              hlines:
                - id: 0
                  xpos: 50
                  ypos: 40
                  length: 70
                  styles:
                    - stroke: rgb(59, 60, 62);
                - id: 0
                  xpos: 50
                  ypos: 60
                  length: 70
                  styles:
                    - stroke: rgb(59, 60, 62);
              vlines:
                - id: 0
                  xpos: 50
                  ypos: 50
                  length: 18
                  styles:
                    - stroke: rgb(59, 60, 62);
                    - stroke-linecap: square;
              states:
                - id: 0
                  entity_index: 0
                  xpos: 50
                  ypos: 34
                  styles:
                    - font-size: 3em;
                    - opacity: 0.9;
                - id: 1
                  entity_index: 1
                  xpos: 44
                  ypos: 53
                  styles:
                    - font-size: 1.4em;
                    - text-anchor: end;
                - id: 2
                  entity_index: 2
                  xpos: 56
                  ypos: 53
                  styles:
                    - text-anchor: start;
                    - font-size: 1.4em;
                - id: 3
                  entity_index: 3
                  xpos: 50
                  ypos: 75
                  styles:
                    - font-size: 2em;
                - id: 4
                  entity_index: 4
                  xpos: 50
                  ypos: 80
                  styles:
                    - font-size: 0.5em;
                    - text-transform: uppercase;
                - id: 5
                  entity_index: 5
                  xpos: 21
                  ypos: 65
                  styles:
                    - text-anchor: start;
                    - font-size: .7em;
                - id: 6
                  entity_index: 6
                  xpos: 85
                  ypos: 65
                  styles:
                    - text-anchor: end;
                    - font-size: .7em;
                - id: 7
                  entity_index: 7
                  xpos: 50
                  ypos: 16
                  styles:
                    - font-size: .8em;
                - id: 8
                  entity_index: 8
                  xpos: 100
                  ypos: 5
                  styles:
                    - text-anchor: end;
                    - font-size: 1.1em;
                - id: 9
                  entity_index: 9
                  xpos: 0
                  ypos: 5
                  styles:
                    - text-anchor: start;
                    - font-size: 1.1em;
              icons:
                - id: 0
                  entity_index: 5
                  xpos: 4
                  ypos: 65.5
                  align: start
                  size: 0
                  styles:
                    - color: white;
                    - '--mdc-icon-size': 0.65em;
                - id: 0
                  entity_index: 6
                  xpos: 80
                  ypos: 65.5
                  align: end
                  size: 0
                  styles:
                    - color: white;
                    - '--mdc-icon-size': 0.65em;
              names:
                - id: 0
                  entity_index: 0
                  xpos: 50
                  ypos: 95
                  styles:
                    - font-size: 1.2em;
                - id: 1
                  entity_index: 8
                  xpos: 100
                  ypos: 9
                  styles:
                    - font-size: 0.5em;
                    - text-anchor: end;
                - id: 2
                  entity_index: 9
                  xpos: 0
                  ypos: 9
                  styles:
                    - font-size: 0.5em;
                    - text-anchor: start;
            horseshoe_scale:
              min: 0
              max: 7500
              width: 6
            color_stops:
              '0': pink
              '2000': pink
            card_mod:
              style: |
                ha-card {
                  --ha-card-background: var(--card-background-color);
                  color: var(--primary-color);
                }
      - type: grid
        cards:
          - type: custom:flex-horseshoe-card
            view_layout:
              grid-area: g3
            entities:
              - entity: sensor.inverter_load_power
                unit: W
                decimals: 0
                name: Load
              - entity: sensor.inverter_load_l1_power
                decimals: 0
                unit: W
              - entity: sensor.inverter_load_l1_voltage
                decimals: 1
                unit: V
              - entity: sensor.inverter_load_l2_power
                decimals: 0
                unit: W
              - entity: sensor.inverter_load_l2_voltage
                decimals: 1
                unit: V
              - entity: sensor.inverter_load_l3_power
                decimals: 0
                unit: W
              - entity: sensor.inverter_load_l3_voltage
                decimals: 1
                unit: V
              - entity: sensor.inverter_temperature
                unit: °C
              - entity: sensor.inverter_power_losses
                decimals: 0
                unit: W
                name: Losses
              - entity: sensor.inverter_today_losses
                unit: kWh
                name: Losses
              - entity: sensor.inverter_today_load_consumption
                unit: kWh
                name: Consumption
            show:
              horseshoe_style: autominmax
            layout:
              hlines:
                - id: 0
                  xpos: 50
                  ypos: 40
                  length: 70
                  styles:
                    - stroke: rgb(59, 60, 62);
                - id: 1
                  xpos: 50
                  ypos: 60
                  length: 70
                  styles:
                    - stroke: rgb(59, 60, 62);
              vlines:
                - id: 0
                  xpos: 37
                  ypos: 50
                  length: 18
                  styles:
                    - stroke: rgb(59, 60, 62);
                    - stroke-linecap: square;
                - id: 1
                  xpos: 63
                  ypos: 50
                  length: 18
                  styles:
                    - stroke: rgb(59, 60, 62);
                    - stroke-linecap: square;
              states:
                - id: 0
                  entity_index: 0
                  xpos: 50
                  ypos: 34
                  styles:
                    - font-size: 3em;
                    - opacity: 0.9;
                - id: 1
                  entity_index: 1
                  xpos: 34
                  ypos: 49
                  styles:
                    - font-size: 1.2em;
                    - text-anchor: end;
                - id: 2
                  entity_index: 2
                  xpos: 34
                  ypos: 56
                  styles:
                    - font-size: .9em;
                    - text-anchor: end;
                - id: 3
                  entity_index: 3
                  xpos: 51
                  ypos: 49
                  styles:
                    - font-size: 1.2em;
                - id: 4
                  entity_index: 4
                  xpos: 51
                  ypos: 56
                  styles:
                    - font-size: .9em;
                - id: 5
                  entity_index: 5
                  xpos: 66
                  ypos: 49
                  styles:
                    - font-size: 1.2em;
                    - text-anchor: start;
                - id: 6
                  entity_index: 6
                  xpos: 66
                  ypos: 56
                  styles:
                    - font-size: .9em;
                    - text-anchor: start;
                - id: 7
                  entity_index: 7
                  xpos: 50
                  ypos: 16
                  styles:
                    - font-size: .8em;
                - id: 8
                  entity_index: 8
                  xpos: 50
                  ypos: 75
                  styles:
                    - font-size: 2em;
                - id: 9
                  entity_index: 9
                  xpos: 100
                  ypos: 5
                  styles:
                    - text-anchor: end;
                    - font-size: 1.1em;
                - id: 10
                  entity_index: 10
                  xpos: 0
                  ypos: 5
                  styles:
                    - text-anchor: start;
                    - font-size: 1.1em;
              icons:
                - id: 0
                  entity_index: 1
                  xpos: 30
                  ypos: 52
                  align: start
                  size: 1
              names:
                - id: 0
                  entity_index: 0
                  xpos: 50
                  ypos: 95
                  styles:
                    - font-size: 1.2em;
                - id: 1
                  entity_index: 8
                  xpos: 50
                  ypos: 80
                  styles:
                    - font-size: 0.5em;
                - id: 2
                  entity_index: 9
                  xpos: 100
                  ypos: 9
                  styles:
                    - font-size: 0.5em;
                    - text-anchor: end;
                - id: 3
                  entity_index: 10
                  xpos: 0
                  ypos: 9
                  styles:
                    - font-size: 0.5em;
                    - text-anchor: start;
            horseshoe_scale:
              min: 0
              max: 12000
              width: 6
            color_stops:
              '0': '#5fb6ad'
              '2000': '#5fb6ad'
            card_mod:
              style: |
                ha-card {
                  --ha-card-background: var(--card-background-color);
                  color: var(--primary-color); 
                }
    cards: []
    max_columns: 3
```