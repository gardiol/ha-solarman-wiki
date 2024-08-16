# 🐎 Horseshoe gauges
![wiki_1_1](https://github.com/user-attachments/assets/323eb0fd-9409-49fb-9577-12b6241d7faf)

**Dependency**: Flexible Horseshoe Card for Lovelace, card-mod, Solcast PV Forecast integration (for 'REMAINING')
<details>
  <summary>Code</summary>

  _Change 'entitys' in following snippet accordingly_ 😉
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

</details>

# ⚡ Power Flow Card Plus
![power_flow_card_plus](https://github.com/user-attachments/assets/a18ff34f-dc0e-49c9-aa65-4a1a3d83f518)

**Dependency**: Power Flow Card Plus, card-mod
<details>
  <summary>Code</summary>

  _Change 'entitys' in following snippet accordingly_ 😉
  ```
type: custom:power-flow-card-plus
entities:
  battery:
    entity: sensor.inverter_battery_power
    display_state: one_way_no_zero
    invert_state: false
    color_value: true
    use_metadata: true
    name: ' '
    state_of_charge_unit_white_space: false
    state_of_charge: sensor.inverter_battery
    color_icon: true
    color_circle: true
    display_zero_tolerance: 20
  grid:
    entity: sensor.inverter_grid_power
    display_state: one_way
    use_metadata: true
    color_icon: true
    color_value: true
    invert_state: false
    icon: mdi:transmission-tower
    color_circle: true
    name: ' '
    display_zero_tolerance: 0
    secondary_info:
      entity: sensor.grid_metrics_total_cost
      decimals: 2
      unit_of_measurement: ' '
    power_outage:
      entity: binary_sensor.inverter_grid
      state_alert: Clear
  solar:
    entity: sensor.inverter_pv_power
    display_state: one_way
    use_metadata: true
    display_zero_state: false
    invert_state: false
    color_icon: true
    secondary_info: {}
    name: ' '
    color_value: false
    icon: mdi:solar-power-variant
  home:
    entity: sensor.inverter_load_power
    override_state: true
    subtract_individual: false
    use_metadata: true
    name: ' '
    icon: ' '
    secondary_info:
      entity: sensor.inverter_power_losses
      icon: ''
  fossil_fuel_percentage: {}
clickable_entities: true
display_zero_lines:
  mode: transparency
  transparency: 75
  grey_color:
    - 189
    - 189
    - 189
use_new_flow_rate_model: true
w_decimals: 0
kw_decimals: 1
min_flow_rate: 0.75
max_flow_rate: 6
max_expected_power: 12000
min_expected_power: 0.01
watt_threshold: 1000
transparency_zero_lines: 0
dashboard_link: /energy
card_mod:
  style:
    .: >
      .home span.secondary-info, .grid span.secondary-info,
      span#battery-state-of-charge-text {
        font-size: 90%;
        color: var(--secondary-text-color) !important;
      }

  ```

</details>

# 📊 Apexcharts & Plotly Graph Card
![forecast_daily_stats_graphs](https://github.com/user-attachments/assets/b5ee4989-b57f-4657-a64a-92870b7161b9)

**Dependency**: Apexcharts-card, Plotly Graph Card, Solcast PV Forecast integration, card-mod
<details>
  <summary>Apexcharts code</summary>

  _Change 'entitys' in following snippet accordingly_ 😉
  ```
  type: custom:apexcharts-card
  view_layout:
    grid-area: solar
  header:
    show: true
    standard_format: true
    show_states: true
    colorize_states: true
  apex_config:
    grid:
      show: false
    chart:
      height: 400px
    tooltip:
      enabled: true
      shared: true
      followCursor: true
    xaxis:
      axisTicks:
        show: false
      axisBorder:
        show: false
  graph_span: 4d
  now:
    show: true
    label: Now
  span:
    start: day
    offset: '-1day'
  all_series_config:
    type: area
    opacity: 0.3
    stroke_width: 2
  series:
    - entity: sensor.inverter_battery
      name: Battery
      float_precision: 0
      type: line
      color: pink
      opacity: 0.8
      yaxis_id: capacity
      extend_to: now
      show:
        legend_value: true
        in_header: false
      group_by:
        func: last
        duration: 5m
    - entity: sensor.inverter_pv_power
      name: Solar Power
      float_precision: 3
      color: '#ff9800'
      yaxis_id: kWh
      unit: kW
      transform: return x/1000;
      extend_to: now
      show:
        legend_value: true
        in_header: false
      group_by:
        func: avg
        duration: 5m
    - entity: sensor.solcast_pv_forecast_forecast_today
      name: Today's Forecast
      extend_to: false
      color: grey
      opacity: 0.3
      stroke_width: 0
      yaxis_id: kWh
      show:
        legend_value: false
        in_header: false
      data_generator: |
        return entity.attributes.detailedForecast.map((entry) => {
              return [new Date(entry.period_start), entry.pv_estimate];
            });
    - entity: sensor.solcast_pv_forecast_forecast_tomorrow
      name: Tomorrow's Forecast
      float_precision: 3
      extend_to: false
      color: grey
      opacity: 0.3
      stroke_width: 0
      yaxis_id: kWh
      show:
        legend_value: false
        in_header: false
      data_generator: |
        return entity.attributes.detailedForecast.map((entry) => {
              return [new Date(entry.period_start), entry.pv_estimate];
            });
    - entity: sensor.solcast_pv_forecast_forecast_day_3
      name: Overmorrow's Forecast
      float_precision: 3
      extend_to: false
      color: grey
      opacity: 0.3
      stroke_width: 0
      yaxis_id: kWh
      show:
        legend_value: false
        in_header: false
      data_generator: |
        return entity.attributes.detailedForecast.map((entry) => {
              return [new Date(entry.period_start), entry.pv_estimate];
            });
    - entity: sensor.solcast_pv_forecast_forecast_today
      yaxis_id: header_only
      name: Today's Forecast
      color: grey
      show:
        legend_value: true
        in_header: true
        in_chart: false
    - entity: sensor.solcast_pv_forecast_forecast_remaining_today
      yaxis_id: header_only
      name: Remaining
      color: grey
      show:
        legend_value: true
        in_header: true
        in_chart: false
    - entity: sensor.solcast_pv_forecast_forecast_tomorrow
      yaxis_id: header_only
      name: Tomorrow's Forecast
      color: grey
      show:
        legend_value: true
        in_header: true
        in_chart: false
    - entity: sensor.solcast_pv_forecast_forecast_day_3
      yaxis_id: header_only
      name: Overmorrow's Forecast
      color: grey
      show:
        legend_value: true
        in_header: true
        in_chart: false
    - entity: sensor.solcast_pv_forecast_api_last_polled
      yaxis_id: header_only
      name: Last updated
      color: grey
      unit: ' min.'
      transform: return ((Date.now()) - (new Date(x).getTime())) / 60 / 60 / 24
      show:
        legend_value: true
        in_header: true
        in_chart: false
  yaxis:
    - id: capacity
      show: true
      opposite: true
      decimals: 0
      max: 100
      min: 0
      apex_config:
        tickAmount: 5
    - id: kWh
      show: true
      min: 0
      apex_config:
        tickAmount: 5
    - id: header_only
      show: false
  card_mod:
    style:
      .: |
        .apexcharts-tooltip {
          border: 0 !important;
          border-radius: 4px !important;
        }
        .apexcharts-tooltip-title {
          border-bottom: 0 !important;
        }
        .apexcharts-xaxistooltip {
          display: none;
        }
  ```

</details>

<details>
  <summary>Plotly code</summary>

  _Change 'entitys' in following snippet accordingly_ 😉
  ```
  type: custom:plotly-graph
  title: null
  time_offset: 12h
  hours_to_show: 5d
  refresh_interval: 120
  view_layout:
    grid-area: daily
  layout:
    xaxis:
      showgrid: false
    yaxis:
      showgrid: false
      fixedrange: true
    legend:
      bgcolor: rgba(0,0,0,0)
      itemsizing: constant
      font:
        size: 12
    height: 450
  config:
    displayModeBar: false
    scrollZoom: false
  entities:
    - entity: sensor.inverter_today_energy_sold
      statistic: state
      name: |
        $fn ({ ys,meta }) =>
          "💰 " + "Export" + " (" +ys[ys.length - 1]+"kWh)"
      period: day
      type: bar
      texttemplate: '%{y}'
      filters:
        - filter: i>0
      marker:
        color: rgb(162, 128, 219)
    - entity: sensor.inverter_today_energy_bought
      statistic: state
      name: |
        $fn ({ ys,meta }) =>
          "💡 " + "Import" + " (" +ys[ys.length - 1]+"kWh)"
      period: day
      type: bar
      texttemplate: '%{y}'
      filters:
        - filter: i>0
      marker:
        color: rgb(84, 144, 194)
    - entity: sensor.inverter_today_production
      statistic: state
      name: |
        $fn ({ ys,meta }) =>
          "☀️ " + "Solar" + " (" +ys[ys.length - 1]+"kWh)"
      period: day
      type: bar
      texttemplate: '%{y}'
      filters:
        - filter: i>0
      marker:
        color: rgb(255, 152, 0)
    - entity: sensor.inverter_today_load_consumption
      statistic: state
      name: |
        $fn ({ ys,meta }) =>
          "⚡ " + "Load" + " (" +ys[ys.length - 1]+"kWh)"
      period: day
      type: bar
      filters:
        - filter: i>0
      texttemplate: '%{y}'
      marker:
        color: rgb(95, 182, 173)
    - entity: sensor.inverter_today_battery_charge
      statistic: state
      name: |
        $fn ({ ys,meta }) =>
          "🔋 " + "Battery Charge" + " (" +ys[ys.length - 1]+"kWh)"
      period: day
      type: bar
      texttemplate: '%{y}'
      filters:
        - filter: i>0
      marker:
        color: rgb(240, 98, 146)
    - entity: sensor.inverter_today_battery_discharge
      statistic: state
      name: |
        $fn ({ ys,meta }) =>
          "🔋 " + "Battery Discharge" + " (" +ys[ys.length - 1]+"kWh)"
      period: day
      type: bar
      texttemplate: '%{y}'
      filters:
        - filter: i>0
      marker:
        color: pink
  ```

</details>