# PZEM-016-OLED-2-OUT-ESPHome

I modified a PZEM-016 putting inside a Wemos D1 mini with ESPHome firmware and an oled display to show relevant readings. PZEM-016 has an rs485 interface, so to connect it to Wemos d1 rs485 chip must be removed and voltage level has to be shifted to 3.3V using two 2k2 resistors. I used A and B pin on the old rs485 connector to create two digital outputs that can be used ie to drive two relais module. 

ESPHome firmware source: [wemos_d1_pzem016_display.yaml](https://github.com/Gio-dot/PZEM-016-OLED-2-OUT-ESPHome/blob/master/wemos_d1_pzem016_display.yaml)

For instructions about ESPHome installation see: https://esphome.io/index.html

## Schematic

<img src="https://github.com/Gio-dot/PZEM-016-OLED-2-OUT-ESPHome/blob/master/img/ESPHome-wemos-d1-pzem016-display_bb.png" width="800">

<p float="left">
  <img src="https://github.com/Gio-dot/PZEM-016-OLED-2-OUT-ESPHome/blob/master/img/IMG_20200429_104740.jpg" width="300" />
  <img src="https://github.com/Gio-dot/PZEM-016-OLED-2-OUT-ESPHome/blob/master/img/IMG_20200429_023520.jpg" width="300" /> 
  <img src="https://github.com/Gio-dot/PZEM-016-OLED-2-OUT-ESPHome/blob/master/img/2020-04-30%2000_55_38-Panoramica%20-%20Home%20Assistant.png" width="300" />
</p>


This image show Home assitant card from Sonoff Pow. Washing phases are shown in sequence from bottom to top. At the end of the cycle all phases (except RUN) remains lighted. At next cycle start they are resetted.
Sonoff Pow blue Led is lighted when a cycle is running and turned off at the cycle end.

## ESPHome firmware notes

Use this yaml code to create your ESPHome firmware: [sonoff_pow_r2_w_machine.yaml](https://github.com/Gio-dot/Washing-Machine-Sonoff-Pow-R2-Esphome/blob/master/sonoff_pow_r2_w_machine.yaml)

Line 5: `esp8266_restore_from_flash: true` to restore previous relay state after a Sonoff POW R2 power cycle.

Lines 48-167: washing phases; phases detection can be optimized changing power thresholds and delay filters. 

ESPHome `total_daily_energy` isn't retained through Sonoff power cycles. For this reason and also to store washing machine consumption hystorical data, i used an utility meter in Home assistant Configuration feeding it with `total_daily_energy` sensor from Sonoff POW.


