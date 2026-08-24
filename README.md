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
![Dashboard Hauptansicht]
*Das Responsive 2-Spalten-Layout auf dem Desktop.*
<img width="1600" height="887" alt="Screenshot 2026-08-24 095135" src="https://github.com/user-attachments/assets/e46ffc9e-1050-4b72-8b72-4a37b806c261" />

![Dashboard Mobile]
*Die optimierte 1-Spalten-Ansicht für mobile Endgeräte.*
<img width="549" height="918" alt="Screenshot 2026-08-24 095220" src="https://github.com/user-attachments/assets/5ae38f84-7e9f-45ac-9b3f-b62c335ae683" />


### Konfiguration
![Globale Einstellungen]
*Zentrale Konfiguration für Wasserfass und Watchdogs.*
<img width="520" height="754" alt="Screenshot 2026-08-24 095309" src="https://github.com/user-attachments/assets/2fc29b8b-f593-4bb9-b03f-c58f92324a54" />

![Pflanzennamen Setup]
*Zentrale Vergabe der Pflanzennamen in den globalen Einstellungen.*
<img width="533" height="506" alt="Screenshot 2026-08-24 095258" src="https://github.com/user-attachments/assets/1ad855d4-3897-4641-916f-8dc4160eff52" />


### Feinjustierung der Pflanzen
![Feinjustierung Tröpfchen]
*Beispiel: Klassisches Gießen mit Start-/Zielwert und Sickerpausen.*
<img width="513" height="567" alt="Screenshot 2026-08-24 105505" src="https://github.com/user-attachments/assets/3833a239-f6f6-4e24-8c0a-7977c8816305" />

![Feinjustierung Untersetzer]
*Beispiel: Untersetzer-Modus mit langer Sperrzeit nach dem Fluten.*
<img width="526" height="472" alt="Screenshot 2026-08-24 105532" src="https://github.com/user-attachments/assets/ca4b359d-ce65-41ae-a133-8690ff3e2794" />

![Uhrzeitsteuerung & Notfall]
*Steuerung nach Uhrzeit und das Notfall-Setup.*
<img width="538" height="379" alt="Screenshot 2026-08-24 105514" src="https://github.com/user-attachments/assets/7c919bb4-a890-4a9a-9201-73c406db67ec" />

![Sonnensteuerung & Notfall]
*Dynamische Steuerung nach Sonnenstand und das Notfall-Setup.*
<img width="545" height="537" alt="Screenshot 2026-08-24 105544" src="https://github.com/user-attachments/assets/6598a505-8b60-41e8-8f59-561ecc60e1ed" />


### Tools
![Manuelle Korrektur]
*Fass befüllen oder Wasserverbrauch manuell korrigieren.*
<img width="542" height="284" alt="Screenshot 2026-08-24 105431" src="https://github.com/user-attachments/assets/e38ff588-c6be-460b-87ec-2e6eee3abf9b" />


### System
![System-Übersicht](Screenshot_2026-08-24_105706.png)
*Manuelle Kontrolle aller Hardware-Komponenten (Pumpe, Ventile & Trockenlaufschutz).*
<img width="530" height="628" alt="Screenshot 2026-08-24 105706" src="https://github.com/user-attachments/assets/c0530f64-9929-4684-b313-7d23d404d7c2" />


### Tools & Historie
![Logbuch](Gemini_Generated_Image_8ncgtd8ncgtd8ncg.jpg)
*Smartes Logbuch mit Historie über Dauer, Verbrauch und Liter pro Stunde (L/h).*
<img width="513" height="567" alt="Screenshot 2026-08-24 105505" src="https://github.com/user-attachments/assets/27954695-1dcf-47cf-ad8b-151f54cea6f6" />


---

## 🛡️ Sicherheitskonzept (Die Watchdogs)

Da Wasserschäden auf Balkonen fatal sind, verfügt das System über mehrere redundante Sicherheitsmechanismen:
1. **Füllstandschutz:** Hartes Abschalten der Pumpe (Trockenlaufschutz), sobald das Restwasser ≤ Totvolumen fällt.
2. **Hardware-Trockenlaufschutz:** Zieht die Pumpe weniger als 150W Leistung (sie zieht Luft statt Wasser), wird sie in Sekunden blockiert.
3. **Dynamischer Laufzeit-Watchdog:** Berechnet das zulässige Limit aus der aktuell höchsten Impuls-Dauer der offenen Ventile plus 2 Minuten Puffer.
4. **Ghost-Prevention:** Schaltet die Pumpe sofort ab, falls kein Ventil geöffnet ist.

---

## 🛠️ Stückliste (Hardware & Komponenten)

