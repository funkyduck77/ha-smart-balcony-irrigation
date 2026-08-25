# 🌱 Home Assistant Balkon-Bewässerungssystem

Ein intelligentes, vollautomatisiertes und ausfallsicheres Bewässerungssystem für den Balkon. Vollständig integriert in Home Assistant mit dynamischer Füllstandsberechnung, mehreren Fallback-Ebenen (Watchdogs) und individueller Gießlogik für bis zu 5 Pflanzen (Slots).

## 💡 Key Features
- **Brutto vs. Netto Füllstandsberechnung:** Striktes Trennen von physischem Wasser und nutzbarem Wasser (Totvolumen der Pumpe).
- **Hybrid-Steuerung:** Gießen nach Uhrzeit (oder Sonnenauf-/untergang) in Kombination mit echter Bodenfeuchte.
- **Untersetzer-Modus vs. Tröpfchen:** Intelligente Sperrzeiten nach dem Fluten des Untersetzers (inkl. Hitze-Bypass) oder Sickerpausen beim Gießen von oben.
- **Multi-Level Watchdogs:** Hardware-Trockenlaufschutz via aktiver Strommessung und dynamische Laufzeitlimits.
- **Smartes Logbuch:** Zeichnet jeden Gießvorgang inkl. Dauer, Verbrauch und Art (Manuell/Automatisch) auf.

---

## 📸 Screenshots & Dashboard

