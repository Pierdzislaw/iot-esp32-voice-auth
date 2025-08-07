# Architektura systemu - IoT ESP32 Voice Authentication Device

## 🏗️ Przegląd architektury

### Główne komponenty
```
┌─────────────────┐    ┌──────────────┐    ┌─────────────────┐
│   Mikrofon      │    │    ESP32-S3  │    │  Czytnik linii  │
│   INMP441       │───▶│              │◄──▶│  papilarnych    │
│   (I2S Input)   │    │              │    │  R307 (UART)    │
└─────────────────┘    │              │    └─────────────────┘
                       │              │    
┌─────────────────┐    │              │    ┌─────────────────┐
│   Wzmacniacz    │◄───│              │───▶│   Diody LED     │
│   MAX98357A     │    │              │    │   Status        │
│   (I2S Output)  │    │              │    └─────────────────┘
└─────────────────┘    │              │    
        │              │              │    ┌─────────────────┐
        ▼              │              │───▶│   Przyciski     │
┌─────────────────┐    │              │    │   Sterowanie    │
│   Głośnik       │    │              │    └─────────────────┘
│   4Ω 4W         │    └──────────────┘    
└─────────────────┘            │           
                               ▼           
                    ┌─────────────────┐    
                    │   Wi-Fi/MQTT    │    
                    │   Home Assistant│    
                    └─────────────────┘    
```

## 🔌 Schemat blokowy zasilania

```
┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│  2x 18650   │───▶│  2S BMS +   │───▶│ Step-down   │
│  Li-ion     │    │  Balancer   │    │ 6.0-8.4V    │
│  Recykling  │    │  Protection │    │ → 5.0V      │
└─────────────┘    └─────────────┘    └─────────────┘
                           │                   │
                           ▼                   ▼
                   ┌─────────────┐    ┌─────────────┐
                   │ Ładowarka   │    │   LDO       │
                   │ 2S 8.4V     │    │ 5.0V→3.3V   │
                   │ Dedykowana  │    │ ESP32-S3    │
                   └─────────────┘    └─────────────┘
```

## 🧠 Logika stanów systemu

### Automat stanów
```
     [POWER ON]
          │
          ▼
    ┌──────────┐     VAD wykrywa    ┌─────────────────┐
    │ UŚPIONY  │────────────────────▶│ CZEKA_NA_ODCISK │
    │(Lt.Sleep)│                    │   (Timeout 30s) │
    └──────────┘                    └─────────────────┘
          ▲                                   │
          │                                   │ Odcisk OK
          │                                   ▼
          │                         ┌─────────────────┐
          │                         │ AUTORYZOWANY_   │
          │                         │ NAGRYWA         │
          │                         │ (Timeout 10s)   │
          │                         └─────────────────┘
          │                                   │
          │ Timeout/Błąd/                     │ Nagranie OK
          │ Ukończone                         │
          │                                   ▼
          │                         ┌─────────────────┐
          └─────────────────────────│ WYSYŁA_DANE     │
                                    │ (Wi-Fi/MQTT)    │
                                    └─────────────────┘
```

### Zarządzanie energią
- **Light Sleep**: ESP32-S3 + aktywny mikrofon dla VAD
- **N-MOSFET sterowanie**: Czytnik linii papilarnych (GPIO → GND switching)
- **Monitorowanie**: ADC + dzielnik napięcia baterii

## 📡 Protokoły komunikacji

### I2S Audio Pipeline
```
INMP441 ──I2S──▶ ESP32-S3 ──I2S──▶ MAX98357A ──Analog──▶ Speaker
  (Input)         (Processing)        (Amplifier)         (Output)
```

### UART Communication
```
ESP32-S3 ──UART──▶ R307 Fingerprint Reader
TX/RX pins         (9600 baud, 8N1)
```

### Network Communication
```
ESP32-S3 ──Wi-Fi──▶ Home Assistant
                    ├─ MQTT (telemetry)
                    ├─ HTTP POST (audio)
                    └─ OTA updates
```

## 🔧 Konfiguracja pinów ESP32-S3

### Audio (I2S)
- **I2S_BCLK**: GPIO4 (Bit Clock)
- **I2S_LRC**: GPIO5 (Left/Right Clock)  
- **I2S_DIN**: GPIO6 (Data Input - INMP441)
- **I2S_DOUT**: GPIO7 (Data Output - MAX98357A)

### UART (Fingerprint)
- **UART_TX**: GPIO17
- **UART_RX**: GPIO18

### Control & Status
- **FP_POWER_EN**: GPIO8 (N-MOSFET Gate - czytnik ON/OFF)
- **LED_RED**: GPIO9
- **LED_GREEN**: GPIO10  
- **LED_BLUE**: GPIO11
- **BTN_MAIN**: GPIO12 (pull-up)
- **BTN_RESET**: GPIO13 (pull-up)

### Power Management
- **BAT_VOLTAGE**: GPIO1 (ADC - dzielnik napięcia)
- **CHARGE_STATUS**: GPIO2 (input - status ładowania)

## 💾 Struktura firmware

### ESPHome Configuration
```yaml
# Główne sekcje konfiguracji
esphome:
  name: voice-auth-device
  platform: ESP32
  board: esp32-s3-devkitc-1

# Kluczowe komponenty
i2s_audio:
  - id: i2s_in    # INMP441
  - id: i2s_out   # MAX98357A

microphone:
  platform: i2s_audio
  
speaker:
  platform: i2s_audio

voice_assistant:
  microphone: mic
  speaker: speaker

fingerprint_grow:
  uart_id: uart_fp
```

### Alternatywna struktura MicroPython
```
/main.py           # Główna pętla programu
/vad.py            # Voice Activity Detection
/fingerprint.py    # Obsługa czytnika R307  
/audio.py          # I2S audio handling
/power.py          # Zarządzanie energią
/network.py        # Wi-Fi/MQTT communication
/config.py         # Konfiguracja systemu
```

## 🔐 Bezpieczeństwo

### Uwierzytelnianie wielopoziomowe
1. **VAD**: Wykrywanie aktywności głosowej
2. **Biometria**: Weryfikacja odcisku palca  
3. **Timeout**: Automatyczne wylogowanie
4. **Encryption**: Szyfrowane przesyłanie audio

### Zarządzanie użytkownikami
- **Rejestracja**: Tryb zapisu nowych odcisków (Admin mode)
- **Usuwanie**: Zdalne usuwanie użytkowników
- **Backup**: Export/import bazy odcisków
- **Audit**: Logi dostępu i prób autoryzacji

---
**Wersja**: 1.0  
**Data**: Sierpień 2025  
**Status**: Projekt konceptualny
