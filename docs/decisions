# Decyzje projektowe - IoT ESP32 Voice Authentication Device

## 🎯 Kluczowe wybory techniczne

### 🧠 Mikrocontroller: ESP32-S3
**Decyzja**: ESP32-S3 zamiast standardowego ESP32

**Uzasadnienie**:
- **RAM**: 512KB SRAM (vs 320KB w ESP32) - potrzebne dla przetwarzania audio
- **Flash**: Do 32MB external flash dla większych aplikacji
- **USB**: Native USB support dla łatwiejszego debugowania
- **AI**: Wbudowane wsparcie dla AI acceleration
- **Kompatybilność**: Pin-compatible z ESP32 w większości zastosowań

**Koszt**: +4-5 PLN względem ESP32, ale uzasadniony funkcjonalnością

---

### 🎤 Mikrofon: INMP441 (I2S MEMS)
**Decyzja**: INMP441 zamiast analogowych alternatyw

**Uzasadnienie**:
- **Jakość**: 24-bit I2S output, lepsze SNR niż analogowe
- **Dostępność**: Łatwo dostępny w Polsce (5-15 PLN)
- **Dokumentacja**: Dużo przykładów z ESPHome i Arduino
- **Integracja**: Natywne wsparcie I2S w ESP32-S3
- **Brak VAD**: Software VAD daje większą kontrolę niż hardware

**Alternatywy odrzucone**: SPH0641LU4H (droższy), analogowe (gorsze SNR)

---

### 👆 Czytnik linii papilarnych: R307
**Decyzja**: R307 jako główny wybór

**Uzasadnienie**:
- **Cena**: 15-25 PLN (dobry stosunek jakość/cena)
- **Protokół**: UART - prosty w obsłudze
- **Pojemność**: Do 127 odcisków
- **Czas odpowiedzi**: <1s identyfikacja
- **Dokumentacja**: Dostępne biblioteki Arduino/MicroPython

**Backup opcja**: AS608 (25-35 PLN) - jeśli R307 niedostępny

---

### 🔊 Audio Output: MAX98357A + Głośnik 4Ω 4W
**Decyzja**: MAX98357A I2S amplifier z głośnikiem 4W

**Uzasadnienie**:
- **Moc**: 3.2W @ 5V, 4Ω load - wystarczająca do feedback audio
- **Protokół**: I2S - synchronizacja z mikrofonem
- **Jakość**: Klasa D - wysoka sprawność
- **Głośnik 4W**: Margines bezpieczeństwa dla 3.2W wzmacniacza
- **Rozmiar**: 40-50mm - kompromis jakość/wielkość

**Alternatywy odrzucone**: Analogowe wzmacniacze (większa złożoność)

---

### 🔋 Zasilanie: 2x 18650 Li-ion + 2S BMS
**Decyzja**: Konfiguracja szeregowa 2S z dedykowanym BMS

**Uzasadnienie**:
- **Napięcie**: 6.0-8.4V - idealny zakres dla step-down do 5V
- **Pojemność**: 2x 2600mAh = 5200mAh przy 7.4V nominalnie
- **Recykling**: Wykorzystanie ogniw z podgrzewaczy GLO (oszczędność ~40 PLN)
- **BMS**: Balancing + protection - bezpieczeństwo i długość życia
- **Sprawność**: Step-down lepsza niż boost z single cell

**Odrzucone**: Single cell + boost (gorsza sprawność, mniejsza pojemność)

---

### ⚡ Zarządzanie zasilaniem: N-MOSFET Low-side
**Decyzja**: N-MOSFET (2N7000) do low-side switching czytnika

**Uzasadnienie**: ✅ **Poprawka z sesji**
- **Sterowanie**: Łatwiejsze sterowanie względem masy (GND)
- **GPIO**: Bezpośrednie sterowanie z ESP32 (3.3V gate)
- **Koszt**: 1-2 PLN
- **Niezawodność**: Sprawdzone rozwiązanie
- **Schemat**: GPIO → Gate, Source → GND, Drain → Load GND