### Hauptansichten
*Das Responsive 2-Spalten-Layout auf dem Desktop.*
<br>
[<img width="800" height="443" alt="Dashboard Hauptansicht" src="https://github.com/user-attachments/assets/e46ffc9e-1050-4b72-8b72-4a37b806c261" />](https://github.com/user-attachments/assets/e46ffc9e-1050-4b72-8b72-4a37b806c261)

*Die optimierte 1-Spalten-Ansicht für mobile Endgeräte.*
<br>
[<img width="274" height="459" alt="Dashboard Mobile" src="https://github.com/user-attachments/assets/5ae38f84-7e9f-45ac-9b3f-b62c335ae683" />](https://github.com/user-attachments/assets/5ae38f84-7e9f-45ac-9b3f-b62c335ae683)

### Konfiguration
*Zentrale Konfiguration für Wasserfass und Watchdogs.*
<br>
[<img width="260" height="377" alt="Globale Einstellungen" src="https://github.com/user-attachments/assets/2fc29b8b-f593-4bb9-b03f-c58f92324a54" />](https://github.com/user-attachments/assets/2fc29b8b-f593-4bb9-b03f-c58f92324a54)

*Zentrale Vergabe der Pflanzennamen in den globalen Einstellungen.*
<br>
[<img width="266" height="253" alt="Pflanzennamen Setup" src="https://github.com/user-attachments/assets/1ad855d4-3897-4641-916f-8dc4160eff52" />](https://github.com/user-attachments/assets/1ad855d4-3897-4641-916f-8dc4160eff52)

### Feinjustierung der Pflanzen
*Beispiel: Klassisches Gießen mit Start-/Zielwert und Sickerpausen.*
<br>
[<img width="256" height="283" alt="Feinjustierung Tröpfchen" src="https://github.com/user-attachments/assets/3833a239-f6f6-4e24-8c0a-7977c8816305" />](https://github.com/user-attachments/assets/3833a239-f6f6-4e24-8c0a-7977c8816305)

*Beispiel: Untersetzer-Modus mit langer Sperrzeit nach dem Fluten.*
<br>
[<img width="263" height="236" alt="Feinjustierung Untersetzer" src="https://github.com/user-attachments/assets/ca4b359d-ce65-41ae-a133-8690ff3e2794" />](https://github.com/user-attachments/assets/ca4b359d-ce65-41ae-a133-8690ff3e2794)

*Steuerung nach Uhrzeit und das Notfall-Setup.*
<br>
[<img width="269" height="189" alt="Uhrzeitsteuerung & Notfall" src="https://github.com/user-attachments/assets/7c919bb4-a890-4a9a-9201-73c406db67ec" />](https://github.com/user-attachments/assets/7c919bb4-a890-4a9a-9201-73c406db67ec)

*Dynamische Steuerung nach Sonnenstand und das Notfall-Setup.*
<br>
[<img width="272" height="268" alt="Sonnensteuerung & Notfall" src="https://github.com/user-attachments/assets/6598a505-8b60-41e8-8f59-561ecc60e1ed" />](https://github.com/user-attachments/assets/6598a505-8b60-41e8-8f59-561ecc60e1ed)

### Tools
*Fass befüllen oder Wasserverbrauch manuell korrigieren.*
<br>
[<img width="271" height="142" alt="Manuelle Korrektur" src="https://github.com/user-attachments/assets/e38ff588-c6be-460b-87ec-2e6eee3abf9b" />](https://github.com/user-attachments/assets/e38ff588-c6be-460b-87ec-2e6eee3abf9b)

### System
*Manuelle Kontrolle aller Hardware-Komponenten (Pumpe, Ventile & Trockenlaufschutz).*
<br>
[<img width="265" height="314" alt="System-Übersicht" src="https://github.com/user-attachments/assets/c0530f64-9929-4684-b313-7d23d404d7c2" />](https://github.com/user-attachments/assets/c0530f64-9929-4684-b313-7d23d404d7c2)

### Historie
*Smartes Logbuch mit Historie über Dauer, Verbrauch und Liter pro Stunde (L/h).*
<br>
[<img width="256" height="283" alt="Logbuch" src="https://github.com/user-attachments/assets/27954695-1dcf-47cf-ad8b-151f54cea6f6" />](https://github.com/user-attachments/assets/27954695-1dcf-47cf-ad8b-151f54cea6f6)

---

## 🛡️ Sicherheitskonzept (Die Watchdogs)

Da Wasserschäden auf Balkonen gelinde gesagt ungünstig sind und Pumpen nicht trockenlaufen oder gegen große Widerstände arbeiten dürfen, verfügt das System über fünf redundante Sicherheitsmechanismen. Fällt eine Ebene aus, greift sofort die nächste:

**1. Füllstandschutz (Software-Trockenlaufschutz)**
Das System berechnet kontinuierlich das verbleibende Wasser im Fass über Gießzeit und angegebenen Durchfluss. Erreicht dieser berechnete Wert das von dir in den globalen Einstellungen definierte "Totvolumen" (die Menge an Wasser, die nicht angesaugt werden kann, plus die Wasserverdrängung der Pumpe selbst), wird die Pumpe softwareseitig blockiert. Das verhindert, dass sie bei leerem Fass anläuft.

**2. Hardware-Trockenlaufschutz (Aktive Strommessung)**
Sollte der berechnete Wasserstand falsch sein (z. B. durch manuelle Entnahme mit der Gießkanne), greift diese physische Absicherung. Die smarte Steckdose überwacht den Stromverbrauch der Pumpe in Echtzeit. Zieht die Pumpe plötzlich weniger als 150 Watt Leistung, bedeutet das: Sie pumpt keinen Widerstand (Wasser) mehr, sondern zieht Luft. Das System blockiert die Pumpe innerhalb von Sekunden. 

**3. Dynamischer Laufzeit-Watchdog (Smartes Zeitlimit)**
Diese Funktion verhindert Überschwemmungen bei einem fehlerhaften Ablauf. Da das System die Ventile immer brav nacheinander gießt (Queued-Modus), prüft es bei jedem Start, welches Ventil gerade öffnet. Es nimmt die für genau diesen Slot geplante Gießdauer und addiert pauschal 2 Minuten als Sicherheitspuffer. Läuft die Pumpe bei diesem einen Durchgang unvorhergesehen länger als dieser errechnete Wert, kappt der Watchdog den Strom.

**4. Ghost-Prevention (Pumpen-Schutz)**
Wenn die Pumpe anspringt – sei es durch einen Glitch oder manuelles Schalten der Steckdose – ohne dass ein Ventil geöffnet ist, pumpt sie massiv gegen eine geschlossene Wand. Dies kann die Pumpe schwer beschädigen. Die Ghost-Prevention prüft sofort: *„Pumpe ist AN, aber alle Ventile sind ZU?“* und blockiert die Pumpe augenblicklich.

**5. Hard-Watchdog (Der absolute Not-Aus)**
Die letzte Fail-Safe-Ebene, falls alle anderen Skripte versagen sollten. Im Dashboard definierst du eine absolute Maximalzeit für den Dauerbetrieb der Pumpe. **Wichtig:** Dieser Wert muss mindestens 1 Minute höher eingestellt sein als deine längste Einzel-Gießlaufzeit! Überschreitet die Laufzeit diesen Wert, wird die Pumpe gnadenlos zwangsabgeschaltet.

---

## 🛠️ Stückliste (Hardware & Komponenten)

**Steuerung & Elektronik:**
- **Zentrale:** Home Assistant (inkl. HACS)
- **Ventil-Steuerung (Microcontroller):** ESP32 NodeMCU mit Terminalboard
- **Klima-Sensor (Hitze-Bypass):** IKEA TIMMERFLOTTE Temperatur-/Feuchtigkeitssensor smart
- **Bodenfeuchtesensoren:** 5x Ecowitt GW1100A Soil Moisture Sensoren
- **Pumpen-Steuerung:** IKEA TOFSMYGGA Steckdose für draußen (smart)
- **Netzteil (12V):** Schaltnetzteil 230V auf DC 12V 20A LED Transformator (240W)
- **Spannungswandler (für ESP32):** AC/DC 12V/24V zu DC 5V 5A 25W Wandler
- **Gehäuselüfter 40 mm 5V:** 2x optional, sollte auch ohne funktionieren. 

**Wasser & Gehäuse:**
- **Gehäuse:** Eurobox System Box Vollwand 40x30x12 cm, Grau inkl. Deckel
- **Wassertank:** 60 Liter Wasserfass
- **Pumpe:** T.I.P. Deep Inox (DIO) 45/13 (4-Zoll Tiefbrunnenpumpe)
- **Ventile:** 5x G1/4" elektronisches Magnetventil 12V (Funduino) für die Zonen (`switch.ventil_slot_1` bis `5`)
- **Schläuche & Tropfer:** Gardena Micro-Drip-System Tropfbewässerung Set Balkon
- **Gardena Adapter (statt Basisgerät):** Gardena Profi-System-Gerätestück 26,5 mm (G 3/4) & Gardena Hahn-Anschluss 4,6 mm (3/16")
- **Fittings (Verteiler):** 1/4" Wasserzulaufleitung Fitting Set (T + Y + I + L Typ)

---
 
### 💡 Alternative: Direkter Hausanschluss
Wenn du einen festen Wasseranschluss (Wasserhahn) auf dem Balkon hast, kannst du das Manifold auch direkt an die Hausleitung anschließen und dir das Wasserfass sowie die Pumpe sparen. 

*Der Anschluss auf diese Weise erfolgt auf eigene Verantwortung, da ich diese Anschlussmöglichkeit nicht getestet habe.*

**Wichtige Hinweise für diese Variante:**
- **Druckminderer (Zwingend erforderlich):** Ein Hausanschluss hat oft bis zu 4 Bar Druck. Du musst zwingend das klassische **Gardena Basisgerät 1000 oder 2000 (reduziert den Druck auf ca. 1,5 Bar)** *vor* das Manifold setzen, da sonst die Micro-Drip-Schläuche abplatzen. (Die 3D-Druckdatei für den speziellen Halter des Basisgerätes liegt den Druckdateien bei!).
- **Hauptventil (Optional, aber empfohlen):** Es wird empfohlen, den Hausanschluss nicht 24/7 unter Druck stehen zu lassen. Ein smartes Hauptventil (z. B. ein über Home Assistant steuerbares Magnetventil oder ein Zigbee-Bewässerungscomputer am Hahn) bringt zusätzliche Sicherheit vor Wasserschäden. 
- **Keine Code-Änderung nötig:** Die Logik ist bereits ab Werk für Hauptventile optimiert. Das System öffnet bei einem Gießvorgang *immer* erst das kleine Zonen-Ventil und schaltet 2 Sekunden später den Druck (die Pumpe / das Hauptventil) ein. Trage in der Installationstabelle einfach die Entität deines smarten Hauptventils bei `switch.pumpe_steckdose` ein.

---

## 📸 Aufbau & 3D-Druckteile

Damit die Elektronik und die Wasserverteilung (das Manifold) sicher und aufgeräumt untergebracht sind, ist das gesamte System in einer wetterfesten Eurobox verbaut. 

**🖨️ 3D-Druckdateien:**
Wenn du das System nachbauen möchtest, findest du alle von mir konstruierten Halterungen (für die Ventile, den ESP32 etc.) als fertige `.3mf`-Dateien direkt hier im Repository im Ordner [`/3d_druck`](./3d_druck).

**Bilder aus der Praxis:**
Hier siehst du, wie das Manifold (aus den 1/4" Fittings und Gardena-Adaptern) und die Elektronik im Gehäuse platziert wurden *(Bilder zum Vergrößern anklicken)*:

*Innenansicht der Eurobox / Manifold*
<br>
<a href="https://github.com/user-attachments/assets/c024af20-4ca3-4c12-9047-9c8ef93392bd"><img src="https://github.com/user-attachments/assets/c024af20-4ca3-4c12-9047-9c8ef93392bd" alt="Innenansicht der Eurobox / Manifold" width="300"></a>

*Ansicht Gehäuse unten*
<br>
<a href="https://github.com/user-attachments/assets/5b90ca3e-2273-432b-ac41-ec83036b4ba6"><img src="https://github.com/user-attachments/assets/5b90ca3e-2273-432b-ac41-ec83036b4ba6" alt="Ansicht Gehäuse unten" width="300"></a>

*Ansicht Gehäuse oben*
<br>
<a href="https://github.com/user-attachments/assets/c7473101-2318-4e1d-9d1b-5fa6da537081"><img src="https://github.com/user-attachments/assets/c7473101-2318-4e1d-9d1b-5fa6da537081" alt="Ansicht Gehäuse oben" width="300"></a>

*Ansicht Gehäuse geschlossen mit Kabelabdeckung*
<br>
<a href="https://github.com/user-attachments/assets/531e56e9-afdc-4778-a1e9-e41031fd6329"><img src="https://github.com/user-attachments/assets/531e56e9-afdc-4778-a1e9-e41031fd6329" alt="Ansicht Gehäuse geschlossen mit Kabelabdeckung" width="300"></a>

---

## 💻 Voraussetzungen & Software

- **Zentrale:** Home Assistant
- **HACS Frontend-Erweiterungen (Zwingend!):** Bitte suche und installiere folgende Karten über den Home Assistant Community Store (HACS), damit das Dashboard korrekt angezeigt wird:
  - `layout-card` (für das Responsive Grid-Layout)
  - `fluid-level-background-card` (für die animierte Wassertank-Anzeige)
  - `config-template-card`
  - `fold-entity-row` (für die aufklappbaren Menüs)
  - `template-entity-row`
  - `card-mod` (für dynamische CSS-Anpassungen, wie Farbwechsel bei leerem Tank)

---

## 🎛️ Dokumentation der Einstellungsmöglichkeiten

Das Dashboard bietet vollständige Kontrolle über das System, ohne jemals den Code anfassen zu müssen.

### Konfiguration
- **Fass Volumen (Max) & Totvolumen:** Definiert die Brutto/Netto-Mathematik des Fasses. Die Pumpe stoppt zwingend beim Erreichen des Totvolumens.
- **Wasserpuffer:** Warnschwelle (Vorwarnung), bevor das Totvolumen erreicht wird.
- **Watchdog / Hitze-Schwelle:** Definiere globale Limits für den Not-Aus und die Außentemperatur, ab der sich Sperrzeiten im Untersetzer-Modus automatisch verkürzen.
- **Zuweisung der Pflanzennamen:** Zentrale Namensvergabe. Die hier eingetragenen Namen werden automatisch im gesamten System (Dashboards, Ventile, Logbuch) übernommen.

### Feinjustierung der Pflanzen
Für jeden der 5 Slots lässt sich die Gießlogik separat definieren:
- **Untersetzer-Modus AUS:** Ideal für Tröpfchenbewässerung von oben. Du definierst einen Startwert (Min) und Zielwert (Max). Das System gießt in "Dauer Normal"-Impulsen und wartet dazwischen die "Sickerpause" ab, bis der Zielwert erreicht ist.
- **Untersetzer-Modus AN:** Ideal zum Fluten von Untersetzern. Das System flutet einmalig (Dauer Normal) und blockiert den Slot danach für die "Sperrzeit (h)", damit die Pflanze das Wasser aufsaugen kann.
- **Durchfluss (L/h):** Der Durchfluss des jeweiligen Strangs. Dient zur exakten mathematischen Berechnung des Wasserverbrauchs für das Logbuch und die Restwasser-Anzeige.
- **Sonne statt Uhrzeit AUS:** Gießfreigabe über feste Start- und Endzeiten.
- **Sonne statt Uhrzeit AN:** Gießfreigabe dynamisch nach Sonnenstand, justierbar über "Minuten nach Aufgang" und "Minuten vor Untergang".
- **Notfall-Setup:** Fällt die Bodenfeuchtigkeit unter das "Notfall-Limit", ignoriert das System sämtliche Uhrzeiten oder Sonnenstände und feuert sofort einen Impuls in Höhe der "Dauer Notfall" ab. Danach greift eine separate "Notfall-Sperrzeit".

### Tools
- **Manuelle Korrektur:** Wurde Wasser entnommen (z.B. Gießkanne), kann der berechnete Wasserverbrauch überschrieben werden. Bei einem frisch befüllten Fass genügt ein Klick auf "Wasserfass befüllt (RESET)".

### System
- **Hardware & Ventile:** Direkter Zugriff auf alle Relais. Schaltest du hier manuell, greift die "Ghost-Prevention" dennoch ein, falls du die Pumpe ohne offenes Ventil startest.

### Historie
- **Logbuch:** Smartes Logbuch, das jeden Gießvorgang inkl. Dauer, Verbrauch und Liter pro Stunde (L/h) lückenlos dokumentiert.

---

## 🚀 Installation & Setup

1. **Abhängigkeiten installieren:** Stelle sicher, dass alle oben genannten HACS-Karten installiert sind.
2. **YAML-Dateien einfügen:** Kopiere die bereitgestellten Hauptdateien (`automations.yaml`, `scripts.yaml`, `template.yaml`) sowie den kompletten Ordner `helpers` (inklusive der 4 darin liegenden Dateien) in deine eigene Home Assistant Konfiguration. 
3. **Dashboard anlegen:** Erstelle ein neues Dashboard und füge den Code aus `dashboard.yaml` über den Raw-Konfigurationseditor ein.
4. **⚠️ WICHTIG: Eigene Entitäten eintragen (Pflicht!)**
   Damit das System in deinem Home Assistant funktioniert, musst du die neutralen Platzhalter im Code durch deine tatsächlichen Entitäten ersetzen. Suche in den heruntergeladenen Dateien nach folgenden Platzhaltern und passe sie an:

| Neutraler Platzhalter im Code | Beschreibung / Deine Hardware | Betroffene Dateien |
| :--- | :--- | :--- |
| `switch.pumpe_steckdose` | Die smarte Steckdose/Relais deiner Pumpe | `dashboard.yaml`, `automations.yaml`, `scripts.yaml` |
| `sensor.pumpe_leistung` | Der Stromverbrauchssensor (W) deiner Pumpe | `automations.yaml` |
| `switch.ventil_slot_1` (bis `5`) | Die Relais/Ventile für Slot 1 bis 5 | `dashboard.yaml`, `automations.yaml`, `scripts.yaml`, `template.yaml` |
| `sensor.bodenfeuchte_slot_1` (bis `5`) | Deine Bodenfeuchtigkeitssensoren (0-100%) | `dashboard.yaml`, `automations.yaml` |
| `sensor.aussentemperatur` | Ein lokaler Temperatursensor für den Hitze-Bypass | `automations.yaml`, `template.yaml` |
| `notify.smartphone` | Dein Notify-Dienst (z.B. `notify.mobile_app_iphone`) | `scripts.yaml` |
| `tts.sprachausgabe` | Dein Text-to-Speech Dienst (z.B. `tts.google_translate_say`) | `scripts.yaml` |
| `media_player.smart_speaker` | Dein Smart-Speaker für Warnungen (z.B. `media_player.wohnzimmer`) | `scripts.yaml` |

*(Tipp: Wenn du keine Sprachausgabe für Warnungen nutzen möchtest, kannst du den `tts.speak`-Block in der `scripts.yaml` einfach löschen).*

---

## ⚠️ Disclaimer (Haftungsausschluss)

**Wasser und Strom sind eine gefährliche Kombination!** Der Nachbau dieses Projekts erfolgt ausdrücklich auf eigene Gefahr. Bitte achte auf eine fachgerechte und wasserdichte Isolierung der Elektronik, sichere 230V-Komponenten ordnungsgemäß ab und nutze zwingend einen FI-Schutzschalter (RCD) für den Betrieb im Außenbereich.
