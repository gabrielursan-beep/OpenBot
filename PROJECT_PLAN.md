# OpenBot - Plan Proiect FULL OPTIONS

## Status: IN LUCRU — Piese comandate, printare 3D in curs, software voce gata de test

---

## 1. CONFIGURATIE ALEASA

| Parametru | Valoare |
|---|---|
| Body | **DIY Block Body Big LEGO** (3D print) + Camera Elevator |
| MCU | Arduino Nano (ATmega328P) |
| Motor Driver | L298N |
| Conectare telefon | USB OTG (cablu) |
| Versiune | **FULL OPTIONS** — toate senzoriile si accesoriile |
| Imprimanta 3D | **Bambu Lab P2S** |
| Filament | **Bambu Lab PLA Matte Orange** |
| Telefon | **Google Pixel 10** (Tensor G5, 12GB RAM, 128GB) |
| Voce AI | **Max Brain** — Whisper + Claude + ElevenLabs |
| Limba | Romana (accent romanesc) |

---

## 2. IMPRIMANTA 3D — BAMBU LAB P2S

### Specificatii Relevante

| Parametru | Valoare |
|---|---|
| Build volume | **256 x 256 x 256 mm** |
| Viteza maxima miscare | 600 mm/s |
| Acceleratie maxima | 20,000 mm/s² |
| Nozzle inclus | 0.4mm hardened steel |
| Temperatura maxima nozzle | 300°C |
| Temperatura maxima heatbed | 110°C |
| Build plate | Textured PEI |
| Camera inchisa | Da (50°C chamber ready) |
| Conectivitate | WiFi, Bluetooth, USB |
| AMS compatibil | Da (AMS 2 Pro) |

### Compatibilitate cu OpenBot

| Cerinta OpenBot | Bambu Lab P2S | Status |
|---|---|---|
| Build plate min 240 x 150mm | 256 x 256mm | INCAPE LEJER |
| PLA support | Da, nativ | PERFECT |
| 0.4mm nozzle | Inclus standard | PERFECT |
| 0.2mm layer height | Da | PERFECT |

**Concluzie:** Piesa cea mai mare (block_body_bottom = 221x150mm) incape confortabil pe P2S cu 17mm margine. Nu e nevoie de varianta Slim sau Glueable.

---

## 3. FILAMENT — BAMBU LAB PLA MATTE ORANGE

### Setari Print (specifice P2S + PLA Matte)

| Parametru | Valoare |
|---|---|
| Filament | Bambu Lab PLA Matte Orange, 1.75mm |
| Detectie | **Automata via RFID** (Bambu Studio citeste spool-ul) |
| Temperatura nozzle | **210°C** (range: 190-220°C) |
| Temperatura bed | **35-45°C** (textured PEI, camera inchisa) |
| Cooling fan | **Auto** (Bambu Studio default; off primele 1-2 layere) |
| Max volumetric speed | ~12-15 mm³/s (PLA Matte standard) |
| Retraction | Gestionata automat de Bambu Studio |
| Uscare filament | 50°C / 8 ore (daca e absorbit umiditate) |

**IMPORTANT:** Pe Bambu Lab P2S cu filament original Bambu Lab, pur si simplu incarci STL-ul in Bambu Studio, selectezi profilul PLA Matte (sau lasi RFID-ul sa-l detecteze automat), si printezi. Nu trebuie sa faci tuning manual.

---

## 4. PIESE DE PRINTAT

### Fisiere STL (Block Body Big LEGO + Camera Elevator)

| # | Piesa | Fisier STL (cale relativa in repo) | Dimensiuni Aprox | Timp Estimat P2S |
|---|---|---|---|---|
| 1 | Block body bottom | `body/diy/cad/block_body/block_body_bottom.stl` | 221 x 150mm | ~4-5h |
| 2 | Block body top big LEGO | `body/diy/cad/block_body/block_body_top_big_lego.stl` | 221 x 150mm | ~4-5h |
| 3 | Camera elevator | `body/rc_truck/cad/rc_truck_body/camera_elevator.stl` | mic | ~15-20min |
| 4 | Phone mount bottom | `body/phone_mount/phone_mount_bottom.stl` | mic | ~30-45min |
| 5 | Phone mount top | `body/phone_mount/phone_mount_top.stl` | mic | ~20-30min |
| | **TOTAL** | **5 piese** | | **~9-11h** |

**Nota:** Timpii sunt estimati pentru P2S la viteza standard (nu Ludicrous). P2S e semnificativ mai rapid decat imprimantele generic — o piesa de 13.5h pe Ender devine ~4-5h pe P2S.

**De ce Block Body Big LEGO?**
- Mai mult spatiu interior = cablare mai usoara, electronica incape mai confortabil
- Suprafata LEGO-compatibila pe top = poti monta accesorii, senzori, decoratiuni din LEGO
- Camera elevator ridica phone mount-ul mai sus = camera vede mai bine cand te ridici in picioare sau cand Max te urmareste

**Nota Camera Elevator:** Piesa este din proiectul RC Truck dar e compatibila — se monteaza intre body top si phone mount bottom cu aceleasi suruburi M3x25 (sau M3x35 daca e nevoie de suruburi mai lungi).

### Profil Bambu Studio pentru OpenBot