**Poprzednia decyzja**: P-channel MOSFET - odrzucona jako bardziej skomplikowana

---

### 🛜 Firmware: ESPHome (główny)
**Decyzja**: ESPHome jako pierwotna platforma

**Uzasadnienie**:
- **Integracja**: Natywne wsparcie Home Assistant
- **Szybkość**: Szybki prototyping z YAML
- **Komponenty**: Gotowe: I2S audio, fingerprint, MQTT
- **OTA**: Wbudowane aktualizacje
- **Społeczność**: Duża baza wiedzy

**Backup**: MicroPython - jeśli ESPHome niewystarczający dla VAD

---

### 🔋 Tryb oszczędzania energii: Light Sleep
**Decyzja**: Light Sleep zamiast Deep Sleep

**Uzasadnienie**:
- **VAD**: Wymaga ciągłego próbkowania mikrofonu
- **Zużycie**: 50-80mA w Light Sleep z aktywnym I2S
- **Wybudzanie**: Szybkie (ms) vs Deep Sleep (sekundy)
- **RAM**: Zachowanie stanu systemu

**Deep Sleep**: Tylko w trybie emergency/shipping

---

## 📊 Parametry docelowe

### Energetyczne
- **Aktywny**: 150-200mA
- **Light Sleep + VAD**: 50-80mA  
- **Czas pracy**: 8-12h ciągłej pracy
- **Ładowanie**: 4-6h (1A charger)

### Wydajnościowe  
- **VAD latency**: <100ms
- **Fingerprint**: <1s weryfikacja
- **Audio quality**: 16kHz/16-bit minimum
- **Wi-Fi reconnect**: <5s

### Fizyczne
- **Rozmiary**: <150x100x50mm (docelowo)
- **Waga**: <300g z bateriami
- **Temperatura**: 0-40°C operacyjna

---

## 🔄 Historia zmian decyzji

### 2025-08-07: Sesja korekcyjna
- ✅ **ESP32 → ESP32-S3**: Więcej RAM dla audio
- ✅ **P-MOSFET → N-MOSFET**: Łatwiejsze sterowanie
- ✅ **Głośnik 3W → 4W**: Margines bezpieczeństwa
- ✅ **Deep Sleep → Light Sleep**: Ciągły VAD
- ✅ **Dodano AS608**: Jako backup dla R307

### 2025-08-07: Decyzje początkowe  
- ✅ **R307 vs AS608**: R307 wybrany (cena)
- ✅ **INMP441**: Wybrany (dostępność)
- ✅ **2S zasilanie**: Potwierdzone
- ✅ **Recykling baterii**: GLO 18650

---

## ⏭️ Następne decyzje do podjęcia

### Hardware
- [ ] **Dokładny model ESP32-S3** (DevKit vs custom PCB)
- [ ] **Dokładny model step-down** (LM2596 vs alternatywy)
- [ ] **Specyfikacja BMS** (konkretny model)
- [ ] **Rozmiar/typ głośnika** (40mm vs 50mm)

### Software  
- [ ] **VAD algorithm** (threshold-based vs ML)
- [ ] **Audio codec** (PCM vs compressed)
- [ ] **MQTT structure** (topics, payloads)
- [ ] **Fingerprint storage** (local vs cloud backup)

### Mechanika
- [ ] **Typ złączy** (JST vs inne)
- [ ] **Montaż PCB** (śruby vs clips)
- [ ] **Materiał obudowy** (PLA vs PETG vs ABS)
- [ ] **Pozycja mikrofonu** (góra vs przód)

---
**Ostatnia aktualizacja**: 2025-08-07  
**Przez**: Claude + User collaboration  
**Status**: Decyzje podstawowe ustalone, szczegóły do dopracowania
