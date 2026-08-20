# KB00004 – Ping zwischen Client und Server nicht möglich

## Betroffene Systeme

- Windows Server

- Windows 10

- Windows 11

## Kategorie

Networking / Windows Firewall / Troubleshooting

## Zielgruppe

- IT Support Techniker

- Systemadministratoren

# Problembeschreibung

Ein Windows Client konnte einen Windows Server nicht per Ping erreichen.

Der Netzwerkadapter war korrekt konfiguriert und die Geräte befanden sich im selben Netzwerk.

## Fehlermeldung

```text

Zeitüberschreitung der Anforderung.

```

oder

```text

Request timed out.

```
# Ursache des Problems

ICMP-Anfragen wurden durch die Windows Firewall blockiert.

Dadurch konnte der Server nicht auf Ping-Anfragen antworten.

# Voraussetzungen für die Lösung

Benötigt werden:

- Lokale Administratorrechte

- Zugriff auf die Windows Firewall

# Lösung

## Windows Firewall öffnen

Öffnen:

```text

Win + R

```
Danach eingeben:

```text

firewall.cpl

```
## Erweiterte Einstellungen öffnen

In der Windows Defender Firewall:

```text

Erweiterte Einstellungen

```
auswählen.

## Eingehende Regeln überprüfen

Folgenden Bereich öffnen:

```text

Eingehende Regeln

```

## ICMP-Regeln suchen

Nach folgenden Regeln suchen:

```text

Netzwerkdiagnose (ICMP)

```
## Regeln aktivieren

Alle benötigten ICMP-Regeln aktivieren.

Danach werden ICMP-Anfragen durch die Firewall zugelassen.

## Verbindung testen

Auf dem Client erneut ausführen:

```cmd
ping <Servername>

```

oder

```cmd

ping <IP-Adresse>

```

# Kontrolle nach der Lösung

Nach der Aktivierung der Regeln prüfen:

- Ping funktioniert erfolgreich

- Antworten vom Server werden empfangen

- Keine Zeitüberschreitung mehr vorhanden

Beispiel:

```text

Antwort von 192.168.x.x

```
# Was habe ich gelernt?

- Ping verwendet das ICMP-Protokoll.

- Die Windows Firewall kann ICMP-Anfragen blockieren.

- Netzwerkprobleme werden nicht immer durch DNS verursacht.

- Bei der Fehlersuche sollte die Firewall immer überprüft werden.

- ICMP-Regeln können über die erweiterten Firewall-Einstellungen aktiviert werden.

## Autor

Ahmad Javid Qarizadah

Auszubildender Fachinformatiker für Systemintegration

## Projekt

Persönliche IT Knowledge Base zur Dokumentation von Windows-, Netzwerk- und Troubleshooting-Themen während der Ausbildung.
