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

Die genaue Ursache konnte nicht eindeutig festgestellt werden. Aufgrund der beobachteten Systeminstabilität wurde eine mögliche Beschädigung geschützter Windows-Systemdateien als Fehlerursache untersucht.

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

Ein häufig verwendeter vollständiger Reparaturablauf ist:

```cmd
DISM /Online /Cleanup-Image /RestoreHealth
sfc /scannow
```

Im dokumentierten Fall wurde zunächst `sfc /scannow` ausgeführt. Da sich das Systemverhalten danach verbesserte, war keine weitere Reparatur mit DISM erforderlich.

---

# 5. Systemdateien mit SFC prüfen

## Eingabeaufforderung als Administrator öffnen

Windows-Suche öffnen und Folgendes eingeben:

```text
cmd
```

Bei **Eingabeaufforderung** die Option auswählen:

```text
Als Administrator ausführen
```

Die Abfrage der Benutzerkontensteuerung bestätigen.

Alternativ kann Windows Terminal oder PowerShell als Administrator verwendet werden.

## Systemprüfung starten

Folgenden Befehl ausführen:

```cmd
sfc /scannow
```

Die Überprüfung nicht unterbrechen und warten, bis der Fortschritt 100 Prozent erreicht hat.

Je nach Systemleistung und Zustand von Windows kann die Prüfung einige Zeit benötigen.

---

# 6. Ergebnisse des SFC-Scans auswerten

Die genaue Ausgabe hängt von der Sprache und Version des Windows-Systems ab.

## Keine Integritätsverletzungen gefunden

Mögliche englische Ausgabe:

```text
Windows Resource Protection did not find any integrity violations.
```

Bedeutung:

- SFC hat keine beschädigten geschützten Windows-Systemdateien gefunden.
- Die Ursache des Problems liegt möglicherweise in Treibern, Diensten, Anwendungen, Benutzerprofilen, Einstellungen oder Hardware.

## Beschädigte Dateien erfolgreich repariert

Mögliche englische Ausgabe:

```text
Windows Resource Protection found corrupt files and successfully repaired them.
```

Bedeutung:

- Beschädigte Windows-Systemdateien wurden gefunden.
- SFC konnte die betroffenen Dateien erfolgreich reparieren.
- Anschließend sollte Windows neu gestartet und ein Funktionstest durchgeführt werden.

## Einige Dateien konnten nicht repariert werden

Mögliche englische Ausgabe:

```text
Windows Resource Protection found corrupt files but was unable to fix some of them.
```

Bedeutung:

- SFC hat beschädigte Dateien gefunden.
- Nicht alle Dateien konnten repariert werden.
- DISM sollte ausgeführt und SFC anschließend wiederholt werden.

## Der Reparaturdienst konnte nicht gestartet werden

Mögliche englische Ausgabe:

```text
Windows Resource Protection could not start the repair service.
```

Mögliche Maßnahmen:

- prüfen, ob die Konsole als Administrator geöffnet wurde
- Windows neu starten und den Scan erneut durchführen
- den Windows Modules Installer prüfen
- DISM verwenden
- den Scan gegebenenfalls im abgesicherten Modus ausführen

## Die angeforderte Operation konnte nicht ausgeführt werden

Mögliche englische Ausgabe:

```text
Windows Resource Protection could not perform the requested operation.
```

Mögliche Maßnahmen:

- Windows neu starten
- Dateisystem und Datenträgerzustand prüfen
- DISM ausführen
- SFC im abgesicherten Modus erneut starten
- Ereignisanzeige und CBS-Protokoll kontrollieren

> **Hinweis:** Für die Fehlerbewertung ist die sichtbare Abschlussmeldung zusammen mit dem CBS-Protokoll normalerweise hilfreicher als ein allgemeiner Prozess-Exitcode.

---

# 7. Windows-Komponentenspeicher mit DISM reparieren

Falls SFC Dateien nicht reparieren konnte, eine administrative Konsole öffnen und zunächst den folgenden Befehl ausführen:

```cmd
DISM /Online /Cleanup-Image /RestoreHealth
```

DISM prüft den Windows-Komponentenspeicher und versucht, erkannte Beschädigungen zu reparieren.

Warten, bis der Vorgang vollständig abgeschlossen ist.

Anschließend SFC erneut ausführen:

```cmd
sfc /scannow
```

Empfohlene Reihenfolge:

```cmd
DISM /Online /Cleanup-Image /RestoreHealth
sfc /scannow
```

Danach Windows neu starten.

---

# 8. SFC-Protokoll überprüfen

Detaillierte Informationen des SFC-Scans werden im CBS-Protokoll gespeichert:

```text
C:\Windows\Logs\CBS\CBS.log
```

Da die Datei umfangreiche Informationen verschiedener Windows-Wartungsvorgänge enthält, können die SFC-relevanten Einträge in eine separate Datei exportiert werden.

Diesen Befehl in einer administrativen Eingabeaufforderung ausführen:

```cmd
findstr /c:"[SR]" %windir%\Logs\CBS\CBS.log > "%userprofile%\Desktop\SFC-Details.txt"
```

Die Datei wird anschließend auf dem Desktop erstellt:

```text
SFC-Details.txt
```

Die Datei kann für die weitere Fehleranalyse verwendet werden.

Zu prüfen sind insbesondere:

