# Sunsynk-Power-Flow-Card
An animated Home Assistant card to emulate the Sunsynk power flow that's shown on the Inverter screen.

[![hacs_badge](https://img.shields.io/badge/HACS-Custom-41BDF5.svg?style=for-the-badge)](https://github.com/hacs/integration) ![GitHub release (latest by date)](https://img.shields.io/github/v/release/slipx06/sunsynk-power-flow-card?style=for-the-badge)

## Features
* Option to switch between two card styles: `lite` or `full`.
* Animated power flow based on positive/negative/zero sensor values. (Supports inverted battery and AUX power).
* Dynamic battery image based on SOC (empty->low->medium->high). 
* Grid connected status.
* Inverter status (standby, normal, self-test, alarm, fault).  
* Configurable battery size and shutdown SOC to calculate and display remaining battery runtime based on current battery usage. Can be toggled off.
* Daily Totals that can be toggled on or off.
* Hide all solar data if not installed or specify number of mppts in use.
* "Use Timer" setting and "Energy Pattern" setting (Priority Load or Priority Battery) shown as dynamic icons with ability to hide if not required.
* Panel mode for bigger card
* AUX and Non-essential can be hidden from the full card.
* Customisable - Change colours and inverter image

## Screenshots

![image](https://user-images.githubusercontent.com/7227275/236638326-b3f48d9c-1e26-4e68-a69e-8529f12ca44e.png)
![sunsynk-power-flow-lite](https://github.com/slipx06/sunsynk-power-flow-card/assets/7227275/ef9809ed-c060-4ea0-8ee3-094212329121)


*Lite Version*

![image](https://user-images.githubusercontent.com/7227275/236638211-a891a0e1-5142-41d8-8bc4-cac1cdbb740e.png)
![sunsynk-power-flow-full](https://github.com/slipx06/sunsynk-power-flow-card/assets/7227275/c5ed0518-a867-4804-90b7-36e2c90223a4)


*Full Version*

## Installation
The card can be installed manually or via HACS

### Manual Installation
1. Create a new directory under `www` and name it `sunsynk-power-flow-card` e.g www/sunsynk-power-flow-card/
2. Copy the `sunsynk-power-flow-card.js` into the directory
3. Add the resource to your Dashboard. You can append the filename with a `?ver=x` and increment x each time you download a new version to force a reload and avoid using a cached version. It is also a good idea to clear your browser cache.

![image](https://user-images.githubusercontent.com/7227275/235441241-93ab0c7d-341d-428f-8ca8-60ec932dde2d.png)

### Installation using HACS
[![hacs_badge](https://img.shields.io/badge/HACS-Custom-41BDF5.svg?style=for-the-badge)](https://github.com/hacs/integration)
You can add to HACS as a Custom Repo

## Usage
Add the `Custom: Sunsynk Power Flow Card` to your Dashboard view. 

![image](https://user-images.githubusercontent.com/7227275/235375690-65d17663-e117-4626-9151-1a41979a13b8.png)

### Card Options

![sunsynk-power-flow-config](https://github.com/slipx06/sunsynk-power-flow-card/assets/7227275/580e397a-289b-4361-90e5-6e76e20028cb)

The card requires that all of these attributes be defined. 

| Attribute | Default | Description |
| --- | --- | --- |
|type: | `custom:sunsynk-power-flow-card` | The custom card |
|cardstyle: | `lite` | Selects the card layout that is used  `lite, simple, full` |
|panel_mode:| `no` | Toggles panel mode removing any card height restrictions. For use with Panel(1 card) view types or grid layouts|
|inverter: |  | List of inverter attributes. See required [Inverter](#inverter) attributes below |
|battery: |  | List of battery attributes. See required [Battery](#battery) attributes below |
|solar: |  | List of solar attributes. See required [Solar](#solar) attributes below |
|load: |  | List of load attributes. See required [Load](#load) attributes below |
|grid: |  | List of grid attributes. See required [Grid](#grid) attributes below |
|entities:||List of sensor entities. See required [Entities](#entities) attributes below|

### Inverter
Requires the folowing:

| Attribute | Default | Description |
| --- | --- | --- |
|modern:| `no`| Changes the inverter image.|
|colour:| `'#959595'`| Changes the colour of the inverter. Hex codes (`'#66ff00'` etc) or names (`red`, `green`, `blue` etc) |


### Battery
Requires the folowing:

| Attribute | Default | Description |
| --- | --- | --- |
|energy: | `15960` | Total Battery Energy in Wh (e.g. 3 x 5.32kWh = 15960). If set to `hidden` the remaining battery runtime will be hidden|
|shutdown_soc: | `20` |The battery shutdown percentage used to calculate remaining runtime |
|invert_power:| `no`|Set to `yes` if your sensor provides a positive number for battery charge and negative number for battery discharge|
|colour:| `pink`| Changes the colour of all the battery card objects. Hex codes (`'#66ff00'` etc) or names (`red`, `green`, `blue` etc) |
|show_daily: | `yes` | Toggles the Daily Total `yes/no` |

### Solar
Requires the folowing:

| Attribute | Default | Description |
| --- | --- | --- |
|show_solar:| `yes` | Toggle display of solar information `yes/no`|
|colour:| `orange`| Changes the colour of all the solar card objects. Hex codes (`'#66ff00'` etc) or names (`red`, `green`, `blue` etc) |
|show_daily: | `yes` | Toggles the Daily Total `yes/no` |
|mppts: | `two` | Specify the number of MPPT's in use `one`, `two`, `three` or `four` |

### Load
Requires the folowing:

| Attribute | Default | Description |
| --- | --- | --- |
|colour:| `'#5fb6ad'`| Changes the colour of all the load card objects. Hex codes (`'#66ff00'` etc) or names (`red`, `green`, `blue` etc) |
|show_daily: | `yes` | Toggles the Daily Total `yes/no` Only displayed if `show_aux` is set to `no` |
|show_aux: | `yes` | Toggles the display of Aux `yes/no` |
|invert_aux: | `no` | Set to `yes` if your sensor provides a positive number for AUX input and negative number for AUX output  |


### Grid
Requires the folowing:

| Attribute | Default | Description |
| --- | --- | --- |
|colour:| `'#5490c2'`| Changes the colour of all the grid card objects. Hex codes (`'#66ff00'` etc) or names (`red`, `green`, `blue` etc) |
|no_grid_colour:|`'#a40013'`|Changes the colour of the grid disconnected icon. Hex codes (`'#66ff00'` etc) or names (`red`, `green`, `blue` etc)|
|show_daily_buy: | `yes` | Toggles the Daily Buy Total `yes/no` |
|show_daily_sell: | `no` | Toggles the Daily Sell Total `yes/no` |
|show_nonessential: | `yes` | Toggles the display of Non-Essential `yes/no`|

### Entities
Entity attributes below have been appended with the modbus register # e.g. `pv2_power_187` to indicate which Sunsynk register should be read when configuring your sensors. Replace the default sensors with your own specific sensor names. It is important that your sensors read the expected modbus register value. If you have missing sensors for any attribute set it to none i.e. `solarday_108: none` and it will use a default value of 0.

| Attribute | Default | Description |
| --- | --- | --- |
|use_timer_248: | `switch.toggle_system_timer` | Displays "Use timer" status as an icon next to the inverter. Set to `no` to hide |
|priority_load_243: | `switch.toggle_priority_load` | Shows if energy pattern is set to Priority Load or Priority Battery as an icon next to the inverter. Set to `no` to hide|
|batdischargeday_71: | `sensor.battery_discharge_day` | Daily Battery Usage (kWh) |
|batchargeday_70: | `sensor.battery_charge_day` | Daily Battery Charge (kWh) |
|loadday_84: | `sensor.daily_load_power_kwh` | Daily Load (kWh) |
|grid_buy_day_76: | `sensor.grid_import_day_buy` | Daily Grid Import (kWh) |
|grid_sell_day_77: | `sensor.grid_export_day_sell` | Daily Grid Export (kWh) |
|solarday_108: | `sensor.daily_pv_power_kwh` | Daily Solar Usage (kWh |
|inverter_grid_voltage_154: | `sensor.grid_inverter_voltage` | Grid Voltage (V) |
|inverter_load_freq_192: | `sensor.load_frequency` | Load Frequency (Hz) |
|inverter_out_164: | `sensor.inverter_output_current` | Inverter Output Current (A) |
|inverter_out_175: | `sensor.inverter_output_power` | Inverter Output Power (W) |
|inverter_load_grid_169: | `sensor.grid_inverter_load` | Inverter Load (W) |
|pv1_power_186: | `sensor.pv1_power` | PV String 1 Power (W)|
|pv2_power_187: | `sensor.pv2_power` | PV String 2 Power (W)  |
|pv3_power_188: | `sensor.pv3_power` | PV String 3 Power (W)  |
|pv4_power_189: | `sensor.pv4_power` | PV String 4 Power (W)  |
|battery_voltage_183: | `sensor.battery_voltage` | Battery Voltage (V) |
|battery_soc_184: | `sensor.battery_soc` | Battery State of Charge (%) |
|battery_out_190: | `sensor.battery_output_power` | Battery Output Power (W). Requires a negative number for battery charging and a positive number for battery discharging. Set the `invert_power:` battery attribute to `yes` if your sensor reports this the other way around |
|ess_power: | `sensor.sunsynk_essential_load` | This sensor is only used for the simple and lite cards. You can use register 178. It is automatically calculated for the full card based on other attributes. (W) |
|grid_external_power_172: | `sensor.grid_external_power`  | Grid External Power (W)|
|pv1_v_109: | `sensor.dc1_voltage` | PV String 1 Voltage (V) |
|pv1_i_110: | `sensor.dc1_current` | PV String 1 Current (A)|
|pv2_v_111: | `sensor.dc2_voltage` | PV String 2 Voltage (V)|
|pv2_i_112: | `sensor.dc2_current` | PV String 2 Current (A)|
|pv3_v_113: | `sensor.dc3_voltage` | PV String 3 Voltage (V) |
|pv3_i_114: | `sensor.dc3_current` | PV String 3 Current (A)|
|pv4_v_115: | `sensor.dc4_voltage` | PV String 4 Voltage (V)|
|pv4_i_116: | `sensor.dc4_current` | PV String 4 Current (A)|
|grid_status_194: | `binary_sensor.grid_connected_status` | Grid Connected Status `on/off` or `1/0` |
|inverter_status_59: | `sensor.overall_state` | Inverter Status `0, 1, 2, 3, 4` or `standby, selftest, normal, alarm, fault` |
|aux_power_166: | `sensor.aux_output_power` | Auxilary Power (W) |

The card calculates the sensors below based on supplied attributes in the config so you dont need to define them in Home Assistant
 
 ```
 totalsolar = pv1_power_186 + pv2_power_187 + pv3_power_188 + pv4_power_189
 nonessential = grid_external_power_172 - inverter_load_grid_169
 essential = inverter_out_175 - (aux_power_166 - inverter_load_grid_169 )
 ```
The modbus registers can be visualised on the `full` card below:

![image](https://user-images.githubusercontent.com/7227275/235479493-b322d5b2-f2b1-431f-9048-f845fc2989b4.png)


### Example Card Configuration

```
type: custom:sunsynk-power-flow-card
cardstyle: full
panel_mode: 'no'
inverter:
  modern: 'yes'
  colour: '#959595'
battery:
  energy: 15960
  shutdown_soc: 20
  invert_power: 'no'
  colour: pink
  show_daily: 'yes'
solar:
  show_solar: 'yes'
  colour: orange
  show_daily: 'yes'
  mppts: two
load:
  colour: '#5fb6ad'
  show_daily: 'yes'
  show_aux: 'yes'
  invert_aux: 'no'
grid:
  colour: '#5490c2'
  show_daily_buy: 'yes'
  show_daily_sell: 'yes'
  no_grid_colour: '#a40013'
  show_nonessential: 'no'
entities:
  use_timer_248: switch.toggle_system_timer
  priority_load_243: switch.toggle_priority_load
  batchargeday_70: sensor.battery_charge_day
  batdischargeday_71: sensor.battery_discharge_day
  loadday_84: sensor.daily_load_power_kwh
  grid_buy_day_76: sensor.grid_import_day_buy
  grid_sell_day_77: none
  solarday_108: sensor.daily_pv_power_kwh
  inverter_grid_voltage_154: sensor.grid_inverter_voltage
  inverter_load_freq_192: sensor.load_frequency
  inverter_out_164: sensor.inverter_output_current
  inverter_out_175: sensor.inverter_output_power
  inverter_load_grid_169: sensor.grid_power
  pv1_power_186: sensor.pv1_power
  pv2_power_187: sensor.pv2_power
  pv3_power_188: none
  pv4_power_189: none
  battery_voltage_183: sensor.battery_voltage
  battery_soc_184: sensor.battery_soc
  battery_out_190: sensor.battery_output_power
  ess_power: sensor.load_power
  grid_external_power_172: sensor.grid_external_power
  pv1_v_109: sensor.dc1_voltage
  pv1_i_110: sensor.dc1_current
  pv2_v_111: sensor.dc2_voltage
  pv2_i_112: sensor.dc2_current
  pv3_v_113: none
  pv3_i_114: none
  pv4_v_115: none
  pv4_i_116: none
  grid_status_194: binary_sensor.grid_connected_status
  inverter_status_59: sensor.overall_state
  aux_power_166: sensor.aux_output_power


```
