Markdown

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
85
 
86
```text
87
Win + R
88
dsa.msc
89
```
90
 
91
## Schritt 2
92
 
93
Das betroffene Benutzerkonto suchen.
94
 
95
Beispiel:
96
 
97
```text
98
<DOMAIN>\<username-adm>
99
```
100
 
101
## Schritt 3
102
 
103
Eigenschaften des Benutzers öffnen.
104
 
105
## Schritt 4
106
 
107
Zum Reiter **Konto** wechseln.
108
 
109
## Schritt 5
110
 
111
Option aktivieren:
112
 
113
```text
114
☑ Konto entsperren
115
```
116
 
117
## Schritt 6
118
 
119
Auf **Übernehmen** und anschließend auf **OK** klicken.
120
 
121
---
122
 
123
# 5. Kontrolle nach der Lösung
124
 
125
Nach der Entsperrung prüfen:
126
 
127
- Anmeldung mit dem Benutzerkonto funktioniert wieder
128
- UAC-Abfragen akzeptieren die Administrator-Anmeldedaten wieder
129
- Keine erneute Sperrung des Kontos tritt auf
130
- Keine neuen Lockout-Ereignisse im Event Viewer
131
 
132
## Wichtige Event-ID
133
 
134
```text
135
4740 - A user account was locked out
136
```
137
 
138
Diese Event-ID hilft dabei, den Computer zu identifizieren, der die Kontosperrung verursacht hat.
139
 
140
---
141
 
142
# 6. Was habe ich gelernt?
143
 
144
- Active Directory verwaltet Benutzerkonten und Berechtigungen.
145
- Benutzerkonten können durch Sicherheitsrichtlinien automatisch gesperrt werden.
146
- Event ID 4740 unterstützt bei der Fehlersuche.
147
- Bei wiederholten Kontosperrungen sollte die Ursache analysiert und behoben werden.
148
- Die reine Entsperrung des Kontos löst das eigentliche Problem nicht dauerhaft.
149
 
150
---
151
 
152
## Autor
153
 
154
Ahmad Javid Qarizadah
155
 
156
Auszubildender Fachinformatiker für Systemintegration
157
 
158
## Projekt
159
 
160
Persönliche IT Knowledge Base während der Ausbildung und des Aufbaus eines Active-Directory-Labs.
