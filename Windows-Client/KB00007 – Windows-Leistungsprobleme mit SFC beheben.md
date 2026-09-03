# KB00009 - Windows-Systemdateien mit SFC reparieren

## Betroffene Systeme

- Windows 10
- Windows 11

## Kategorie

Windows / System Repair / Troubleshooting

## Zielgruppe

- IT Support
- Systemadministratoren
- Fachinformatiker für Systemintegration

---

# 1. Problembeschreibung

Das Windows-System reagierte ungewöhnlich langsam und zeigte zeitweise ein instabiles Verhalten.

Folgende Symptome wurden festgestellt:

- Anwendungen und Windows-Systemfenster wurden nur verzögert geöffnet.
- Der Datei-Explorer reagierte zeitweise langsam.
- Das Mikrofon funktionierte nicht zuverlässig.
- Das Headset wurde zeitweise nicht korrekt erkannt.
- Ein Neustart führte nicht zu einer dauerhaften Verbesserung.

---

# 2. Ursache des Problems

Die genaue Ursache konnte nicht eindeutig festgestellt werden.

Probleme mit Mikrofonen, Headsets und anderen Audiogeräten können beispielsweise durch folgende Komponenten verursacht werden:

- Gerätetreiber
- Windows Audio Services
- Windows-Updates
- Geräte- oder Hardwarefehler
- Datenschutzeinstellungen und Berechtigungen
- beschädigte oder fehlende Windows-Systemdateien

Aufgrund der allgemeinen Systeminstabilität wurde zunächst eine Beschädigung geschützter Windows-Systemdateien als mögliche Ursache untersucht.

> **Hinweis:** Die spätere Verbesserung nach der Ausführung von SFC deutet darauf hin, dass beschädigte Systemdateien beteiligt gewesen sein könnten. Sie beweist jedoch nicht, dass sämtliche Symptome ausschließlich dadurch verursacht wurden.

---

# 3. Voraussetzungen

Benötigt werden:

- Lokale Administratorrechte
- Zugriff auf Windows Terminal, PowerShell oder Eingabeaufforderung
- Ausreichend Zeit für die vollständige Systemprüfung
- Bei Verwendung von DISM eine funktionierende Netzwerkverbindung oder eine geeignete alternative Reparaturquelle

Vor Beginn sollten geöffnete Dokumente und wichtige Arbeiten gespeichert werden.

---

# 4. Unterschied zwischen SFC und DISM

## System File Checker

Der System File Checker überprüft geschützte Windows-Systemdateien.

Befehl:

```cmd
sfc /scannow
```

Wenn beschädigte oder fehlende geschützte Systemdateien erkannt werden, versucht SFC, diese durch funktionsfähige Kopien aus dem Windows-Komponentenspeicher zu ersetzen.

## Deployment Image Servicing and Management

DISM überprüft und repariert den Windows-Komponentenspeicher, den SFC als Reparaturquelle verwenden kann.

Befehl:

```cmd
DISM /Online /Cleanup-Image /RestoreHealth
```

## Wann SFC verwenden?

SFC eignet sich als erste Maßnahme, wenn vermutet wird, dass geschützte Windows-Systemdateien beschädigt oder nicht mehr vollständig vorhanden sind.

Typische Beispiele:

- Windows-Komponenten reagieren ungewöhnlich.
- Systemfenster oder integrierte Anwendungen funktionieren nicht korrekt.
- Nach einem Update oder Treiberproblem treten Systemfehler auf.
- Windows zeigt ein allgemein instabiles Verhalten.

## Wann DISM verwenden?

DISM sollte verwendet werden, wenn:

- SFC beschädigte Dateien nicht reparieren konnte.
- SFC wiederholt Fehler meldet.
- der Windows-Komponentenspeicher möglicherweise beschädigt ist.
- ein professioneller vollständiger Reparaturdurchlauf durchgeführt werden soll.

Ein häufig verwend