| Parametru | Valoare | Note |
|---|---|---|
| Printer | Bambu Lab P2S 0.4mm nozzle | Selecteaza in Bambu Studio |
| Filament | Bambu PLA Matte | Auto-detectat via RFID |
| Layer height | **0.20mm** (Standard) | Profil "0.20mm Standard" |
| Wall loops | 3 | Rezistenta structurala buna |
| Top/bottom layers | 4 | Finisaj solid |
| Infill | **30%** | Mai solid, ideal pentru robot in miscare |
| Infill pattern | **Triangle** | Rezistenta excelenta in toate directiile |
| Supports | **Da** (Generate Support: Yes, Pattern: Concentric, Density: 15%) | Recomandat pt Block Body |
| Build plate adhesion | **Brim** (optional) | Recomandat pt body_bottom (piesa mare) |
| Seam position | **Nearest** | Minimizeaza vizibilitatea cusaturii |
| Print speed | **Default Bambu Studio** | P2S gestioneaza automat |

### Pasi Printare in Bambu Studio

1. Deschide **Bambu Studio**
2. Selecteaza printer: **Bambu Lab P2S**
3. Incarca STL-ul (drag & drop sau File > Import)
4. Filament: se detecteaza automat via RFID, sau selecteaza manual **Bambu PLA Matte**
5. Profil: **0.20mm Standard**
6. Slice (butonul Slice Plate)
7. Verifica preview-ul (fara probleme evidente)
8. Send to Printer (WiFi) sau Export to SD card
9. Printeaza

### Ordine Recomandata de Printare

1. **camera_elevator.stl** (~15-20 min) — piesa mica, test rapid sa verifici ca totul merge
2. **phone_mount_top.stl** (~20-30 min) — a doua piesa mica
3. **phone_mount_bottom.stl** (~30-45 min) — a treia piesa mica
4. **block_body_top_big_lego.stl** (~4-5h) — piesa mare cu LEGO studs
5. **block_body_bottom.stl** (~4-5h) — piesa cea mai mare, printeaz-o ultima dupa ce esti sigur pe setari

### Post-Processing dupa Print

1. Scoate piesa de pe textured PEI (se dezlipeste usor dupa racire)
2. Curata suporturile daca ai folosit (probabil nu e cazul)
3. Verifica fitment-ul motorilor in sloturile din body_bottom
4. Indeparteaza eventualele stringing sau blobs cu un cutter

---

## 5. LISTA COMPLETA DE PIESE — COMANDA BITMI.RO

### A. De comandat de pe Bitmi.ro (toate IN STOC, livrare 1-2 zile)

