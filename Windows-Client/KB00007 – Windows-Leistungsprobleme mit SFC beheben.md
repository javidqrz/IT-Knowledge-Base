# KB00007 – Windows-Systemdateien mit SFC reparieren

## Betroffene Systeme

- Windows 10
- Windows 11

## Kategorie

Windows / Troubleshooting / System Repair

## Zielgruppe

- IT Support
- Systemadministratoren
- Fachinformatiker für Systemintegration

---

# 1. Problembeschreibung

Das Windows-System reagierte ungewöhnlich langsam.

Zusätzlich traten folgende Probleme auf:

- Anwendungen und Systemfenster wurden teilweise nur verzögert geöffnet.
- Anwendungen reagierten verzögert.
- Das Mikrofon funktionierte zeitweise nicht.
- Headset und Audiogeräte wurden nicht immer korrekt erkannt.

Ein Neustart des Systems führte nicht zu einer dauerhaften Verbesserung.

---

# 2. Ursache des Problems

Die genaue Ursache konnte nicht eindeutig festgestellt werden.

Die Symptome deuteten jedoch auf beschädigte oder fehlende Windows-Systemdateien hin.

Beschädigte Systemdateien können zu Leistungsproblemen, Fehlern bei der Geräteerkennung und einem instabilen Systemverhalten führen.

---

# 3. Lösung

## Schritt 1: Eingabeaufforderung als Administrator öffnen

Windows-Suche öffnen:

```text
cmd
```

Anschließend:

```text
Als Administrator ausführen
```

---

## Schritt 2: Systemdateien prüfen und reparieren

Folgenden Befehl ausführen:

```cmd
sfc /scannow
```

Der System File Checker (SFC) überprüft alle geschützten Windows-Systemdateien und ersetzt beschädigte Dateien automatisch durch eine funktionsfähige Kopie.

---

## Schritt 3: Scan abschließen lassen

Warten bis der Scan:

```text
100 %
```

erreicht hat.

Der Vorgang kann je nach System einige Zeit in Anspruch nehmen.

---

## Schritt 4: Ergebnis prüfen

Mögliche Ergebnisse:

### Keine Integritätsverletzungen gefunden

```text
Der Windows-Ressourcenschutz hat keine Integritätsverletzungen gefunden.
```

### Beschädigte Dateien gefunden und erfolgreich repariert

```text
Der Windows-Ressourcenschutz hat beschädigte Dateien gefunden und erfolgreich repariert.
```

### Beschädigte Dateien konnten nicht repariert werden

```text
Der Windows-Ressourcenschutz hat beschädigte Dateien gefunden, einige davon konnten jedoch nicht repariert werden.
```

In diesem Fall sollte zusätzlich DISM ausgeführt werden.

---

## Optional: DISM verwenden

Falls SFC die Dateien nicht reparieren kann:

```cmd
DISM /Online /Cleanup-Image /RestoreHealth
```

Nach Abschluss erneut ausführen:

```cmd
sfc /scannow
```

---

## Schritt 5: System neu starten

Nach erfolgreicher Reparatur:

```cmd
shutdown /r /t 0
```

oder

```text
Windows normal neu starten
```

---

# 4. Kontrolle nach der Lösung

Prüfen:

- Windows reagiert wieder normal
- Anwendungen starten fehlerfrei
- Webseiten werden korrekt geladen
- Mikrofon funktioniert wieder
- Headset wird korrekt erkannt
- Keine ungewöhnlichen Systemfehler mehr vorhanden

---

# 5. Ergebnis

Nach der Ausführung von:

```cmd
sfc /scannow
```

arbeitete das System wieder stabil.

Die zuvor auftretenden Leistungsprobleme konnten nicht mehr festgestellt werden.

Webseiten und Anwendungen wurden wieder korrekt geladen.

Zusätzlich funktionierten Mikrofon und Headset wieder ordnungsgemäß.

---

# 6. Was habe ich gelernt?

- Windows-Systemdateien können beschädigt werden.
- Beschädigte Systemdateien können Leistungs- und Treiberprobleme verursachen.
- Mit `sfc /scannow` lassen sich Windows-Systemdateien prüfen und reparieren.
- Bei schwerwiegenderen Problemen kann zusätzlich DISM verwendet werden.
- Nach einer Reparatur sollte immer ein Funktionstest durchgeführt werden.

---

## Autor

Ahmad Javid Qarizadah

Auszubildender Fachinformatiker für Systemintegration

---

## Projekt

Persönliche IT Knowledge Base während der Ausbildung zum Fachinformatiker für Systemintegration.
