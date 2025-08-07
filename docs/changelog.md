# Changelog - IoT ESP32 Voice Authentication Device

Wszystkie znaczące zmiany w projekcie będą dokumentowane w tym pliku.

Format oparty na [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
projekt używa [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Planowane
- Projekt schematu PCB w KiCad
- Wybór konkretnych modeli komponentów
- Projekt obudowy 3D w Solid Edge
- Implementacja firmware ESPHome
- Testy prototypu na breadboard

---

## [0.2.0] - 2025-08-07

### 🔧 Changed - Korekcje techniczne
- **BREAKING**: ESP32 → ESP32-S3 (więcej RAM dla audio processing)
- **BREAKING**: P-channel MOSFET → N-channel MOSFET (łatwiejsze sterowanie)
- **BREAKING**: Deep Sleep → Light Sleep (ciągły VAD)
- Głośnik 2-3W → 4W (margines bezpieczeństwa dla MAX98357A)
- Aktualizacja kosztorysu: 72-167 PLN

### ✅ Added - Nowe funkcjonalności 
- AS608 jako alternatywa dla R307 w kosztorysie
- Parametry energetyczne (szacunkowe czasy pracy)
- Szczegółowa architektura systemu
- Schemat blokowy zasilania
- Automat stanów systemu
- Konfiguracja pinów ESP32-S3

### 🐛 Fixed - Poprawki błędów
- Usunięto duplikację nagłówka w README
- Wyjaśniono VAD jako funkcję software'ową
- Skorygowano informacje o TP4056 (tylko single cell)
- Ujednolicono nazewnictwo komponentów
- Poprawiono niespójności w kosztorysie

### 📚 Documentation
- Utworzono `docs/architecture.md` - kompletna architektura systemu
- Utworzono `docs/decisions.md` - historia decyzji projektowych  
- Utworzono `docs/changelog.md` - ten plik
- Utworzono `docs/qa.md` - pytania i odpowiedzi

---

## [0.1.0] - 2025-08-07

### ✅ Added - Pierwsza wersja
- Podstawowa koncepcja urządzenia IoT z autoryzacją głosową
- Wybór głównych komponentów:
  - ESP32 jako mikrocontroller
  - INMP441 jako mikrofon I2S
  - R307 jako czytnik linii papilarnych
  - MAX98357 jako wzmacniacz audio
- Koncepcja zasilania 2x 18650 Li-ion
- Struktura folderów projektu
- Podstawowy README.md z opisem funkcjonalności

### 🎯 Project Scope
- Wybudzanie głosem (VAD)
- Autoryzacja biometryczna (fingerprint)
- Integracja z Home Assistant
- Optymalizacja energetyczna
- Zbieranie metryk

### 💰 Budget
- Wstępny kosztorys: 65-127 PLN
- Decyzja o recyklingu baterii z GLO (oszczędność ~40 PLN)

### 🏗️ Infrastructure
- Struktura projektu z folderami:
  - `/firmware/` - kod ESP32
  - `/hardware/` - schematy PCB
  - `/enclosure/` - modele 3D
  - `/docs/` - dokumentacja
  - `/docker/` - kontenery dla audio processing

---

## [0.0.0] - 2025-08-07

### 🎬 Project Genesis
- Początkowa idea projektu
- Utworzenie repozytorium
- Podstawowa struktura folderów

---

## 📋 Typy zmian

- **Added** - nowe funkcjonalności
- **Changed** - zmiany w istniejących funkcjonalnościach  
- **Deprecated** - funkcjonalności które będą usunięte
- **Removed** - usunięte funkcjonalności
- **Fixed** - poprawki błędów
- **Security** - poprawki bezpieczeństwa
- **BREAKING** - zmiany łamiące kompatybilność

## 🎯 Milestone Timeline

### Phase 1: Design (Q3 2025)
- [x] Koncepcja i wybór komponentów
- [x] Architektura systemu  
- [ ] Schemat PCB w KiCad
- [ ] Projekt obudowy 3D
- [ ] Zamówienie komponentów

### Phase 2: Prototype (Q4 2025)
- [ ] Montaż prototypu na breadboard
- [ ] Implementacja firmware ESPHome
- [ ] Testy funkcjonalności
- [ ] Optymalizacja energetyczna
- [ ] Integracja z Home Assistant

### Phase 3: Production (Q1 2026)
- [ ] Finalizacja PCB
- [ ] Druk obudowy 3D
- [ ] Montaż końcowy
- [ ] Testy long-term
- [ ] Dokumentacja użytkownika

### Phase 4: Enhancement (Q2 2026)
- [ ] Dodatkowe funkcjonalności
- [ ] Optymalizacje wydajnościowe
- [ ] Alternatywne firmware (MicroPython)
- [ ] Wersja 2.0 hardware

---

**Format**: [Wersja] - YYYY-MM-DD  
**Konwencje**: Semantic Versioning (MAJOR.MINOR.PATCH)  
**Maintainer**: Project Team
