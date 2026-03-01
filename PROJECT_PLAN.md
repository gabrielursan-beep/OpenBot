# OpenBot Max — Plan Proiect

## Status: WAVE ROVER MIGRATION — FIRMWARE READY (1 Mar 2026)

**Obiectiv curent:** Am migrat de la DIY body (Arduino Nano + L298N + cablare manuala) la **Waveshare Wave Rover** — chassis complet asamblat cu ESP32, TB6612FNG motor driver, INA219 battery monitor, OLED, encodere, UPS. Zero cablare complicata. Firmware-ul `openbot.ino` a fost adaptat cu config WAVE_ROVER. Se asteapta livrarea hardware-ului.

---

## 1. CONFIGURATIE

| Parametru | Valoare |
|---|---|
| Body | **Waveshare Wave Rover** (complet asamblat) |
| Phone mount | Inclus (suport 1/4" surub) |
| MCU | ESP32-WROOM-32 (pe placa Wave Rover) |
| Motor Driver | TB6612FNG (cablat pe placa) |
| Motoare | 4x N20 cu encoder quadrature |
| Battery monitor | INA219 (I2C addr 0x42) |
| OLED | 0.91" SSD1306 128x32 (I2C) |
| UPS | 3x 18650 (7800mAh) cu protectie |
| Conectare telefon | BLE (Bluetooth Low Energy) |
| Telefon | Google Pixel 10 |
| Amazon.de | B0CF55LM6Q (~€80) |

---

## 2. DE CE WAVE ROVER?

| Criteriu | DIY (inainte) | Wave Rover (acum) |
|---|---|---|
| Cablare | ~30 fire manuale, breadboard, L298N | Zero — totul pe placa |
| Motoare | TT DC fara encoder real | N20 cu encoder quadrature |
| Voltage monitor | Voltage divider manual | INA219 pe I2C (precis) |
| Conectare telefon | USB OTG (cablu fizic) | BLE (wireless) |
| Timp asamblare | ~3-4 ore | ~15 min (baterii + sonar + LED) |
| Cost | ~€100+ (piese separate) | ~€80 (all-in-one) |

---

## 3. LISTA PIESE

### De comandat

| # | Componenta | Sursa | Cost est. | Status |
|---|---|---|---|---|
| 1 | Waveshare Wave Rover (B0CF55LM6Q) | Amazon.de | ~€80 | DE COMANDAT |

### Refolosim din build-ul DIY anterior

| # | Componenta | Sursa originala |
|---|---|---|
| 1 | 3x 18650 Sony VTC6 | Bitmi |
| 2 | HC-SR04 senzor ultrasonic | Bitmi |
| 3 | Fire Dupont mama-mama (4 fire pt sonar) | Bitmi |
| 4 | Rezistori 10kΩ + 20kΩ (voltage divider ECHO) | Bitmi (set 20 valori) |
| 5 | Incarcator 18650 | Bitmi |

### NU mai folosim (raman spare)

- Arduino Nano + L298N + body 3D printat
- Suport baterii extern + switch
- Speed sensor IR + discuri encoder
- LED-uri galbene (nu se monteaza)
- Cablu USB-C OTG (Wave Rover foloseste BLE, nu USB)
- Suruburi M3

### Ce avem deja

- Google Pixel 10 (configurat, OpenBot APK instalat)
- Bambu Lab P2S (imprimanta 3D — nu e nevoie pt Wave Rover)

---

## 4. WAVE ROVER — GPIO PIN MAP

Totul pe placa Wave Rover este deja cablat (motoare, encodere, INA219, OLED, IMU). Singurele conexiuni externe sunt HC-SR04 si LED-urile.

### ESP32 Pin Map (Wave Rover)

```
GPIO  Functie                   Status
────  ────────────────────────  ──────
25    Motor A PWM (stanga)      PE PLACA
21    Motor A IN1               PE PLACA
17    Motor A IN2               PE PLACA
26    Motor B PWM (dreapta)     PE PLACA
22    Motor B IN1               PE PLACA
23    Motor B IN2               PE PLACA
35    Encoder A CH_A            PE PLACA
27    Encoder B CH_A            PE PLACA
32    I2C SDA                   PE PLACA (INA219+OLED+IMU)
33    I2C SCL                   PE PLACA
4     HC-SR04 TRIGGER           EXTERN (fir Dupont)
5     HC-SR04 ECHO              EXTERN (cu voltage divider 10k+20k)
```

### Singura conexiune externa: HC-SR04 (4 fire Dupont)

```
HC-SR04       Wave Rover Header
───────       ──────────────────
VCC  ───────  5V
GND  ───────  GND
TRIG ───────  GPIO4
ECHO ───────  GPIO5 (prin voltage divider: 10kΩ + 20kΩ → 3.33V)
```

### Voltage divider pe ECHO (5V → 3.3V safe pt ESP32)

```
HC-SR04 ECHO ── [10kΩ] ──┬── [20kΩ] ── GND
                           │
                        GPIO5
```

---

## 5. ASAMBLARE + TEST — CHECKLIST

Wave Rover vine COMPLET asamblat. Singurele operatii fizice:

### Faza 1: Unboxing + baterii
- [ ] Deschide cutia Wave Rover
- [ ] Introdu 3x 18650 Sony VTC6 in UPS-ul Wave Rover
- [ ] Verifica ca porneste (switch ON, LED-uri pe placa)

### Faza 2: Backup factory firmware
- [ ] Conecteaza Wave Rover la Mac prin USB-C
- [ ] `esptool.py --port /dev/tty.usbserial-* read_flash 0 ALL waveshare_factory_backup.bin`
- [ ] Salveaza backup-ul in loc sigur!

### Faza 3: Flash OpenBot firmware
- [ ] `arduino-cli compile --fqbn esp32:esp32:esp32 firmware/openbot/openbot.ino`
- [ ] `arduino-cli upload -p /dev/tty.usbserial-* --fqbn esp32:esp32:esp32 firmware/openbot/openbot.ino`

### Faza 4: Conecteaza HC-SR04 (4 fire Dupont — singura cablare!)
- [ ] HC-SR04 VCC → 5V (header expansiune Wave Rover)
- [ ] HC-SR04 GND → GND
- [ ] HC-SR04 TRIG → GPIO4
- [ ] HC-SR04 ECHO → GPIO5 (prin voltage divider: 10kΩ serie + 20kΩ la GND)

### Faza 5: Phone mount
- [ ] Monteaza suportul de telefon (surub 1/4", vine in cutie)

### Faza 6: Test BLE
- [ ] Deschide OpenBot app pe Pixel 10
- [ ] Bluetooth → cauta "OpenBot: WAVE_ROVER"
- [ ] Conecteaza

### Faza 7: Test functionalitate
- [ ] Robot Info → verifica tensiune (9.6-12.6V)
- [ ] Robot Info → verifica encodere (wheel speed)
- [ ] Robot Info → verifica sonar (distance)
- [ ] OLED → afiseaza voltage, RPM, distance
- [ ] Free Roam → test motoare ambele directii
- [ ] Object Tracking → test autonom

### Faza 8: Calibrare encodere
- [ ] Masoara distanta reala vs raportata
- [ ] Ajusteaza TICKS_PER_REV in firmware daca e nevoie
- [ ] Re-flash si re-test

---

## 6. FIRMWARE

Fisier: `firmware/openbot/openbot.ino`

```c
#define OPENBOT WAVE_ROVER
#define MCU ESP32
#define HAS_BLUETOOTH 1
#define HAS_INA219 1
#define HAS_VOLTAGE_DIVIDER 0
#define HAS_INDICATORS 0
#define HAS_SONAR 1
#define HAS_SPEED_SENSORS_FRONT 1
#define HAS_OLED 1
```

**Motor control:** TB6612FNG — PWM + 2 direction pins per motor (IN1/IN2 for direction, PWM for speed). Coast mode = both LOW, brake = both HIGH.

**Voltage:** INA219 (I2C addr 0x42) — `getBusVoltage_V() + getShuntVoltage_mV()/1000`. No voltage divider needed.

**Encodere:** N20 quadrature, TICKS_PER_REV = 1400 (calibrare dupa test).

**I2C pins:** SDA=GPIO32, SCL=GPIO33 (custom, `Wire.begin(32,33)` before OLED init).

**Librarii necesare:**
- INA219_WE (Wolfgang Ewald)
- Adafruit SSD1306
- Adafruit GFX

**Flash cu arduino-cli:**
```bash
arduino-cli compile --fqbn esp32:esp32:esp32 firmware/openbot/openbot.ino
arduino-cli upload -p /dev/tty.usbserial-* --fqbn esp32:esp32:esp32 firmware/openbot/openbot.ino
```

**IMPORTANT:** Backup factory firmware Wave Rover INAINTE de flash!

---

## 7. APP ANDROID

- **APK:** https://app.openbot.org/robot (sau GitHub releases v0.8.0)
- **Telefon:** Google Pixel 10 — deja configurat, OpenBot APK instalat
- **Conectare:** Bluetooth → "OpenBot: WAVE_ROVER"
- **Moduri:** Free Roam, Data Collection, Autopilot, Object Tracking, Point Goal Nav, Controller Mapping, Robot Info

---

## 8. MAX BRAIN — LATER

Brain-ul AI e deployed pe Render si functional. Il integram dupa ce robotul fizic merge.

| Detaliu | Valoare |
|---|---|
| URL | `https://max-brain.onrender.com` |
| Repo | `github.com/gabrielursan-beep/openbot-max` (privat) |
| Service ID | `srv-d6bgusogjchc73aj989g` |
| Stack | FastAPI + Claude + ElevenLabs + Google APIs |
| Voce | Jora Slobod, accent romanesc (`eleven_multilingual_v2` + `ro`) |
| Wake word | "Max" |
| Cron | Morning briefing L-V 09:00 |

Fisiere: `max_brain/server/` (deploy Render) + `max_brain/client/` (telefon).

---

## 9. TROUBLESHOOTING

| Problema | Solutie |
|---|---|
| ESP32 nu apare in IDE/CLI | Instaleaza driver CP2102 (inclus de obicei in macOS) |
| Motoare nu merg | Verifica firmware WAVE_ROVER; check PIN_AIN1/AIN2/BIN1/BIN2 |
| Motoare merg invers | Swap AIN1<->AIN2 sau BIN1<->BIN2 in firmware |
| BLE nu apare | Verifica `HAS_BLUETOOTH 1`; restart ESP32 |
| Tensiune = 0 | Verifica INA219 addr 0x42; I2C SDA=32, SCL=33 |
| Sonar = 0 cm | Verifica TRIG=GPIO4, ECHO=GPIO5; voltage divider pe ECHO |
| OLED nu afiseaza | `Wire.begin(32,33)` trebuie inainte de `display.begin()` |
| Encodere citesc 0 | Verifica PIN_SPEED_LF=35, PIN_SPEED_RF=27; INPUT_PULLUP |
| Factory restore | `esptool.py --port /dev/tty.usbserial-* write_flash 0 waveshare_factory_backup.bin` |

---

## 10. REFERINTE

- **Repo oficial:** https://github.com/isl-org/OpenBot
- **Instructiuni asamblare:** `body/diy/README.md` (DIY Option 1)
- **Wiring diagram:** `docs/images/wiring_diagram.png`
- **Firmware docs:** `firmware/README.md`
- **Android releases:** https://github.com/isl-org/OpenBot/releases