- **Wassertank:** 60 Liter Wasserfass.
- **Pumpe:** T.I.P. Deep Inox (DIO) 45/13 (4-Zoll Tiefbrunnenpumpe).
- **Pumpen-Steuerung:** WLAN-Steckdose mit aktiver Strommessung (z.B. Shelly Plus Plug S).
- **Ventile:** 5 unabhängige Zonen/Magnetventile für individuelle Bewässerung (`switch.irrigation_valve_1` bis `5`).
- **Bodenfeuchtesensoren:** 5x Ecowitt GW1100A Soil Moisture Sensoren.
- **Klima-Sensoren:** Temperatur- & Luftfeuchtigkeitssensoren (z.B. Ecowitt oder Zigbee).

---

## 💻 Voraussetzungen & Software

- **Zentrale:** Home Assistant
- **HACS Frontend-Erweiterungen (Zwingend!):**
  - `custom:grid-layout`
  - `custom:fluid-level-background-card`
  - `custom:fold-entity-row`
  - `custom:template-entity-row`
  - `custom:hui-markdown-card`
  - `card-mod` (für dynamische CSS Anpassungen)

---

## 🎛️ Dokumentation der Einstellungsmöglichkeiten

Das Dashboard bietet vollständige Kontrolle über das System, ohne jemals den Code anfassen zu müssen.

### 1. Globale Einstellungen & Zuweisung
- **Fass Volumen (Max) & Totvolumen:** Definiert die Brutto/Netto-Mathematik des Fasses. Die Pumpe stoppt zwingend beim Erreichen des Totvolumens.
- **Wasserpuffer:** Warnschwelle (Vorwarnung), bevor das Totvolumen erreicht wird.
- **Watchdog / Hitze-Schwelle:** Definiere globale Limits für den Not-Aus und die Außentemperatur, ab der sich Sperrzeiten im Untersetzer-Modus automatisch verkürzen.
- **Zuweisung der Pflanzennamen:** Zentrale Namensvergabe. Die hier eingetragenen Namen werden automatisch im gesamten System (Dashboards, Ventile, Logbuch) übernommen.

### 2. System-Übersicht & Manuelle Korrektur
- **Hardware & Ventile:** Direkter Zugriff auf alle Relais. Schaltest du hier manuell, greift die "Ghost-Prevention" dennoch ein, falls du die Pumpe ohne offenes Ventil startest.
- **Manuelle Korrektur:** Wurde Wasser entnommen (z.B. Gießkanne), kann der berechnete Wasserverbrauch überschrieben werden. Bei einem frisch befüllten Fass genügt ein Klick auf "Wasserfass befüllt (RESET)".

### 3. Einzelpflanzen-Feinjustierung (Slots 1 bis 5)
Für jeden Slot lässt sich die Gießlogik separat definieren:
- **Untersetzer-Modus (Schalter):** 
  - **AUS:** Ideal für Tröpfchenbewässerung von oben. Du definierst einen Startwert (Min) und Zielwert (Max). Das System gießt in "Dauer Normal"-Impulsen und wartet dazwischen die "Sickerpause" ab, bis der Zielwert erreicht ist.
  - **AN:** Ideal zum Fluten von Untersetzern. Das System flutet einmalig (Dauer Normal) und blockiert den Slot danach für die "Sperrzeit (h)", damit die Pflanze das Wasser aufsaugen kann.
- **Durchfluss (L/h):** Der Durchfluss des jeweiligen Strangs. Dient zur exakten mathematischen Berechnung des Wasserverbrauchs für das Logbuch und die Restwasser-Anzeige.
- **Sonne statt Uhrzeit (Schalter):**
  - **AUS:** Gießfreigabe über feste Start- und Endzeiten.
  - **AN:** Gießfreigabe dynamisch nach Sonnenstand, justierbar über "Minuten nach Aufgang" und "Minuten vor Untergang".
- **Notfall-Setup:** Fällt die Bodenfeuchtigkeit unter das "Notfall-Limit", ignoriert das System sämtliche Uhrzeiten oder Sonnenstände und feuert sofort einen Impuls in Höhe der "Dauer Notfall" ab. Danach greift eine separate "Notfall-Sperrzeit".

---

## 🚀 Installation & Setup

1. **Abhängigkeiten installieren:** Stelle sicher, dass alle oben genannten HACS-Karten installiert sind.
2. **YAML-Dateien einfügen:** Kopiere die Inhalte der bereitgestellten Dateien (`automations.yaml`, `scripts.yaml`, `helpers.yaml`, `template.yaml`) in deine eigene Home Assistant Konfiguration. (Tipp: Nutze idealerweise Home Assistant Packages).
3. **Dashboard anlegen:** Erstelle ein neues Dashboard und füge den Code aus `dashboard.yaml` über den Raw-Konfigurationseditor ein.
4. **Platzhalter anpassen:**
   - In der `template.yaml`: Trage deinen eigenen Außentemperatur-Sensor im Proxy-Sensor `sensor.referenztemperatur_bewaesserung` ein.
   - In der `scripts.yaml`: Passe in der `globale_benachrichtigung` deinen eigenen `notify`-Dienst an.
   - Tausche ggf. die Entitäten für Pumpe und Ventile gegen deine eigenen aus.
