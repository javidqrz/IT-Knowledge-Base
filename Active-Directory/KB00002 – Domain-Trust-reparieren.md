# KB00002 – Beschädigte Domänenvertrauensstellung nach doppeltem Computernamen reparieren

## Betroffene Systeme

- Windows 10/11 Enterprise

- Active Directory Domain Services (AD DS)

## Kategorie

Infrastructure / Client Management / Active Directory

## Zielgruppe

- Systemadministratoren

- IT Support Techniker

# 1. Problembeschreibung

Bei administrativen Aufgaben auf einem Client wurde eine UAC-Abfrage angezeigt.

Die Anmeldung mit einem Domänenkonto war nicht mehr möglich, da die Vertrauensstellung zwischen dem Computer und Active Directory beschädigt war.

## Fehlermeldung

> Die Sicherheitsdatenbank auf dem Server enthält kein Computerkonto für diese Arbeitsstationsvertrauensstellung.

# 2. Ursache des Problems

Das Problem wurde durch einen doppelten Computernamen verursacht.

## Mögliche Ursachen

- Zwei Computer wurden mit demselben Namen in die Domäne aufgenommen.

- Das Computerkonto im Active Directory wurde durch das zweite Gerät überschrieben.


- Die sichere Verbindung zwischen Computer und Active Directory war dadurch nicht mehr gültig.

# 3. Voraussetzungen für die Lösung

Benötigt werden:

- Zugriff auf ein lokales Administrator-Konto

- Zugangsdaten eines Domänen-Administrators

- Netzwerkverbindung zum Domain Controller nach der Umbenennung

# 4. Lösung Schritt für Schritt

## Schritt 1: Lokale Anmeldung verwenden

### Netzwerkverbindung trennen

- LAN-Kabel entfernen

- WLAN deaktivieren

**Ziel:** Die Anmeldung erfolgt mit dem lokalen Benutzerkonto und nicht über die Domäne.

### Lokales Konto verwenden

Bei der Anmeldung:

```text

Weitere Optionen → Anderes Konto verwenden
```

Lokales Administratorkonto:

```text

.\LokalerAdministrator

```
## Schritt 2: Computer aus der Domäne entfernen

Öffnen:

```text

Win + R

sysdm.cpl

```
Danach:

1. Auf „Ändern“ klicken

2. Mitgliedschaft ändern

3. Von „Domäne“ auf „Arbeitsgruppe“ wechseln

4. Computer neu starten

## Schritt 3: Computer umbenennen

Nach dem Neustart:

```text

sysdm.cpl

```
1. Bereich „Computername“ öffnen

2. Einen neuen eindeutigen Computernamen vergeben

3. Computer neu starten

## Schritt 4: Computer erneut zur Domäne hinzufügen

1. Netzwerk wieder verbinden

2. Erneut öffnen:

```text

sysdm.cpl

```
3. Auf „Ändern“ klicken

4. Domäne auswählen

5. Computer wieder zur Domäne hinzufügen

6. Domänenadministrator-Anmeldedaten eingeben

7. Computer neu starten

Nach dem Neustart wird die Vertrauensstellung neu aufgebaut.

# 5. Kontrolle nach der Lösung

Nach der Reparatur prüfen:

- Anmeldung mit einem Domänenkonto funktioniert wieder

- `gpupdate /force` läuft ohne Fehlermeldung

- UAC akzeptiert wieder Domänen-Anmeldedaten

- Zugriff auf Netzwerkfreigaben funktioniert

# 6. Was habe ich gelernt?

- Jeder Computer in einer Domäne benötigt einen eindeutigen Namen.

- Active Directory verwendet Computerkonten für die Kommunikation mit Clients.

- Bei Problemen mit der Vertrauensstellung muss zuerst die Ursache gefunden werden.

- Nach einem Namenskonflikt ist ein erneuter Domänenbeitritt notwendig.

## Autor

Ahmad Javid Qarizadah

Auszubildender Fachinformatiker für Systemintegration

## Projekt

Persönliche IT Knowledge Base zur Dokumentation von Active-Directory-, Windows-Server- und Troubleshooting-Themen während der Ausbildung.