- Dateien, die als beschädigt erkannt wurden
- Dateien, die erfolgreich repariert wurden
- Dateien, die nicht repariert werden konnten
- wiederholt auftretende Reparaturfehler

> **Datenschutz:** Vor einer Veröffentlichung von Logauszügen müssen Benutzernamen, Dateipfade, Gerätenamen und andere identifizierende Informationen entfernt oder anonymisiert werden.

---

# 9. System neu starten

Nach einer erfolgreichen Reparatur Windows neu starten.

Über die grafische Oberfläche:

```text
Start
→ Ein/Aus
→ Neu starten
```

Alternativ über die administrative Konsole:

```cmd
shutdown /r /t 0
```

---

# 10. Kontrolle nach der Lösung

Nach dem Neustart wurden die zuvor betroffenen Funktionen erneut getestet.

Folgende Punkte wurden geprüft:

- Windows reagiert wieder normal.
- Anwendungen und Windows-Systemfenster öffnen sich ohne ungewöhnliche Verzögerung.
- Der Datei-Explorer reagiert wieder normal.
- Das Mikrofon funktioniert zuverlässig.
- Das Headset wird korrekt erkannt.
- Die Audiowiedergabe funktioniert.
- Keine neuen ungewöhnlichen Systemfehler treten auf.
- Die SFC-Abschlussmeldung wurde kontrolliert.

Abschließend sollten genau die Anwendungen, Geräte und Windows-Funktionen getestet werden, bei denen zuvor Probleme aufgetreten waren.

---

# 11. Ergebnis

Nach der Ausführung von:

```cmd
sfc /scannow
```

arbeitete Windows wieder stabiler.

Anwendungen und Windows-Systemfenster, darunter der Datei-Explorer, wurden wieder ohne die zuvor beobachteten Verzögerungen geöffnet.

Das Mikrofon und das Headset funktionierten nach der Maßnahme wieder ordnungsgemäß.

Da die Symptome nach der Systemdateiprüfung nicht mehr auftraten, war im konkreten Fall keine zusätzliche Reparatur mit DISM notwendig.

Die genaue ursprüngliche Ursache konnte dennoch nicht abschließend bewiesen werden. Die erfolgreiche SFC-Maßnahme deutet darauf hin, dass beschädigte geschützte Windows-Systemdateien am Fehlerbild beteiligt gewesen sein könnten.

---

# 12. Weiterführende Maßnahmen

Falls SFC und DISM das Problem nicht beheben, sollten weitere Fehlerquellen untersucht werden.

## Bei Audio- und Geräteproblemen

- Geräte-Manager kontrollieren
- Audiotreiber aktualisieren oder neu installieren
- Windows Audio und Windows Audio Endpoint Builder prüfen
- Datenschutzeinstellungen für das Mikrofon kontrollieren
- Headset an einem anderen Anschluss testen
- Gerät an einem anderen Computer testen
- Windows-Problembehandlung ausführen

Dienste können beispielsweise über folgenden Befehl geöffnet werden:

```text
services.msc
```

## Bei Leistungsproblemen

- Task-Manager kontrollieren
- CPU-, RAM- und Datenträgerauslastung prüfen
- Autostart-Programme prüfen
- freien Speicherplatz kontrollieren
- Windows Update prüfen
- Ereignisanzeige kontrollieren
- Datenträgerzustand untersuchen
- Malware-Prüfung durchführen

Task-Manager öffnen:

```text
Ctrl + Shift + Esc
```

Ereignisanzeige öffnen:

```text
eventvwr.msc
```

## Bei weiterhin beschädigten Systemkomponenten

- DISM mit einer geeigneten Reparaturquelle verwenden
- aktuellen Wiederherstellungspunkt prüfen
- In-Place-Reparaturinstallation von Windows erwägen
- vor umfangreichen Maßnahmen ein Backup erstellen

---

# 13. Was habe ich gelernt?

- Die Ursache allgemeiner Windows-Probleme sollte vorsichtig und ohne unbelegte Schlussfolgerungen beschrieben werden.
- Probleme mit Mikrofon und Headset können sowohl durch Systemdateien als auch durch Treiber, Dienste, Berechtigungen oder Hardware verursacht werden.
- `sfc /scannow` überprüft und repariert geschützte Windows-Systemdateien.
- DISM repariert den Windows-Komponentenspeicher, den SFC als Reparaturquelle verwenden kann.
- Wenn SFC nicht alle Dateien reparieren kann, sollte zuerst DISM und anschließend SFC erneut ausgeführt werden.
- Die Abschlussmeldung des SFC-Scans muss ausgewertet werden.
- Das CBS-Protokoll enthält detaillierte Informationen über erkannte und reparierte Dateien.
- Nach jeder Reparatur müssen die ursprünglich betroffenen Funktionen erneut getestet werden.
- Ein erfolgreiches Ergebnis einer Maßnahme ist ein wichtiger Hinweis, aber nicht immer ein vollständiger Beweis für die ursprüngliche Fehlerursache.

---

## Autor

Ahmad Javid Qarizadah

Bachelor of Computer Science

Auszubildender Fachinformatiker für Systemintegration

---

## Projekt

Persönliche IT Knowledge Base zur Dokumentation von Windows-Troubleshooting und praktischen Erfahrungen während der Ausbildung.
