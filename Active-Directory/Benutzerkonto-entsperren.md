# KB00001 – Gesperrtes Domain-Benutzerkonto in Active Directory entsperren

## Betroffene Systeme

- Windows Server

- Active Directory Domain Services (AD DS)

- Windows 10/11 Clients

 
## Kategorie

 

Identity Management / Active Directory / Troubleshooting

## Zielgruppe

- IT Support

- Systemadministratoren

# 1. Problembeschreibung

Bei einer Anmeldung oder bei administrativen Aufgaben konnte ein Domain-Benutzerkonto nicht verwendet werden.

Das Konto wurde nach mehreren falschen Passworteingaben automatisch gesperrt.

## Fehlermeldung

> Das angesprochene Konto ist momentan gesperrt und kann möglicherweise nicht für den Anmeldevorgang verwendet werden.

# 2. Ursache des Problems

Das Benutzerkonto wurde durch die Sicherheitsrichtlinien von Active Directory gesperrt.

## Mögliche Ursachen

- Mehrere falsche Eingaben des Passworts

- Ein gespeichertes altes Passwort auf einem Gerät
  
- Ein Dienst oder eine geplante Aufgabe verwendet weiterhin ein altes Passwort

# 3. Sofortmaßnahmen

## Option 1: Anderes Administrator-Konto verwenden

Wenn ein anderes Administrator-Konto verfügbar ist:

1. Anmeldemaske öffnen

2. Gesperrtes Benutzerkonto entfernen

3. Mit einem anderen Administrator-Konto anmelden


## Option 2: Lokales Administratorkonto verwenden

Falls keine Anmeldung mit dem Domain-Konto möglich ist:

1. Mit einem lokalen Administratorkonto anmelden

Beispiel:

```text

.\Administrator

Der Ausdruck `.\` bedeutet, dass Windows das lokale Benutzerkonto des Computers verwendet.

## Option 3: Automatische Entsperrung abwarten

Wenn eine Kontosperrdauer (Account Lockout Policy) konfiguriert wurde, wird das Benutzerkonto nach Ablauf der festgelegten Zeit automatisch entsperrt.

# 4. Active Directory Konto entsperren

Wenn das Konto weiterhin gesperrt ist:

## Schritt 1

Active Directory-Benutzer und -Computer öffnen:

```text

Win + R

dsa.msc


## Schritt 2

Das betroffene Benutzerkonto suchen.

Beispiel:

```text

<DOMAIN>\<username-adm>

## Schritt 3

Eigenschaften des Benutzers öffnen.

## Schritt 4

Zum Reiter **Konto** wechseln.

## Schritt 5

Option aktivieren:

```text

☑ Konto entsperren

## Schritt 6

Auf **Übernehmen** und anschließend auf **OK** klicken.

# 5. Kontrolle nach der Lösung

Nach der Entsperrung prüfen:

- Anmeldung mit dem Benutzerkonto funktioniert wieder

- UAC-Abfragen akzeptieren die Administrator-Anmeldedaten wieder

- Keine erneute Sperrung des Kontos tritt auf

- Keine neuen Lockout-Ereignisse im Event Viewer

## Wichtige Event-ID

```text

4740 - A user account was locked out

Diese Event-ID hilft dabei, den Computer zu identifizieren, der die Kontosperrung verursacht hat.

# 6. Was habe ich gelernt?

- Active Directory verwaltet Benutzerkonten und Berechtigungen.

- Benutzerkonten können durch Sicherheitsrichtlinien automatisch gesperrt werden.

- Event ID 4740 unterstützt bei der Fehlersuche.

- Bei wiederholten Kontosperrungen sollte die Ursache analysiert und behoben werden.

- Die reine Entsperrung des Kontos löst das eigentliche Problem nicht dauerhaft.

## Autor

Ahmad Javid Qarizadah

Auszubildender Fachinformatiker für Systemintegration

## Projekt

Persönliche IT Knowledge Base während der Ausbildung und des Aufbaus eines Active-Directory-Labs.