| # | Componenta | Produs Bitmi | Pret | Qty | Subtotal | Link Bitmi.ro |
|---|---|---|---|---|---|---|
| 1 | Arduino Nano | Placa compatibila Arduino Nano V3 CH340G | 27.44 RON | 1 | 27.44 RON | [Bitmi](https://www.bitmi.ro/electronica/placa-de-dezvoltare-compatibila-arduino-nano-v3-ch340g-10360.html) |
| 2 | L298N Motor Driver | Modul driver L298N cu punte H dubla | 11.99 RON | 1 | 11.99 RON | [Bitmi](https://www.bitmi.ro/electronica/modul-driver-l298n-cu-punte-h-dubla-pentru-motoare-dc-stepper-10400.html) |
| 3 | TT Motor + roata | Set motor DC 3V-6V cu reductor si roata | 9.99 RON | **4** | 39.96 RON | [Bitmi](https://www.bitmi.ro/set-motor-dc-3v-6v-cu-reductor-si-roata-11227.html) |
| 4 | Senzor Ultrasonic | Senzor ultrasonic HC-SR04 | 6.09 RON | 1 | 6.09 RON | [Bitmi](https://www.bitmi.ro/electronica/senzor-ultrasonic-hc-sr04-10406.html) |
| 5 | Speed Sensor | Modul senzor fotoelectric IR masurare viteza | 4.26 RON | **2** | 8.52 RON | [Bitmi](https://www.bitmi.ro/electronica/modul-senzor-fotoelectric-ir-pentru-masurarea-vitezei-10410.html) |
| 6 | Display OLED | Ecran OLED 0.96" I2C SSD1306 128x64 | 18.98 RON | 1 | 18.98 RON | [Bitmi](https://www.bitmi.ro/electronica/ecran-oled-0-96-cu-interfata-iic-i2c-10488.html) |
| 7 | Baterii 18650 | Acumulator Li-Ion 18650 3000mAh Sony Murata VTC6 | 44.17 RON | **3** | 132.51 RON | [Bitmi](https://www.bitmi.ro/electrice/acumulator-li-ion-18650-3-6v-3000mah-30a-sony-murata-us18650vtc6-10596.html) |
| 8 | Suport baterii 18650 | Suport prindere acumulator 18650 (interconectabile) | 2.09 RON | **3** | 6.27 RON | [Bitmi](https://www.bitmi.ro/electronica/suport-de-prindere-pentru-acumulatori-litiu-18650-10557.html) |
| 9 | Incarcator 18650 | Incarcator 4 porturi 18650 Li-Ion 3.7V | 44.99 RON | 1 | 44.99 RON | [Bitmi](https://www.bitmi.ro/electrice/incarcator-cu-4-porturi-pentru-acumulatori-18650-10157.html) |
| 10 | Fire Dupont tata-mama | 40x Fire Dupont tata-mama 30cm | 7.99 RON | 1 | 7.99 RON | [Bitmi](https://www.bitmi.ro/electronica/40-fire-dupont-tata-mama-30cm-10504.html) |
| 11 | Fire Dupont mama-mama | 40x Fire Dupont mama-mama 20cm | 8.99 RON | 1 | 8.99 RON | [Bitmi](https://www.bitmi.ro/electronica/40-x-fire-dupont-mama-mama-20cm-10509.html) |
| 12 | Set rezistori | Set 400 buc, 20 valori, 10ohm-1Mohm, 1/4W | 19.99 RON | 1 | 19.99 RON | [Bitmi](https://www.bitmi.ro/electronica/set-rezistori-20-de-valori-400-bucati-10-10m-1-4w-11255.html) |
| | | | | **TOTAL BITMI:** | **333.72 RON** | |

**Nota baterii:** Poti reduce costul cu baterii alternative de pe Bitmi:
- [LG MJ1 3500mAh — 39.xx RON/buc](https://www.bitmi.ro/electrice/acumulator-li-ion-18650-3-6v-3400mah-10a-lg-inr18650-mj1-10598.html) (mai multa capacitate, mai ieftin)
- [Sanyo 2470mAh — ~25 RON/buc](https://www.bitmi.ro/electrice/acumulator-li-ion-18650-3-6v-2470mah-8a-sanyo-ur18650zm2-10854.html) (buget)

**Nota rezistori:** Set-ul include 10k ohm dar NU include 150 ohm si 20k ohm. Inlocuitori din set:
- In loc de 150 ohm → foloseste **220 ohm** (LED un pic mai slab, functioneaza perfect)
- In loc de 20k ohm → foloseste **22k ohm** (factor divisor 3.2 in loc de 3.0, diferenta neglijabila)

### B. De cumparat SEPARAT (nu sunt pe Bitmi)

| # | Componenta | Qty | De unde | Pret Estimat |
|---|---|---|---|---|
| 1 | Suruburi M3x25 | 16 buc | Dedeman / Bricostore / AliExpress | ~5-10 RON |
| 2 | Piulite M3 | 16 buc | Dedeman / Bricostore / AliExpress | ~3-5 RON |
| 3 | Suruburi M3x5 | 6 buc | Dedeman / Bricostore / AliExpress | ~3-5 RON |
| 4 | LED-uri portocalii 5mm | 2 buc | Magazin electronice / AliExpress | ~2-3 RON |
| 5 | Cablu USB OTG (Micro-USB sau USB-C) | 1 | eMag / Altex / Amazon | ~10-20 RON |
| 6 | Intrerupator On/Off mic | 1 | Magazin electronice / AliExpress | ~2-3 RON |
| 7 | Arc sau elastic (phone mount) | 1 | Ai acasa / orice magazin | ~0 RON |

### C. Ce ai deja

| Componenta | Status |
|---|---|
| Bambu Lab P2S (imprimanta 3D) | AI |
| Bambu Lab PLA Matte Orange (filament) | AI |

---

## 6. COST TOTAL ESTIMAT

| Sursa | Cost |
|---|---|
| **Bitmi.ro** (comanda principala) | **~334 RON** |
| **Alte surse** (suruburi M3, LED, OTG, switch) | **~25-45 RON** |
| **Google Pixel 10** (eMag) | **3,398 RON** |
| **Filament PLA** (~150-200g din spool) | **~10-15 RON** |
| **TOTAL PROIECT (fara telefon)** | **~370-395 RON** |
| **TOTAL PROIECT (cu telefon)** | **~3,770-3,800 RON** |

*API costs (Claude + ElevenLabs) — platite lunar, separate. Estimat: ~5-15 EUR/luna la utilizare normala.*

---

## 7. SCHEMA CONEXIUNI (WIRING)

### Arduino Nano Pin Map (Full Options DIY)

```
Arduino Nano          Componenta
─────────────         ────────────────────────────────
D2  ────────────────  Speed Sensor STANGA (OUT)
D3  ────────────────  Speed Sensor DREAPTA (OUT)
D4  ────────────────  LED Indicator STANGA (prin R 220 ohm din set Bitmi)
D5  ────────────────  L298N ENA (PWM Motor Stanga 1)
D6  ────────────────  L298N IN1 (PWM Motor Stanga 2)
D7  ────────────────  LED Indicator DREAPTA (prin R 220 ohm din set Bitmi)
D9  ────────────────  L298N ENB (PWM Motor Dreapta 1)
D10 ────────────────  L298N IN2 (PWM Motor Dreapta 2)
D11 ────────────────  HC-SR04 ECHO
D12 ────────────────  HC-SR04 TRIGGER
A4  ────────────────  OLED SDA (I2C)
A5  ────────────────  OLED SCL (I2C)
A7  ────────────────  Divisor Tensiune (punct mijloc R1/R2)
5V  ────────────────  HC-SR04 VCC / Speed Sensors VCC / OLED VCC
GND ────────────────  GND comun (toate componentele)
```

### Divisor Tensiune (Battery Monitor)

```
Baterie (+) ──── [R1 = 22k ohm] ──┬── [R2 = 10k ohm] ──── GND
                                   │
                               Arduino A7

Factor = (22k + 10k) / 10k = 3.2
Tensiune maxima masurabila: 5V x 3.2 = 16V (suficient pentru 3S = 12.6V)
Nota: Folosim 22k din set-ul Bitmi in loc de 20k. Diferenta e neglijabila.
```

### L298N Conexiuni

```
L298N              Conexiune
─────              ─────────
12V IN  ──────── Baterie (+) (prin switch On/Off)
GND     ──────── Baterie (-) / Arduino GND
5V OUT  ──────── Arduino 5V / distributor 5V
ENA     ──────── Arduino D5 (SCOATE JUMPER-UL!)
IN1     ──────── Arduino D6
IN2     ──────── (gestionat de firmware)
ENB     ──────── Arduino D9 (SCOATE JUMPER-UL!)
IN3     ──────── Arduino D10
IN4     ──────── (gestionat de firmware)
OUT1/2  ──────── Motoare STANGA (2 motoare in paralel)
OUT3/4  ──────── Motoare DREAPTA (2 motoare in paralel)
```

**CRITICAL: Scoate jumper-ele de pe ENA si ENB pe L298N! Fara asta, PWM-ul nu functioneaza si motoarele merg doar full speed sau deloc.**

---

## 8. FIRMWARE (DEJA CONFIGURAT FULL OPTIONS)

Fisierul `firmware/openbot/openbot.ino` a fost modificat cu toate flag-urile activate:

```c
#define OPENBOT DIY
#define MCU NANO
#define HAS_VOLTAGE_DIVIDER 1    // Monitor baterie activ
#define HAS_INDICATORS 1         // LED-uri semnalizare active
#define HAS_SONAR 1              // Senzor ultrasonic activ
#define SONAR_MEDIAN 1           // Filtru median sonar activ
#define HAS_SPEED_SENSORS_FRONT 1 // Encodere viteza roti active
#define HAS_OLED 1               // Display OLED activ
```

### Pasi Flash Firmware

1. Instaleaza **Arduino IDE** (https://www.arduino.cc/en/software)
2. Instaleaza librarii (Tools > Manage Libraries):
   - `PinChangeInterrupt` by Nico Hood
   - `Adafruit SSD1306`
   - `Adafruit GFX Library`
3. Deschide `firmware/openbot/openbot.ino`
4. Board: **Tools > Board > Arduino AVR Boards > Arduino Nano**
5. Processor: **Tools > Processor > ATmega328P (Old Bootloader)**
6. Port: **Tools > Port > selecteaza portul COM corect**
7. Click **Upload** (sageata dreapta)

**Nota:** Daca Arduino Nano e clone chinezesc, instaleaza driverul CH340:
- macOS: https://github.com/WCHSoftGroup/ch34xser_macos
- Windows: https://www.wch-ic.com/downloads/CH341SER_EXE.html

---

## 9. APLICATIE ANDROID

### Instalare (cea mai simpla cale)

1. Pe telefon, deschide: **https://app.openbot.org/robot**
2. Descarca si instaleaza APK-ul
3. Permite "Install from unknown sources" cand te intreaba

### Alternativ: descarca de pe GitHub

Versiunea curenta: **v0.8.0** — https://github.com/isl-org/OpenBot/releases

### Sau compileaza din sursa (avansat)

```bash
cd /Users/gabrielursan/Projects/OpenBot/android
./gradlew robot:assembleDebug
# APK in: robot/build/outputs/apk/debug/
```

### Telefoane Testate si Confirmate

| Telefon | Procesor | Status |
|---|---|---|
| Samsung S22 Ultra | Exynos 2200 | Testat OK |
| Samsung S20 FE 5G | Snapdragon 865 | Testat OK |
| Google Pixel 6XL | Tensor | Testat OK |
| Google Pixel 4XL | Snapdragon 855 | Testat OK |
| Xiaomi Mi 9 | Snapdragon 855 | Testat OK |

**Minim:** Android 7.0+, telefon din 2018+ cu procesor decent.

**Telefonul NOSTRU: Google Pixel 10** — Tensor G5, 12GB RAM, Android 16.
Cel mai bun chip pentru ML on-device (TPU optimizat pt TFLite). Perfect pentru Whisper + Object Detection.

### Moduri Disponibile in App

| Mod | Descriere |
|---|---|
| **Free Roam** | Control manual cu telemetrie live (viteza, baterie, distanta) |
| **Data Collection** | Inregistreaza date senzori pt antrenament ML |
| **Autopilot** | Condus autonom cu model TFLite pre-antrenat |
| **Object Tracking** | Urmarire obiecte — 80 clase COCO (persoana, caine, masina, etc.) |
| **Point Goal Navigation** | Navigare AR catre coordonate GPS |
| **Controller Mapping** | Configurare gamepad Bluetooth (PS4/Xbox) |
| **Robot Info** | Diagnostic — citeste toti senzorii in timp real |

### Modele ML Pre-instalate

- **MobileNetV1-300** — object detection default
- **Autopilot Float** — model de condus autonom
- **Navigation** — goal-based navigation
- Alte modele downloadabile din app: YOLOv4-tiny, YOLOv5s/m/l, EfficientDet

---

## 10. TELEFON — GOOGLE PIXEL 10

### De ce Pixel 10?

| Spec | Valoare | Relevanta OpenBot |
|---|---|---|
| Procesor | **Google Tensor G5** (3nm TSMC) | Cel mai bun chip pt TFLite/ML on-device |
| RAM | **12GB** | Suficient pt Whisper + Object Detection + App simultan |
| TPU | **60% mai puternic** vs Tensor G4 | Inferenta ML ultra-rapida |
| Camera | 50MP principal + ultrawide | Excelenta pt Object Tracking si viziune |
| USB | **USB-C 3.2** | Conexiune rapida la Arduino via OTG |
| Android | **Android 16** | Cel mai recent, suport complet OpenBot |
| Stocare | 128GB | Suficient pt modele ML si date |
| 5G | Da | Internet rapid pt API calls (Claude, ElevenLabs) |

### Pret si Status

| Detail | Valoare |
|---|---|
| Pret | **3,398 RON** (eMag) |
| Culoare | Indigo |
| Status | **COMANDAT — vine azi** |

### De cumparat separat

- **Cablu USB-C OTG** (USB-C la USB-A) — pentru conectare Arduino Nano la Pixel 10
- **Suport auto cu ventilatie** (optional) — daca vrei sa il folosesti si ca dashcam

---

## 11. CONTROL VOCAL — MAX BRAIN (AI VOICE ASSISTANT)

### Arhitectura Hybrid (Server + Client)

```
[Telefon/Client]                    [Server Render.com]
+----------------+    WebSocket     +--------------------+
| Whisper STT    | ---- text -----> | FastAPI app.py     |
| Wake word      |                  |   +-- Claude AI    |
| Audio player   | <-- audio+text - |   +-- ElevenLabs  |
| Robot control  | <-- robot cmds - |   +-- Google APIs  |
+----------------+                  |   +-- Memory DB    |
                                    |   +-- Cron jobs    |
                                    +--------------------+
```

**Telefonul** face: STT (Whisper), audio playback, senzori, robot control.
**Serverul** face: Claude AI, TTS, Google APIs, memory, cron jobs.

Protocol WebSocket:
```
Client -> Server: {"type": "command", "text": "...", "user": "Gabriel"}
Server -> Client: {"type": "status", "message": "Thinking...", "model": "sonnet"}
Server -> Client: {"type": "tool", "name": "read_emails", "status": "executing"}
Server -> Client: {"type": "response", "text": "...", "audio_base64": "..."}
Server -> Client: {"type": "robot_action", "command": "forward", "duration_seconds": 3}
```

### Componente Software

| Componenta | Tehnologie | Rol |
|---|---|---|
| Speech-to-Text | **Whisper** (on-device, Pixel 10 TPU) | Transcrie vocea in text romanesc |
| AI Brain | **Claude Sonnet 4.6** (rapid) / **Opus 4.6** (complex) | Intelege comanda, genereaza raspuns + actiune |
| Text-to-Speech | **ElevenLabs** `eleven_multilingual_v2` | Voce Serban Popescu, accent romanesc |
| Wake Word | **"Max"** | Robotul raspunde doar cand e strigat |

### Configuratie Voce (IMPORTANT — Accent Romanesc)

```python
# ElevenLabs — FORTEAZA accent romanesc, NU englezesc
model_id = "eleven_multilingual_v2"   # Model multilingv (NU turbo_v2_5!)
language_code = "ro"                   # Forteaza limba romana
voice_id = "8nBBDfYxYXmDNaqTCxPH"    # Serban Popescu
similarity_boost = 0.85               # Fidelitate mare la vocea originala romaneasca
stability = 0.6
style = 0.15
use_speaker_boost = True
```

**ATENTIE:** Daca schimbi modelul la `eleven_turbo_v2_5`, accentul devine englezesc!
Pastreaza intotdeauna `eleven_multilingual_v2` + `language_code: "ro"`.

### Selectia Automata a Modelului Claude

| Tip comanda | Model | Latenta | Exemplu |
|---|---|---|---|
| Comenzi de miscare | Sonnet 4.6 | ~1-2s | "Max, mergi inainte" |
| Intrebari simple | Sonnet 4.6 | ~1-2s | "Max, cat e ceasul?" |
| Intrebari complexe | Opus 4.6 | ~3-5s | "Max, explica-mi cum functioneaza gravitatia" |
| Conversatie filozofica | Opus 4.6 | ~3-5s | "Max, ce crezi despre AI?" |

Cuvinte cheie care activeaza Opus: `explica`, `de ce`, `cum functioneaza`, `filozofie`, `parere`, `analizeaza`, `compara`, `gandeste`, `povesteste`, `detaliat`, `argumenteaza`, `pro si contra`, `ce crezi`.

### Actiuni Robot Disponibile

| Actiune ID | Descriere | Comanda vocala exemplu |
|---|---|---|
| `forward` | Merge inainte | "Max, mergi inainte" |
| `backward` | Merge inapoi | "Max, da-te inapoi" |
| `left` | Vireaza stanga | "Max, la stanga" |
| `right` | Vireaza dreapta | "Max, la dreapta" |
| `stop` | Opreste-te | "Max, opreste-te" |
| `speed_up` | Accelereaza | "Max, mai repede" |
| `slow_down` | Incetineste | "Max, incetineste" |
| `track_person` | Urmareste persoana | "Max, urmareste-ma" |
| `track_object` | Urmareste obiect | "Max, urmareste mingea" |
| `autopilot_on` | Porneste autopilot | "Max, mergi singur" |
| `autopilot_off` | Opreste autopilot | "Max, opreste autopilotul" |
| `look` | Descrie ce vezi | "Max, ce vezi?" |
| `status` | Raporteaza status | "Max, cum stai cu bateria?" |
| `dance` | Danseaza | "Max, danseaza!" |

### Personalitatea lui Max

- Prietenos, entuziast si usor amuzant
- Raspunde scurt (max 2-3 propozitii) la comenzi de miscare
- Raspunde mai detaliat la intrebari si conversatii
- Se adreseaza informal (cu "tu")
- Raspunde cand e strigat "Max"
- Nu foloseste emoji, markdown, sau formatare — doar text vorbit natural

### Fisiere Max Brain (Hybrid)

```
max_brain/
+-- server/                         # Deploy pe Render.com
|   +-- app.py                      # FastAPI + WebSocket + REST
|   +-- config.py                   # Configuratie (env vars)
|   +-- claude_brain.py             # Claude AI agentic loop
|   +-- tools.py                    # Tool definitions (~30 tools)
|   +-- memory.py                   # SQLite memory system
|   +-- elevenlabs_voice.py         # TTS (return bytes, no playback)
|   +-- google_auth.py              # OAuth2 + API Key auth
|   +-- gmail_service.py            # Gmail API
|   +-- calendar_service.py         # Google Calendar
|   +-- whatsapp_service.py         # WhatsApp (Green-API)
|   +-- drive_service.py            # Google Drive
|   +-- sheets_service.py           # Google Sheets
|   +-- docs_service.py             # Google Docs
|   +-- tasks_service.py            # Google Tasks
|   +-- maps_service.py             # Google Maps
|   +-- air_quality_service.py      # Air Quality API
|   +-- smarthome_service.py        # Home Assistant
|   +-- requirements.txt            # fastapi, uvicorn, websockets
|   +-- render.yaml                 # Render.com deploy config
+-- client/                         # Ruleaza pe telefon/laptop
|   +-- max_client.py               # WebSocket client + audio playback
|   +-- requirements.txt            # websockets
```

### Securitate Chei API

**Local:** Cheile API sunt in `.env` la radacina proiectului (GITIGNORED).
**Server:** Env vars se seteaza direct pe Render.com dashboard.
Google OAuth token: `GOOGLE_TOKEN_JSON` env var (JSON string cu access + refresh token).

```
Env vars necesare:
- ANTHROPIC_API_KEY (Claude API)
- ELEVENLABS_API_KEY (ElevenLabs TTS)
- MAX_SERVER_KEY (autentificare client-server)
- GOOGLE_MAPS_API_KEY (Maps, Air Quality)
- GOOGLE_TOKEN_JSON (OAuth2 token, pe server)
- GOOGLE_CREDENTIALS_JSON (OAuth2 credentials, pe server)
- GMAIL_USER, GREEN_API_*, HOME_ASSISTANT_*
```

### Rulare

**Server local:**
```bash
cd max_brain/server
pip install -r requirements.txt
uvicorn app:app --host 0.0.0.0 --port 8000 --reload
```

**Client local:**
```bash
cd max_brain/client
pip install -r requirements.txt
python max_client.py --url ws://localhost:8000/ws
```

**Client cu server Render:**
```bash
python max_client.py --url wss://max-brain.onrender.com/ws --key YOUR_KEY
```

### Deploy pe Render.com

1. Push pe GitHub
2. Render > New > Web Service > Connect repo
3. Root Directory: `max_brain/server`
4. Build: `pip install -r requirements.txt`
5. Start: `uvicorn app:app --host 0.0.0.0 --port $PORT`
6. Seteaza env vars in dashboard
7. Google OAuth: ruleaza auth local, copiaza token in GOOGLE_TOKEN_JSON env var

---

## 12. ORDINE DE EXECUTIE (CHECKLIST)

### Faza 1: Printare 3D (Bambu Lab P2S) — IN CURS
- [ ] Deschide Bambu Studio
- [ ] Selecteaza printer: Bambu Lab P2S
- [ ] Profil: 0.20mm Standard, Bambu PLA Matte, Infill 30%, Triangle, Supports ON (Concentric 15%)
- [ ] **STL-urile sunt in folderul `print_stl/` — deschide direct de acolo**
- [ ] Print #1: `camera_elevator.stl` — test rapid (~15-20 min)
- [ ] Print #2: `phone_mount_top.stl` (~20-30 min)
- [ ] Print #3: `phone_mount_bottom.stl` (~30-45 min)
- [ ] Print #4: `block_body_top_big_lego.stl` (~4-5h)
- [ ] Print #5: `block_body_bottom.stl` (~4-5h)
- [ ] Curata piesele printate dupa racire
- [ ] Verifica fitment-ul camera elevator intre body top si phone mount

### Faza 2: Comanda Piese Electronice — DONE
- [x] Comanda de pe Bitmi.ro toate cele 12 produse din Sectiunea 5A (~334 RON)
- [ ] Comanda separat: suruburi M3x25 (16), piulite M3 hex (16), suruburi M3x5 (6) — Dedeman/Bricostore
- [ ] Comanda separat: 2x LED portocaliu 5mm + 1x intrerupator On/Off mic
- [x] Comanda cablu USB-C OTG (USB-C la USB-A) — pentru Pixel 10
- [ ] Verifica ca ai ciocan de lipit, fludor, si multimetru

### Faza 3: Pregatire Pixel 10 — CAND VINE TELEFONUL (azi)
- [ ] Scoate din cutie si configureaza initial (Android 16)
- [ ] Activeaza Developer Options (Settings > About > tap Build Number x7)
- [ ] Activeaza USB Debugging (Settings > Developer Options > USB Debugging)
- [ ] Instaleaza OpenBot APK (https://app.openbot.org/robot)
- [ ] Testeaza camera — functioneaza OK?
- [ ] Testeaza microfonul — inregistreaza o proba vocala
- [ ] Instaleaza Whisper (cand integram voice control pe Android)

### Faza 4: Asamblare Mecanica
- [ ] Lipeste fire la cele 4 motoare (ciocan de lipit)
- [ ] Pune discurile encoder pe cele 2 motoare din FATA
- [ ] Monteaza cele 4 motoare pe body_bottom cu 16x M3x25 + 16x piulite M3
- [ ] Monteaza L298N pe body_bottom cu 4x M3x5
- [ ] Monteaza senzorul ultrasonic HC-SR04 in slotul din fata

### Faza 5: Cablare Electronica
- [ ] **SCOATE jumper-ele ENA si ENB de pe L298N**
- [ ] Conecteaza motoarele stanga la OUT1 (+) / OUT2 (-) pe L298N
- [ ] Conecteaza motoarele dreapta la OUT4 (+) / OUT3 (-) pe L298N
- [ ] Construieste distribuitor 5V/GND (perfboard + header 6x2)
- [ ] Conecteaza 5V OUT de pe L298N la distribuitor
- [ ] Cableaza Arduino Nano conform schemei din Sectiunea 7
- [ ] Monteaza speed sensors pe cele 2 motoare din fata
- [ ] Monteaza LED-urile portocalii (D4 si D7 prin rezistori 220 ohm din set Bitmi)
- [ ] Conecteaza divisorul de tensiune (22k ohm + 10k ohm din set Bitmi, la A7)
- [ ] Conecteaza OLED display (SDA=A4, SCL=A5, VCC=5V, GND)
- [ ] Monteaza switch On/Off pe firul pozitiv al bateriei
- [ ] Monteaza suportul de baterii 18650

### Faza 6: Firmware
- [ ] Instaleaza Arduino IDE
- [ ] Instaleaza driverul CH340 (daca Arduino e clone)
- [ ] Instaleaza librariile: PinChangeInterrupt, Adafruit SSD1306, Adafruit GFX
- [ ] Deschide `firmware/openbot/openbot.ino`
- [ ] Verifica ca flag-urile sunt pe 1 (deja configurat)
- [ ] Board: Arduino Nano, Processor: ATmega328P (Old Bootloader)
- [ ] Upload firmware

### Faza 7: Testare Hardware (inainte de asamblare finala)
- [ ] Verifica tensiune baterie cu multimetru (9.6-12.6V)
- [ ] Verifica 5V pe output-ul L298N
- [ ] Testeaza motoarele individual
- [ ] Verifica senzorul ultrasonic (pune mana in fata, verifica distanta)
- [ ] Verifica LED-urile indicator (clipesc?)
- [ ] Verifica OLED display (arata ceva?)
- [ ] Verifica speed sensors (invarte roata, citeste?)

### Faza 8: App Android + Test Basic
- [ ] Conecteaza Pixel 10 cu USB-C OTG la Arduino
- [ ] Deschide app-ul > **Robot Info** > Verifica toti senzorii
- [ ] Testeaza **Free Roam** (control manual din app)
- [ ] Testeaza **Object Tracking** (pune un obiect in fata)
- [ ] Testeaza **Autopilot** (cu model pre-instalat)

### Faza 9: Integrare Voice Control (Max Brain)
- [ ] Portare `max_brain/` pe Android (Kotlin/Java wrapper pt API calls)
- [ ] Integreaza Whisper on-device pe Pixel 10 (whisper.cpp sau whisper-android)
- [ ] Implementeaza wake word detection ("Max")
- [ ] Conecteaza pipeline: Whisper STT → Claude API → ElevenLabs TTS
- [ ] Ruta actiuni de la Claude catre OpenBot motor control
- [ ] Implementeaza camera vision (trimite frame base64 la Claude cu `look`)
- [ ] Testeaza accent romanesc pe device (ElevenLabs multilingual_v2 + ro)
- [ ] Optimizeaza latenta end-to-end (target: < 3 secunde)
- [ ] Adauga conversation history (memoria conversatiei)

### Faza 10: Asamblare Finala
- [ ] Monteaza block_body_top_big_lego pe block_body_bottom cu 2x M3x5
- [ ] Monteaza camera_elevator pe body_top (intre body si phone mount)
- [ ] Monteaza phone_mount_bottom pe camera_elevator (suruburi M3x25 sau M3x35)
- [ ] Monteaza phone_mount_top cu arc/elastic
- [ ] Pune Pixel 10 in mount
- [ ] Conecteaza USB-C OTG
- [ ] Test complet: voce + miscare + viziune
- [ ] GATA! Max e functional!

---

## 13. STRUCTURA PROIECT (FISIERE IMPORTANTE)

```
OpenBot/
├── .env                                   ← CHEI API (GITIGNORED!)
├── .gitignore                             ← Include .env, __pycache__, venv/
├── PROJECT_PLAN.md                        ← ACEST DOCUMENT
├── firmware/openbot/openbot.ino           ← FIRMWARE (configurat full options)
├── print_stl/                             ← FOLDER CU TOATE STL-URILE DE PRINTAT
│   ├── 1_camera_elevator.stl              ← PRINT #1 (test rapid)
│   ├── 2_phone_mount_top.stl              ← PRINT #2
│   ├── 3_phone_mount_bottom.stl           ← PRINT #3
│   ├── 4_block_body_top_big_lego.stl      ← PRINT #4 (piesa mare)
│   └── 5_block_body_bottom.stl            ← PRINT #5 (piesa mare, ultima)
├── body/diy/
│   ├── cad/block_body/                    ← Sursa STL-uri body
│   └── README.md                          ← Instructiuni asamblare oficiale
├── body/phone_mount/                      ← Sursa STL-uri phone mount
├── body/rc_truck/cad/rc_truck_body/       ← Sursa camera_elevator.stl
├── android/
│   ├── robot/                             ← App-ul principal robot
│   └── controller/                        ← App controller (telefon #2, optional)
├── max_brain/                             ← VOICE CONTROL MODULE (hybrid server+client)
│   ├── README.md                          ← Documentatie Max Brain
│   ├── server/                            ← Deploy pe Render.com
│   │   ├── app.py                         ← FastAPI + WebSocket + REST
│   │   ├── config.py                      ← Configuratie (env vars)
│   │   ├── claude_brain.py                ← Claude AI agentic loop
│   │   ├── tools.py                       ← Tool definitions (~30 tools)
│   │   ├── elevenlabs_voice.py            ← TTS (return bytes, no playback)
│   │   ├── google_auth.py                 ← OAuth2 + API Key auth
│   │   ├── *_service.py                   ← Gmail, Calendar, Drive, Sheets, etc.
│   │   ├── requirements.txt               ← fastapi, uvicorn, websockets
│   │   └── render.yaml                    ← Render.com deploy config
│   └── client/                            ← Ruleaza pe telefon/laptop
│       ├── max_client.py                  ← WebSocket client + audio playback
│       └── requirements.txt               ← websockets
└── docs/images/
    └── wiring_diagram.png                 ← Schema de conexiuni vizuala
```

---

## 14. TROUBLESHOOTING

| Problema | Cauza Probabila | Solutie |
|---|---|---|
| Arduino nu apare in IDE | Driver lipsa | Instaleaza driver CH340 |
| Motoarele nu merg deloc | Jumper-ele ENA/ENB sunt pe L298N | **Scoate jumper-ele!** |
| Motoarele merg invers | Polaritate inversata | Inverseaza firele + si - la motor pe L298N |
| Un motor merge, altul nu | Conexiune slaba | Verifica lipiturile si OUT1-4 |
| Telefonul nu vede Arduino | Cablu OTG incompatibil | Incearca alt cablu; verifica USB debugging ON |
| Tensiune baterie citeste 0 | Divisor de tensiune gresit | Verifica 20k/10k si pinul A7 cu multimetru |
| Sonar citeste 0 cm | Pini inversati sau conector | Verifica Trigger=D12, Echo=D11 |
| OLED nu afiseaza nimic | I2C gresit | Verifica SDA=A4, SCL=A5; adresa I2C = 0x3C |
| Robot nu vireaza pe covor | Frictiune 4WD fara diferential | Normal; testeaza pe suprafata neteda |
| App crash pe telefon | Telefon prea vechi | Minim Android 7.0, procesor din 2018+ |
| Print se dezlipeste de pat | Adhesion | Adauga Brim in Bambu Studio; curata PEI plate |
| Print warped/curbat | Camera prea calda pt PLA | Deschide usa P2S in timpul printarii PLA |
| ElevenLabs accent englezesc | Model gresit | Foloseste `eleven_multilingual_v2` + `language_code: "ro"` |
| Claude returneaza JSON invalid | Markdown backticks | `claude_brain.py` stripuieste automat ```json fences |
| Max nu raspunde la voce | Whisper nu transcrrie | Verifica microfon, limba setata pe "ro" |
| Latenta prea mare (>5s) | Model Claude prea greu | Verifica ca folosesti Sonnet, nu Opus, pt comenzi simple |
| ElevenLabs 401 error | API key expirata/invalida | Verifica ELEVENLABS_API_KEY in .env |
| Claude 404 error | Model ID gresit | Verifica model: `claude-sonnet-4-6` (nu cu data suffix!) |

---

## 15. REFERINTE

- **Repo oficial:** https://github.com/isl-org/OpenBot
- **Site oficial:** https://www.openbot.org/
- **Instructiuni asamblare:** `body/diy/README.md` in repo
- **Wiring diagram:** `docs/images/wiring_diagram.png` in repo
- **Android app releases:** https://github.com/isl-org/OpenBot/releases
- **Bambu Lab P2S specs:** https://bambulab.com/en/p2s/specs
- **Bambu Studio download:** https://bambulab.com/en/download/studio
- **Bitmi.ro** (furnizor principal piese RO): https://www.bitmi.ro/
- **Claude API docs:** https://docs.anthropic.com/
- **ElevenLabs API docs:** https://elevenlabs.io/docs/api-reference
- **ElevenLabs Voice Library:** https://elevenlabs.io/app/agents/voice-library
- **Whisper (OpenAI):** https://github.com/openai/whisper
- **whisper.cpp (C++ port for mobile):** https://github.com/ggerganov/whisper.cpp
- **Google Pixel 10:** https://store.google.com/product/pixel_10
