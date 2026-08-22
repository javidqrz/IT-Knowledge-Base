# KB00003 – Windows-Tastatur reagiert nach VMware-Deinstallation nicht

Weitere Zeilen anzeigen

## Betroffene Systeme

- Windows 11 Pro / Windows 11 Enterprise

- VMware Workstation

## Kategorie

Windows Client / Troubleshooting / VMware

## Zielgruppe

- IT Support Techniker

- Systemadministratoren

# Problembeschreibung

Nach der Deinstallation von VMware Workstation und einem anschließenden Neustart funktionierte die integrierte Tastatur des Laptops nicht mehr.

Eine Kennworteingabe am Anmeldebildschirm war nicht möglich.

Auch externe USB-Tastaturen konnten durch die Treiberproblematik beeinträchtigt werden. 【1-ff3f06】

## Fehlersymptome

- Tastatur reagiert nicht

- Anmeldung am System nicht möglich

- Keine Kennworteingabe möglich

- Eingabegeräte funktionieren nicht korrekt

# Ursache des Problems

VMware installiert während der Einrichtung einen eigenen Tastatur-Filtertreiber.

Nach der Deinstallation wurde die Treiberdatei entfernt, der Registry-Eintrag blieb jedoch bestehen.

Beim Systemstart versucht Windows weiterhin den nicht mehr vorhandenen VMware-Treiber zu laden.

Dadurch wird der Eingabestapel der Tastatur blockiert. 【1-ff3f06】


## Temporären Zugriff ermöglichen

Da die integrierte Tastatur nach dem Neustart nicht mehr funktionierte, war eine normale Kennworteingabe nicht möglich.

Um sich trotzdem am System anzumelden, wurde die Windows-Bildschirmtastatur (OSK) verwendet.

Vorgehensweise:

- Am Anmeldebildschirm auf „Barrierefreiheit“ klicken
  
- Bildschirmtastatur (OSK) aktivieren

- Kennwort über die Bildschirmtastatur eingeben

- Anmeldung durchführen

Dadurch konnte auf das System zugegriffen und die weitere Fehleranalyse durchgeführt werden.

## Betroffener Registry-Pfad

```text

HKEY_LOCAL_MACHINE

└─ SYSTEM
└─ CurrentControlSet
└─ Control
└─ Class
└─ {4d36e96b-e325-11ce-bfc1-08002be10318}

```

# Voraussetzungen für die Lösung

Benötigt werden:

- Zugriff auf Windows

- Administratorrechte

- Bildschirmtastatur (OSK) als alternative Eingabemöglichkeit

# Lösung

## Temporären Zugriff ermöglichen

Falls keine Anmeldung möglich ist:

- Bildschirmtastatur (OSK) verwenden

- Über Barrierefreiheit am Anmeldebildschirm aktivieren

## Registrierungseditor öffnen

Öffnen:

```text

Win + R

regedit

```

## UpperFilters prüfen

Zum folgenden Schlüssel navigieren:

```text

HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\{4d36e96b-e325-11ce-bfc1-08002be10318}

```

Den Wert:

```text

UpperFilters

```

öffnen.

---

## VMware-Eintrag entfernen

Folgenden Eintrag löschen:

```text

vmkbd3

```
## Gültige Einträge beibehalten

Es dürfen nur die benötigten Standardwerte verbleiben:

```text

SynTP

kbdclass

```

Hinweis:

- SynTP = Synaptics Touchpad Treiber

- kbdclass = Standard Windows Tastaturtreiber

## REG_MULTI_SZ Fehler beheben

Falls folgende Meldung erscheint:

```text

Daten des Typs REG_MULTI_SZ dürfen keine leeren Zeichenfolgen enthalten

```

müssen alle Leerzeilen am Ende des Feldes entfernt werden.

Anschließend kann der Wert gespeichert werden.

## Computer neu starten

Nach der Anpassung der Registry:

- Änderungen speichern

- Windows neu starten

# Kontrolle nach der Lösung

Nach dem Neustart prüfen:

- Tastatur funktioniert wieder

- Anmeldung ist möglich

- Touchpad funktioniert

- Keine Fehler beim Laden des Tastaturtreibers

# Was habe ich gelernt?

- VMware verwendet eigene Filtertreiber für Eingabegeräte.

- Nicht entfernte Registry-Einträge können Treiberprobleme verursachen.

- Der Registry-Wert UpperFilters beeinflusst den Windows-Treiberstapel.

- Die Bildschirmtastatur kann bei Eingabeproblemen als Notlösung verwendet werden.

- Bei Treiberfehlern sollte die Ursache analysiert werden und nicht nur das Symptom.

## Autor

Ahmad Javid Qarizadah

Auszubildender Fachinformatiker für Systemintegration

## Projekt

Persönliche IT Knowledge Base zur Dokumentation von Windows-, Active-Directory-, Virtualisierungs- und Troubleshooting-Themen während der Ausbildung.
