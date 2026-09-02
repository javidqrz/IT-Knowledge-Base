# KB00005 – Raspberry Pi OS installieren und XRDP für den Remotezugriff konfigurieren

## Betroffene Systeme

- Raspberry Pi
- Raspberry Pi OS
- XRDP
- Windows 10/11
- Microsoft Remotedesktopverbindung

## Kategorie

Linux / Raspberry Pi / Installation / Remote Access

## Zielgruppe

- IT Support
- Systemadministratoren
- Fachinformatiker für Systemintegration

---

# 1. Problembeschreibung

Ein Raspberry Pi sollte für die spätere Nutzung im Netzwerk vorbereitet werden.

Dafür musste Raspberry Pi OS installiert, das System aktualisiert, Benutzer verwaltet und der Remotezugriff per XRDP eingerichtet werden.

Während der Einrichtung trat zusätzlich der XRDP-Fehler

```text
login failed for display 0
```

auf, wodurch eine Remote-Anmeldung zunächst nicht möglich war.

---

# 2. Ursache des Problems

Für den Remotezugriff musste XRDP installiert und korrekt konfiguriert werden.

Zusätzlich konnte eine fehlerhafte XRDP-Sitzung oder eine beschädigte Datei `.Xauthority` verhindern, dass eine grafische Sitzung aufgebaut wird.

## Mögliche Ursachen

- XRDP ist nicht installiert
- xorgxrdp fehlt
- XRDP-Dienste laufen nicht korrekt
- Fehlerhafte Datei `.Xauthority`
- Fehlende oder fehlerhafte `.xsession`
- Beschädigte XRDP-Sitzung
- Falsches Kennwort des lokalen Benutzers

---

# 3. Voraussetzungen für die Lösung

Benötigt werden:

- Raspberry Pi
- microSD-Karte
- Netzteil
- LAN-Kabel
- Monitor
- HDMI-Kabel
- USB-Tastatur
- USB-Maus
- Windows-PC
- Raspberry Pi Imager

---

# 4. Lösung

## Schritt 1: Raspberry Pi OS installieren

microSD-Karte in den Kartenleser einsetzen.

Raspberry Pi Imager starten.

Folgende Punkte auswählen:

- Raspberry-Pi-Modell
- Raspberry Pi OS
- microSD-Karte als Zielmedium

Hostname, Benutzername, Kennwort, Zeitzone und Tastaturlayout konfigurieren.

Den Schreibvorgang starten und vollständig abschließen lassen.

## Übersicht der Installation

> Hier den Screenshot der Installation einfügen.

```markdown
../Screenshots/Raspberry_Pi_Installation.png
```

---

## Schritt 2: Raspberry Pi starten

- microSD-Karte einsetzen
- Monitor verbinden
- Tastatur und Maus verbinden
- Netzwerk verbinden
- Netzteil anschließen

Das System starten und die erste Anmeldung durchführen.

---

## Schritt 3: Systeminformationen prüfen

### Modell anzeigen

```bash
tr -d '\0' < /proc/device-tree/model; echo
```

### Hostname anzeigen

```bash
hostname
```

### IP-Adresse anzeigen

```bash
hostname -I
```

---

## Schritt 4: System aktualisieren

Paketlisten aktualisieren:

```bash
sudo apt update
```

Pakete aktualisieren:

```bash
sudo apt upgrade -y
```

System neu starten:

```bash
sudo reboot
```

---

## Schritt 5: Benutzer verwalten

Benutzer erstellen:

```bash
sudo adduser <benutzername>
```

Benutzer zur sudo-Gruppe hinzufügen:

```bash
sudo usermod -aG sudo <benutzername>
```

Kennwort ändern:

```bash
sudo passwd <benutzername>
```

Benutzer wechseln:

```bash
su - <benutzername>
```

---

## Schritt 6: Auto Login konfigurieren

```bash
sudo raspi-config
```

Menüpfad:

```text
System Options
→ Boot / Auto Login
→ Desktop Autologin
```

Anschließend:

```bash
sudo reboot
```

---

## Schritt 7: XRDP installieren

```bash
sudo apt install xrdp -y
```

Zusätzliche Komponente:

```bash
sudo apt install xorgxrdp -y
```

---

## Schritt 8: XRDP-Dienste prüfen

```bash
sudo systemctl status xrdp
```

```bash
sudo systemctl status xrdp-sesman
```

Beide Dienste sollten anzeigen:

```text
active (running)
```

---

## Schritt 9: Remote Desktop testen

Windows öffnen:

```text
Win + R
```

```text
mstsc
```

IP-Adresse des Raspberry Pi eingeben.

Mit Benutzername und Kennwort anmelden.

Prüfen, ob die grafische Oberfläche angezeigt wird.

---

## Schritt 10: Fehler „login failed for display 0“ beheben

Dienste und Logs prüfen:

```bash
sudo systemctl status xrdp
sudo systemctl status xrdp-sesman

sudo tail -50 /var/log/xrdp.log
sudo tail -50 /var/log/xrdp-sesman.log
```

Datei sichern:

```bash
mv ~/.Xauthority ~/.Xauthority.old
```

XRDP neu starten:

```bash
sudo systemctl restart xrdp
```

System neu starten:

```bash
sudo reboot
```

Remote-Anmeldung erneut testen.

---

# 5. Kontrolle nach der Lösung

Prüfen:

- Raspberry Pi startet
- Netzwerk funktioniert
- Hostname vorhanden
- IP-Adresse vorhanden
- Benutzerkonto funktioniert
- XRDP läuft
- Remote Desktop funktioniert
- Anmeldung nach Neustart möglich

---

# 6. Ergebnis

- Raspberry Pi OS erfolgreich installiert
- System aktualisiert
- Benutzerkonto eingerichtet
- XRDP installiert
- Remote Desktop erfolgreich getestet
- Fehler „login failed for display 0“ analysiert und behoben

---

# 7. Was habe ich gelernt?

- Raspberry Pi OS installieren
- Raspberry Pi Imager verwenden
- Linux-Systeme aktualisieren
- Benutzerkonten verwalten
- XRDP installieren
- Remote Desktop auf Linux-Systemen einrichten
- XRDP-Dienste analysieren
- Logdateien auswerten
- Fehler „login failed for display 0“ beheben

---

## Autor

Ahmad Javid Qarizadah

Bachelor of Computer Science

Auszubildender Fachinformatiker für Systemintegration

---

## Projekt

Persönliche IT Knowledge Base zur Dokumentation von Raspberry Pi, Linux, XRDP und Troubleshooting während der Ausbildung.
