KB00001 – Gesperrtes Domain-Benutzerkonto in Active Directory entsperren
Betroffene Systeme
•	Windows Server / Active Directory Domain Services (AD DS)
•	Windows 10/11 Clients
Kategorie:
Identity Management / Active Directory / Troubleshooting
Zielgruppe:
IT Support, Systemadministratoren
________________________________________
1. Problembeschreibung
Bei einer Anmeldung oder bei administrativen Aufgaben konnte ein Domain-Benutzerkonto nicht verwendet werden.
Das Konto wurde nach mehreren falschen Passworteingaben automatisch gesperrt.
System-Fehlermeldung:
„Das angesprochene Konto ist momentan gesperrt und kann möglicherweise nicht für den Anmeldevorgang verwendet werden.“
________________________________________
2. Ursache des Problems
Das Benutzerkonto wurde durch die Sicherheitsrichtlinien von Active Directory gesperrt.
Mögliche Ursachen:
•	Mehrere falsche Eingaben des Passworts.
•	Ein gespeichertes altes Passwort auf einem Gerät.
•	Ein Dienst oder eine geplante Aufgabe verwendet noch ein altes Passwort.
________________________________________
3. Sofortmaßnahmen
Option 1: Anderes Administrator-Konto verwenden
Wenn ein anderes Administrator-Konto verfügbar ist:
1.	Öffnen Sie die Anmeldemaske.
2.	Entfernen Sie das gesperrte Benutzerkonto.
3.	Melden Sie sich mit einem anderen Administrator-Konto an.
________________________________________
Option 2: Lokales Administratorkonto verwenden
Falls keine Anmeldung mit dem Domain-Konto möglich ist:
1.	Melden Sie sich mit einem lokalen Administrator-Konto an.
Beispiel:
.\Administrator
Der Ausdruck .\ bedeutet, dass Windows das lokale Konto des Computers verwendet.
________________________________________
Option 3: Automatische Entsperrung abwarten
Wenn in der Active Directory Gruppenrichtlinie eine Sperrdauer eingestellt ist, wird das Konto nach Ablauf dieser Zeit automatisch entsperrt.
Die genaue Dauer hängt von der konfigurierten Account Lockout Policy ab.
________________________________________
4. Active Directory Konto entsperren
Wenn das Konto weiterhin gesperrt ist:
1.	Öffnen Sie Active Directory-Benutzer und -Computer.
Tastenkombination:
Win + R → dsa.msc
2.	Suchen Sie das betroffene Benutzerkonto.
Beispiel:
<DOMAIN>\<username-adm>
3.	Öffnen Sie die Eigenschaften des Benutzers.
4.	Wechseln Sie zum Tab Konto.
5.	Aktivieren Sie:
☑ Konto entsperren
6.	Klicken Sie auf Übernehmen und danach auf OK.
________________________________________
5. Kontrolle nach der Lösung
Nach der Entsperrung prüfen:
☑ Anmeldung mit dem Benutzerkonto funktioniert wieder.
☑ UAC-Abfragen akzeptieren die Administrator-Anmeldedaten wieder.
☑ Keine erneute Sperrung des Kontos tritt auf.
☑ Die Ereignisanzeige auf dem Domain Controller zeigt keine neuen Lockout-Ereignisse.
Wichtige Event-ID:
4740 - A user account was locked out
Diese Event-ID hilft dabei, den Computer zu finden, der die Sperrung verursacht hat.
________________________________________
6. Was habe ich gelernt?
•	Active Directory verwaltet Benutzerkonten und Berechtigungen.
•	Benutzerkonten können durch falsche Passworteingaben automatisch gesperrt werden.
•	Event ID 4740 hilft bei der Fehlersuche.
•	Bei wiederholten Sperrungen muss die Ursache gefunden werden und nicht nur das Konto entsperrt werden.
________________________________________
Dokumentation für GitHub / IT Knowledge Base
Erstellt während der Ausbildung zum Fachinformatiker Systemintegration.
