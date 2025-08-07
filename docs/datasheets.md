# Datasheets & Dokumentacja - IoT ESP32 Voice Authentication Device

Linki do dokumentacji technicznej wszystkich komponentów projektu.

---

## 🧠 Mikrocontroller

### ESP32-S3
- **📄 Datasheet**: [ESP32-S3 Datasheet](https://www.espressif.com/sites/default/files/documentation/esp32-s3_datasheet_en.pdf)
- **📖 Technical Reference**: [ESP32-S3 Technical Reference Manual](https://www.espressif.com/sites/default/files/documentation/esp32-s3_technical_reference_manual_en.pdf)
- **💻 Programming Guide**: [ESP-IDF Programming Guide](https://docs.espressif.com/projects/esp-idf/en/latest/esp32s3/)
- **🔧 Hardware Design**: [ESP32-S3 Hardware Design Guidelines](https://www.espressif.com/sites/default/files/documentation/esp32-s3_hardware_design_guidelines_en.pdf)
- **📌 Pinout**: [ESP32-S3 DevKitC-1 Pinout](https://docs.espressif.com/projects/esp-idf/en/latest/esp32s3/hw-reference/esp32s3/user-guide-devkitc-1.html)

---

## 🎤 Audio Input

### INMP441 (I2S MEMS Microphone)
- **📄 Datasheet**: [INMP441 Datasheet](https://invensense.tdk.com/wp-content/uploads/2015/02/INMP441.pdf)
- **📖 Application Note**: [I2S Digital Microphone Design Guidelines](https://invensense.tdk.com/wp-content/uploads/2015/02/AN-1112-v1.1.pdf)
- **💻 ESP32 Examples**: [ESP-IDF I2S Examples](https://github.com/espressif/esp-idf/tree/master/examples/peripherals/i2s)
- **🔧 PCB Layout**: [INMP441 PCB Layout Guidelines](https://invensense.tdk.com/wp-content/uploads/2015/02/AN-1003-v2.0.pdf)

---

## 🔊 Audio Output

### MAX98357A (I2S Audio Amplifier)
- **📄 Datasheet**: [MAX98357A Datasheet](https://datasheets.maximintegrated.com/en/ds/MAX98357A-MAX98357B.pdf)
- **📖 Application Note**: [MAX98357A Design Guidelines](https://pdfserv.maximintegrated.com/en/an/AN6731.pdf)
- **💻 Adafruit Guide**: [MAX98357A Breakout Guide](https://learn.adafruit.com/adafruit-max98357-i2s-class-d-mono-amp)
- **🔧 PCB Design**: [Audio Amplifier PCB Guidelines](https://www.maximintegrated.com/en/design/technical-documents/tutorials/2/2436.html)

---

## 👆 Biometric Sensor

### R307 (Fingerprint Sensor)
- **📄 Datasheet**: [R307 Fingerprint Module Datasheet](https://cdn.sparkfun.com/datasheets/Sensors/Biometric/ZFM-20-series-modules-datasheet.pdf)
- **📖 User Manual**: [R307 User Manual](https://www.openhardware.io/uploads/5060a155757b7613478b4567.pdf)
- **💻 Command Set**: [R307 Protocol & Commands](https://github.com/adafruit/Adafruit-Fingerprint-Sensor-Library/blob/master/examples/fingerprint/fingerprint.ino)
- **🔧 Integration Guide**: [Arduino Fingerprint Tutorial](https://learn.adafruit.com/adafruit-optical-fingerprint-sensor)

### AS608 (Alternative)
- **📄 Datasheet**: [AS608 Fingerprint Sensor](https://www.openhardware.io/uploads/5060a155757b7613478b4567.pdf)
- **📖 Protocol**: [AS608 Communication Protocol](https://github.com/tongbajiel/AS608/blob/master/AS608%20fingerprint%20module%20user%20manual-V1.6.pdf)

---

## ⚡ Power Management

### N-Channel MOSFET (2N7000)
- **📄 Datasheet**: [2N7000 MOSFET Datasheet](https://www.onsemi.com/pdf/datasheet/2n7000-d.pdf)
- **📖 Application Note**: [MOSFET Switching Applications](https://www.onsemi.com/pub/Collateral/AND9083-D.PDF)
- **🔧 Gate Drive**: [MOSFET Gate Drive Fundamentals](https://www.ti.com/lit/an/slva618a/slva618a.pdf)

### Li-ion Battery Management
- **📄 18650 Specifications**: [Generic 18650 Li-ion Specs](https://www.batteryspace.com/prod-specs/6294.pdf)
- **📖 2S BMS Guide**: [2S Li-ion BMS Design](https://www.ti.com/lit/an/slva482a/slva482a.pdf)
- **🔧 Safety Guidelines**: [Li-ion Battery Safety](https://www.ti.com/lit/an/slva551/slva551.pdf)

### Step-Down Converter
- **📄 LM2596 Datasheet**: [LM2596 Buck Converter](https://www.ti.com/lit/ds/symlink/lm2596.pdf)
- **📖 Design Guide**: [LM2596 PCB Layout Guidelines](https://www.ti.com/lit/an/snva009af/snva009af.pdf)
- **🔧 Calculator**: [TI WEBENCH Power Designer](https://www.ti.com/design-tools/webench.html)

---

## 💡 User Interface

### LEDs (0805 SMD)
- **📄 Red LED**: [Standard Red LED 0805](https://www.vishay.com/docs/83171/tlcr5800.pdf)
- **📄 Green LED**: [Standard Green LED 0805](https://www.vishay.com/docs/83171/tlcg5800.pdf)  
- **📄 Blue LED**: [Standard Blue LED 0805](https://www.vishay.com/docs/83171/tlcb5800.pdf)
- **🔧 Current Limiting**: [LED Current Calculator](https://ledcalculator.net/)

### Tactile Switches
- **📄 Tact Switch**: [6x6mm Tactile Switch](https://www.alps.com/prod/info/E/HTML/Tact/SnapIn/SKQG/SKQGAFE010.html)
- **📖 Application**: [Switch Debouncing Guide](https://www.ganssle.com/debouncing.htm)

---

## 🏠 Mechanical Components

### Speakers
- **📄 4Ω Speaker**: [Generic 4Ω 4W Speaker Specs](https://www.mouser.com/datasheet/2/670/pui_as-series_datasheet-1315537.pdf)
- **📖 Enclosure Design**: [Speaker Enclosure Guidelines](https://sound.org/vituix/box.htm)

### Connectors
- **📄 JST Connectors**: [JST PH Series](https://www.jst-mfg.com/product/pdf/eng/ePH.pdf)
- **📄 USB-C**: [USB-C Connector Specs](https://www.usb.org/sites/default/files/USB%20Type-C%20Spec%20R2.0%20-%20August%202019.pdf)

---

## 💻 Software Documentation

### ESPHome
- **📖 Official Docs**: [ESPHome Documentation](https://esphome.io/)
- **🎤 I2S Audio**: [ESPHome I2S Audio Component](https://esphome.io/components/i2s_audio.html)
- **👆 Fingerprint**: [ESPHome Fingerprint Component](https://esphome.io/components/fingerprint_grow.html)
- **🔊 Speaker**: [ESPHome Speaker Component](https://esphome.io/components/speaker/i2s_audio.html)
- **📡 Voice Assistant**: [ESPHome Voice Assistant](https://esphome.io/components/voice_assistant.html)

### Home Assistant
- **📖 Voice Control**: [HA Voice Assistant Integration](https://www.home-assistant.io/voice_control/)
- **📡 MQTT**: [HA MQTT Discovery](https://www.home-assistant.io/docs/mqtt/discovery/)
- **🔧 ESPHome Integration**: [HA ESPHome Integration](https://www.home-assistant.io/integrations/esphome/)

### Alternative Firmware
- **💻 MicroPython**: [MicroPython ESP32 Guide](https://docs.micropython.org/en/latest/esp32/quickref.html)
- **🎤 I2S MicroPython**: [machine.I2S Documentation](https://docs.micropython.org/en/latest/library/machine.I2S.html)
- **👆 UART MicroPython**: [machine.UART Documentation](https://docs.micropython.org/en/latest/library/machine.UART.html)

---

## 🛠️ Design Tools

### PCB Design (KiCad)
- **📖 KiCad Documentation**: [KiCad Official Docs](https://docs.kicad.org/)
- **🔧 Footprint Libraries**: [KiCad Library Repository](https://kicad.github.io/)
- **📐 Design Rules**: [PCB Design Best Practices](https://www.altium.com/documentation/altium-designer/pcb-design-rules-reference)

### 3D Design (Solid Edge)
- **📖 Solid Edge Docs**: [Siemens Solid Edge Documentation](https://docs.plm.automation.siemens.com/tdoc/se/2023/)
- **🖨️ 3D Printing**: [3D Printing Design Guidelines](https://www.protolabs.com/resources/design-tips/3d-printing-design-guidelines/)

---

## 🛒 Component Sources (Poland)

### Online Stores
- **🏪 TME**: [tme.eu](https://www.tme.eu/) - Professional components
- **🏪 Kamami**: [kamami.pl](https://kamami.pl/) - ESP32, sensors, modules
- **🏪 Botland**: [botland.com.pl](https://botland.com.pl/) - Maker components
- **🏪 Mouser**: [mouser.com](https://www.mouser.com/) - International shipping
- **🏪 Allegro**: [allegro.pl](https://allegro.pl/) - Local marketplace

### Specific Component Links
- **ESP32-S3 DevKit**: [Kamami ESP32-S3](https://kamami.pl/esp32-esp8266/575708-esp32-s3-devkitc-1-n16r8.html)
- **INMP441**: [Botland INMP441](https://botland.com.pl/mikrofony/8699-mikrofon-mems-i2s-inmp441.html)
- **MAX98357A**: [Kamami MAX98357A](https://kamami.pl/wzmacniacze-audio/577744-max98357a-wzmacniacz-audio-i2s-klasa-d-32w.html)
- **R307**: [Botland R307](https://botland.com.pl/czytniki-linii-papilarnych/6182-czytnik-linii-papilarnych-r307.html)

---

## 📞 Technical Support

### Community Forums
- **ESP32**: [ESP32.com Forum](https://esp32.com/)
- **ESPHome**: [ESPHome Discord](https://discord.gg/KhAMKrd)
- **Home Assistant**: [HA Community](https://community.home-assistant.io/)
- **Reddit**: [r/esp32](https://www.reddit.com/r/esp32/), [r/homeassistant](https://www.reddit.com/r/homeassistant/)

### Local Communities (Poland)
- **Forbot**: [forbot.pl](https://forbot.pl/) - Polish electronics forum
- **AVR**: [avr.pl](https://www.avr.pl/) - Polish microcontroller community

---

**Ostatnia aktualizacja**: 2025-08-07  
**Status**: Kompletne linki do dokumentacji  
**Uwaga**: Sprawdź aktualność linków przed użyciem
