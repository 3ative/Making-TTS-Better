# Making-TTS-Better
Give your Alexa (or Google Home) more personality with generated sentences.

speak_bedroom_temperature:
```yaml

  alias: Speak Bedroom Temperature
  sequence:
    - service: notify.alexa_media
      data_template:
        target: 
          "{{ states.sensor.last_alexa.state }}"
        data:
          type: tts
        message: "Current Temperature,
        {{states('sensor.bedroom_temperature')}},
        Thermostat set to,
        {{state_attr('climate.bedroom_cooling', 'temperature')}},
        and the Thermostat is,
        {{ states.input_boolean.heating_auto.state }}"
```

speak_heating_auto_off:

```yaml

  alias: Heating Auto Off
  sequence:
    - service: notify.alexa_media
      data_template:
        target:
          - "{{ states.sensor.last_alexa.state }}"
        data:
          type: tts
        message: '{{
          [
          "Bedroom temperature set to manual",
          "Bedroom temperature to manual control",
          "I will no longer control the bedroom temperature",
          "Temperature of the bedroom set to Manual",
          "Control of the bedroom climate is yours",
          "I have stopped controlling the bedroom temperature"
          ]|random}}'
  ```
  
  speak_window_lights:
  ```yaml

  alias: Speak Window Lights
  sequence:
    - service: notify.alexa_media
      data_template:
        target:
          - "{{ states.sensor.last_alexa.state }}"
        data:
          type: tts
        message: '{{
          [
          "Turning on window lights... ",
          "Window lights on... ", "Window lights coming on... ",
          "Lighting up the window... ",
          "Your Window lights are on... ",
          ]|random +[

          "Hmmm, ",
          "Arr, ",
          "Wow, ",
          "Cool, ",
          "sweet, ",
          ]|random +[

          "Blue.",
          "Thats Pretty.",
          "How Nice.",
          "Oh I do love Blue.", "I so love Blue.",
          ]|random}}'
```

How to make the "Last Alexa"
Make a new 'sensor' .yaml file with this code:
```yaml
- platform: template
  sensors:
    last_alexa:
      value_template: >
        {{ states.media_player | selectattr('attributes.last_called','eq',true) | map(attribute='entity_id') | first }}
```

---
### 🤝 Found this useful, want to say 'Thanks' and support my efforts. CHEERS🍺
| Buy me a Coffee | PATREON |
|-----------------|---------|
| [![Buy Me A Coffee](https://img.shields.io/badge/Buy%20Me%20A%20Coffee-donate-yellow.svg?style=flat-square&logo=buy-me-a-coffee)](https://www.buymeacoffee.com/3ative) | [![Patreon](https://img.shields.io/badge/Patreon-support-red.svg?style=flat-square&logo=patreon)](https://www.patreon.com/3ative) |
---
