# 🌱 Home Assistant Balkon-Bewässerungssystem

Ein intelligentes, vollautomatisiertes und ausfallsicheres Bewässerungssystem für den Balkon. Vollständig integriert in Home Assistant mit dynamischer Füllstandsberechnung, mehreren Fallback-Ebenen (Watchdogs) und individueller Gießlogik für bis zu 5 Pflanzen (Slots).

## 💡 Key Features
- **Brutto vs. Netto Füllstandsberechnung:** Striktes Trennen von physischem Wasser und nutzbarem Wasser (Totvolumen der Pumpe).
- **Hybrid-Steuerung:** Gießen nach Zeit (oder Sonnenauf-/untergang) und Bodenfeuchte.
- **Untersetzer-Modus:** Sperrzeiten nach dem Fluten des Untersetzers, inkl. Hitze-Bypass bei hohen Temperaturen.
- **Multi-Level Watchdogs:** Hardware-Trockenlaufschutz via Strommessung und dynamische Laufzeitlimits.

## 📸 Screenshots

![Dashboard Hauptansicht]
*Das Responsive 2-Spalten-Layout auf dem Desktop.*

![Dashboard Mobile]
*Die optimierte 1-Spalten-Ansicht für mobile Endgeräte.*

![Pflanzennamen Setup]
*Zentrale Vergabe der Pflanzennamen in den globalen Einstellungen.*

![Globale Einstellungen]
*Zentrale Konfiguration für Wasserfass und Watchdogs.*

## 🛡️ Sicherheitskonzept (Die Watchdogs)

Da Wasserschäden auf Balkonen fatal sind, verfügt das System über mehrere redundante Sicherheitsmechanismen:
1. **Füllstandschutz:** Hartes Abschalten der Pumpe (Trockenlaufschutz), sobald das Restwasser ≤ Totvolumen fällt[cite: 18].
2. **Hardware-Trockenlaufschutz:** Zieht die Pumpe weniger als 150W Leistung (sie zieht Luft statt Wasser), wird sie in Sekunden blockiert[cite: 18].
3. **Dynamischer Laufzeit-Watchdog:** Berechnet das zulässige Limit aus der aktuell höchsten Impuls-Dauer der offenen Ventile plus 2 Minuten Puffer[cite: 18].
4. **Ghost-Prevention:** Schaltet die Pumpe sofort ab, falls kein Ventil geöffnet ist[cite: 18].

## 🛠️ Stückliste (Hardware & Komponenten)

- **Wassertank:** 60 Liter Wasserfass[cite: 18].
- **Pumpe:** T.I.P. Deep Inox (DIO) 45/13 (4-Zoll Tiefbrunnenpumpe)[cite: 18].
- **Pumpen-Steuerung:** WLAN-Steckdose mit aktiver Strommessung (z.B. Shelly Plus Plug S)[cite: 18].
- **Ventile:** 5 unabhängige Zonen/Magnetventile für individuelle Bewässerung (`switch.irrigation_valve_1` bis `5`)[cite: 18].
- **Bodenfeuchtesensoren:** 5x Ecowitt GW1100A Soil Moisture Sensoren[cite: 18].
- **Klima-Sensoren:** Temperatur- & Luftfeuchtigkeitssensoren (z.B. Ecowitt oder Zigbee)[cite: 18].

## 💻 Voraussetzungen & Software

- **Zentrale:** Home Assistant
- **HACS Frontend-Erweiterungen (Zwingend!):**
  - `custom:grid-layout`
  - `custom:fluid-level-background-card`
  - `custom:fold-entity-row`
  - `custom:template-entity-row`
  - `custom:hui-markdown-card`
  - `card-mod` (für dynamische CSS Anpassungen)

## 🚀 Installation & Setup

1. **Abhängigkeiten installieren:** Stelle sicher, dass alle oben genannten HACS-Karten installiert sind.
2. **YAML-Dateien einfügen:** Kopiere die Inhalte der bereitgestellten Dateien (`automations.yaml`, `scripts.yaml`, `helpers.yaml`, `template.yaml`) in deine eigene Home Assistant Konfiguration. (Tipp: Nutze idealerweise Home Assistant Packages).
3. **Dashboard anlegen:** Erstelle ein neues Dashboard und füge den Code aus `dashboard.yaml` über den Raw-Konfigurationseditor ein.
4. **Platzhalter anpassen:**
   - In der `template.yaml`: Trage deinen eigenen Außentemperatur-Sensor im Proxy-Sensor `sensor.referenztemperatur_bewaesserung` ein.
   - In der `scripts.yaml`: Passe in der `globale_benachrichtigung` deinen eigenen `notify`-Dienst an.
   - Tausche ggf. die Entitäten für Pumpe und Ventile gegen deine eigenen aus.

## 🎛️ Bedienung & Konfiguration

**Globale Einstellungen:**
- **Fass Volumen (Max) & Totvolumen:** Definiert die Brutto/Netto-Mathematik[cite: 18].
- **Wasserpuffer:** Warnschwelle, bevor das Totvolumen erreicht wird[cite: 18].
- **Watchdog / Hitze-Schwelle:** Definiere globale Limits für den Not-Aus und ab wann sich Sperrzeiten im Untersetzer-Modus verkürzen.

**Einzelpflanzen-Feinjustierung:**
Für jeden der 5 Slots kannst du individuell einstellen:
- **Untersetzer-Modus (An/Aus):** Flutet den Untersetzer und sperrt das Ventil danach für X Stunden. Bei "Aus" (Gießen von oben) gilt stattdessen eine kurze Sickerpause zwischen den Impulsen.
- **Feuchte Min / Max:** Schwellenwerte für das Gießen.
- **Notfall-Limit:** Fällt die Feuchtigkeit unter diesen Wert, wird unabhängig von Uhrzeit oder Sperrzeiten ein Notfall-Gießimpuls ausgelöst.
- **Sonnen-Modus:** Ersetzt starre Start-/Endzeiten durch dynamische Sonnenaufgangs- und Sonnenuntergangs-Offsets.
