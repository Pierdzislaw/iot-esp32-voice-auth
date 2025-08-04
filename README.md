## 📝 Notatki techniczne

### 1. Definicja projektu

Urządzenie IoT oparte na ESP32 z mikrofonem MEMS, realizujące:

# IoT ESP32 Voice Authentication Device

Urządzenie IoT oparte na ESP32 z mikrofonem MEMS, realizujące:

## 🎯 Funkcjonalności
- **Wybudzanie głosem (VAD)**: Aktywne nasłuchiwanie i wykrywanie aktywności głosowej
- **Autoryzacja biometryczna**: Weryfikacja tożsamości użytkownika za pomocą odcisku palca
- **Integracja z Home Assistant**: Przesyłanie poleceń głosowych do sterowania inteligentnym domem
- **Energooszczędność**: Optymalizacja pod kątem zasilania bateryjnego
- **Zbieranie metryk**: Wysyłanie danych (np. stan baterii, statusy operacji) do analizy

## 🔧 Hardware

### Komponenty główne
- **PCB**: Projektowane w KiCad, montaż ręczny
- **Mikrofon z VAD**: INMP441 (I2S MEMS) - dobra dostępność i dokumentacja
- **Czytnik linii papilarnych**: R307 (UART) - dobry kompromis cena/jakość, alternatywa AS608 lub FPM10A
- **Mikrocontroller**: ESP32
- **Audio amplifier**: MAX98357 (I2S, 3.2W)
- **Głośnik**: 4Ω 2-3W (40-50mm) - feedback audio

### Zasilanie
- **Akumulatory**: 2x Li-ion 18650 z recyklingu (ze starych podgrzewaczy GLO - 6.0V–8.4V)
- **Ładowarka**: 2S BMS + dedykowana ładowarka 2S (8.4V) lub 2x TP4056
- **Konwersja napięcia**: Step-down 5V + LDO 3.3V
- **Monitorowanie baterii**: Dzielnik napięcia + ADC
- **Zarządzanie zasilaniem**: MOSFET (np. 2N7000) do odłączania czytnika

### Interfejs użytkownika
- **Diody LED 0805**:
  - Czerwona/Zielona: ładowanie, autoryzacja
  - Niebieska: nasłuch, oczekiwanie, błąd
- **Przycisk Tact Switch**: Restart, przywracanie firmware
- **Przycisk wielofunkcyjny**:
  - 3 sekundy: restart
  - 10 sekund: przywrócenie stabilnej wersji

## 💻 Software

### Firmware
- **Główny**: ESPHome (YAML) — szybka integracja z Home Assistant
- **Alternatywa**: MicroPython — większa elastyczność, więcej kodu

### Logika działania
- **Tryb uśpienia**: Deep Sleep + wybudzanie przez VAD
- **Stany systemu**: `UŚPIONY` → `CZEKA_NA_ODCISK` → `AUTORYZOWANY_NAGRYWA` → `BŁĄD`
- **Zarządzanie energią**: MOSFET sterowany programowo
- **Zarządzanie użytkownikami**: Tryb rejestracji odcisków
- **OTA**: Aktualizacje Over-the-Air

### Komunikacja
- **Wi-Fi**: Integracja z siecią domową
- **Protokoły**: MQTT / HTTP POST do Home Assistant
- **Przetwarzanie audio**: Docker z Whisper, Piper

## 📊 Infrastruktura
- **Metryki**: InfluxDB + Grafana (TrueNAS na Proxmox)
- **Dostęp zdalny**: ZeroTier

## 🏠 Obudowa
- **Projekt**: Solid Edge
- **Wykonanie**: Druk 3D, dopasowany do PCB, baterii, czytnika i diod

## 💰 Kosztorys

| Komponent | Cena (PLN) |
|---|---|
| Mikrofon INMP441 | 5–15 zł |
| Czytnik linii papilarnych R307 | 15–25 zł |
| MAX98357 amplifier | 8–15 zł |
| Głośnik 4Ω 3W | 8–15 zł |
| 2S BMS + ładowarka | 15–25 zł |
| Akumulator Li-ion 18650 (2x) | 0 zł (recykling GLO) |
| ESP32 | 8–15 zł |
| Tranzystor MOSFET (2N7000) | 1–2 zł |
| Diody LED i inne komponenty | 5–10 zł |
| **Suma minimalna** | **ok. 65 zł** |
| **Suma maksymalna** | **ok. 127 zł** |

## 📋 Development Log

### Kluczowe decyzje projektowe:
- **R307 vs AS608**: Wybrano R307 (15-25 PLN) - lepszy stosunek cena/jakość niż AS608 (25-35 PLN)
- **INMP441 vs SPH0641LU4H**: Wybrano INMP441 - lepsza dostępność w Polsce, więcej przykładów kodu
- **Zasilanie 2S**: 2x 18650 szeregowo dla stabilnych 5V (step-down lepszy niż boost z single cell)
- **Audio pipeline**: ESP32 → INMP441 (input) → MAX98357 → 4Ω speaker (output)
- **Baterie z recyklingu**: Wykorzystanie sprawnych ogniw z podgrzewaczy GLO (oszczędność ~40 PLN)

### Uwagi techniczne:
- BMS ≠ ładowarka - potrzebne oba dla bezpiecznego ładowania 2S
- VAD to funkcja software'owa, nie hardware'owa w mikrofonach MEMS
- TP4056 tylko dla single cell - dla 2S potrzeba dedykowanych rozwiązań

## 📋 Status projektu
**Faza**: Koncepcja → Zakup komponentów  
**Następne kroki**: Finalizacja schematu, zamówienie komponentów, projekt PCB

## 📖 Dokumentacja techniczna
- Dane techniczne z kart katalogowych: mikrofon, czytnik, ładowarka, MOSFET
- Schematy elektryczne (KiCad)
- Modele 3D obudowy (Solid Edge)

---
**Ostatnia aktualizacja**: Sierpień 2025 - Hardware selection & component decisions

