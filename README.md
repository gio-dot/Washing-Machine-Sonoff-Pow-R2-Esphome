# Washing-Machine-Sonoff-Pow-R2-Esphome

I use a Sonoff Pow R2 to monitor my washing machine activity in Home assistant; traditional approach to do so is to decode washing phases using Home assistant sensors/templates. Thanks to ESPHome firmware this can be easily made directly in the Sonoff Pow R2 cleaning up Home assistant configuration.
Five binary sensors (RUN, WASHING, CENTRIFUGE, DRAIN, END) are automatically exposed by the Sonoff Pow to Home assistant frontend.

RUN or END sensors can be easily used in Home assistant automations to send messages to Telegram or Google home etc. to  warn that the cycle has ended. See Home assistant example: [home_assistant_w_machine.yaml](https://github.com/Gio-dot/Washing-Machine-Sonoff-Pow-R2-Esphome/blob/master/home_assistant_w_machine.yaml)

For instructions about ESPHome installation see: https://esphome.io/index.html

### New Esphome code v.1.1
Changelog:
1. Disabled esp8266_restore_from_flash option.
2. Created a second set of sensors (with slow update rate to use in Home assistant).
3. Optimized washing phases detection.

Use this yaml code to create your ESPHome firmware v.1.1: [sonoff_pow_r2_w_machine.yaml](https://github.com/Gio-dot/Washing-Machine-Sonoff-Pow-R2-Esphome/blob/master/sonoff_pow_r2_lavatrice_v1.1.yaml)

Old version: [sonoff_pow_r2_w_machine.yaml](https://github.com/Gio-dot/Washing-Machine-Sonoff-Pow-R2-Esphome/blob/master/sonoff_pow_r2_w_machine.yaml)

## How it works

<img src="https://github.com/Gio-dot/Washing-Machine-Sonoff-Pow-R2-Esphome/blob/master/img/end.jpg" width="300">
This image show Home assitant card from Sonoff Pow. Washing phases are shown in sequence from bottom to top. At the end of the cycle all phases (except RUN) remains lighted. At next cycle start they are resetted.
Sonoff Pow blue Led is lighted when a cycle is running and turned off at the cycle end.

## ESPHome firmware notes

Line 5: `esp8266_restore_from_flash: true` to restore previous relay state after a Sonoff POW R2 power cycle.

Lines 48-167: washing phases; phases detection can be optimized changing power thresholds and delay filters. 

ESPHome `total_daily_energy` isn't retained through Sonoff power cycles. For this reason and also to store washing machine consumption hystorical data, i used an utility meter in Home assistant Configuration feeding it with `total_daily_energy` sensor from Sonoff POW.


