## 📝 Notatki techniczne

### 1. Definicja projektu

Urządzenie IoT oparte na ESP32 z mikrofonem MEMS, realizujące:

### 1. Definicja

Wybudzanie głosem (VAD): Aktywne nasłuchiwanie i wykrywanie aktywności głosowej.

Autoryzacja biometryczna: Weryfikacja tożsamości użytkownika za pomocą odcisku palca.

Integracja z Home Assistant: Przesyłanie poleceń głosowych do sterowania inteligentnym domem.

Energooszczędność: Optymalizacja pod kątem zasilania bateryjnego.

Zbieranie metryk: Wysyłanie danych (np. stan baterii, statusy operacji) do analizy.

---

### 2. Hardware (ESP32)

- **PCB:** Projektowane w KiCad, montaż ręczny.
- **Mikrofon z VAD:** Knowles SPH0641LU4H (moduł breakout).
- **Czytnik linii papilarnych:** R307 alternatywa AS608 lub FPM10A (UART).
- **Zasilanie:** Moduł ładowarki 2S z balanserem (IP2326, USB-C).
- **Monitorowanie baterii:** Dzielnik napięcia + ADC.
- **Akumulatory:** 2x Li-ion 18650 (6.0V–8.4V).
- **Konwersja napięcia:** Step-down 5V + LDO 3.3V.
- **Zarządzanie zasilaniem:** MOSFET (np. 2N7000) do odłączania czytnika.
- **Diody LED 0805:**
  - Czerwona/Zielona: ładowanie, autoryzacja.
  - Niebieska: nasłuch, oczekiwanie, błąd.
- **Przycisk Tact Switch:** Restart, przywracanie firmware.

---

### 3. Software

- **Firmware:** ESPHome (YAML) — szybka integracja z Home Assistant.
- **Alternatywa:** MicroPython — większa elastyczność, więcej kodu.
- **Tryb uśpienia:** Deep Sleep + wybudzanie przez VAD.
- **Logika stanów:** `UŚPIONY`, `CZEKA_NA_ODCISK`, `AUTORYZOWANY_NAGRYWA`, `BŁĄD`.
- **Komunikacja:** MQTT / HTTP POST do Home Assistant.
- **Przetwarzanie audio:** Docker z `Whisper`, `Piper`.
- **Zarządzanie energią:** MOSFET sterowany programowo.
- **Zarządzanie użytkownikami:** Tryb rejestracji odcisków.
- **OTA:** Aktualizacje Over-the-Air.
- **Metryki:** InfluxDB + Grafana (TrueNAS na Proxmox).
- **Dostęp zdalny:** ZeroTier.
- **Przycisk wielofunkcyjny:**
  - 3 sekundy: restart.
  - 10 sekund: przywrócenie stabilnej wersji.

---

### 4. Schemat i obliczenia

- Dane techniczne z kart katalogowych: mikrofon, czytnik, ładowarka, MOSFET.

---

### 5. Obudowa

- **Projekt:** Solid Edge.
- **Wykonanie:** Druk 3D, dopasowany do PCB, baterii, czytnika i diod.
- **Komunikacja:** Wi-Fi do integracji z siecią domową.

---

### 6. Kosztorys (szacunkowy)

Komponent | Cena (PLN) |
---|---|
Mikrofon Knowles SPH0641LU4H | 15–50 zł |
Czytnik linii papilarnych R307 | 15–25 zł |
Moduł ładowania TP4056 | 3–5 zł |
Akumulator Li-ion 18650 (2x) | 20–40 zł |
Tranzystor MOSFET (2N7000) | 1–2 zł |
Diody LED i inne komponenty | 5–10 zł |
ESP32 | 8–15 zł |
Suma minimalna | ok. 67 zł |
Suma maksymalna | ok. 147 zł |
---

