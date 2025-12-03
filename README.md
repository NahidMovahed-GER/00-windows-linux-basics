# Windows & Linux Basics

Dieses Projekt zeigt grundlegende Aufgaben, die im IT-Betrieb täglich vorkommen:
Benutzer verwalten, Rechte setzen, Dienste prüfen und Logs auslesen.
Alle Beispiele funktionieren auf Windows und Linux und bilden eine praktische Basis für Support und Systemintegration.

## Inhalte des Projekts

* Windows: Benutzer, Ordner, Rechte, Dienste, Event Viewer
* Linux: Dateien anlegen, Rechte ändern, Rechte verstehen, Benutzer anlegen, Dienste und Logs prüfen

# Windows
### Benutzer anlegen
```
net user testuser MeinPasswort123! /add
```

### Benutzer der Gruppe „Administratoren“ hinzufügen
```
net localgroup administrators testuser /add
```

### Ordner erstellen
```
mkdir C:\TestOrdner
```

### NTFS-Rechte anzeigen
```
icacls C:\TestOrdner
```

### NTFS-Rechte vergeben
```
icacls C:\TestOrdner /grant testuser:(R)
```
*(R = Read / Lesen)*

### Dienste prüfen

Beispiel: Druckwarteschlange
```
Get-Service spooler
```

Starten/Stoppen:
```
Start-Service spooler
Stop-Service spooler
```
### Windows Logs anzeigen (Event Viewer)

**1.** Start → „Event Viewer“

**2.** Windows Logs → *Application / System*

**3.** Fehler/Meldungen lesen

Damit erkennt man typische Probleme (z. B. Dienstfehler, Anmeldefehler).

# Linux
### System aktualisieren (wichtig!)

Docker-Ubuntu ist minimal – also müssen Tools erst installiert werden.
```
apt update
apt install adduser nano iputils-ping
```

### Datei anlegen
```
touch test.txt
```

### Datei anzeigen
```
ls -l test.txt
```

### Rechte ändern
```
chmod 600 test.txt
```
### Bedeutung von 600

* Besitzer: **6** (4 + 2 = lesen + schreiben)
* Gruppe: **0**
* Andere: **0**

### Rechte-Berechnung

| Buchstabe | Bedeutung | Zahl |
| :--- | :--- | :--- |
| r | lesen | 4 |
| w | schreiben | 2 |
| x | ausführen | 1 |

Beispiele:
```
chmod 644 datei.txt   # Besitzer: rw-, Gruppe: r--, Andere: r--
chmod 700 script.sh   # Besitzer: rwx, Gruppe: ---, Andere: ---
```
### Benutzer anlegen
```
adduser demo
```
Beim Anlegen fragt Linux optional nach Name, Telefon usw.
Diese Felder gehören zum GECOS-Feld – alles optional.
Man kann einfach mit ENTER bestätigen.

### Benutzergruppen prüfen
```
id demo
```

### Dienste prüfen (z. B. SSH)
*(Achtung: Im Docker-Container funktioniert systemctl nicht, weil kein systemd vorhanden ist.)*
```
systemctl status ssh
```

### Starten/Stoppen:
```
systemctl start ssh
systemctl stop ssh
```

### Logs anzeigen
```
journalctl -xe
```

Damit sieht man Fehler beim Starten von Diensten oder Systemprobleme.

### Fazit

Dieses Projekt zeigt grundlegende Fähigkeiten, die in Systemintegration, Support und IT-Betrieb täglich gebraucht werden:

* Benutzer anlegen und verwalten
* Rechte verstehen und setzen
* Dienste prüfen
* Logs lesen
* Grundbefehle unter Windows und Linux sicher anwenden

Es bildet die Grundlage für Netzwerk-, Cloud- und Container-Themen.
