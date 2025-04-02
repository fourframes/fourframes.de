---
layout: single
title: "Proof-of-Concept: Onsite & Offsite Cross-Platform Backup mit Raspberry Pis"
date:   2025-04-02 
categories: projekt
tags: backup rpi meshnet
excerpt: "Einrichtung eines automatisierten Onsite & Offsite Backup mit Raspberry Pis, NordVPN Meshnet, rsync und restic."
toc: true
toc_sticky: true
header:
  overlay_image: assets/images/posts/offsite-backup/denny-muller-1qL31aacAPA-unsplash.jpg
  overlay_filter: 0.5 # same as adding an opacity of 0.5 to a black background
  caption:  "Foto von [Denny Müller](https://unsplash.com/@redaquamedia?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash) auf [Unsplash](https://unsplash.com/photos/white-and-silver-hard-disk-drive-1qL31aacAPA?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash)"
---

In einem Gespräch kam kürzlich die Frage auf, wie aufwendig die Einrichtung eines automatisierten Offsite-Backups mit vorhandener Hardware ist. Offsite-Backups bieten zusätzlichen Schutz, falls primäre Onsite-Backups durch Ereignisse wie Katastrophen oder Diebstahl unbrauchbar werden. Ich fragte mich, was sich mit einem Raspberry Pi, der vielleicht noch ungenutzt herumliegt, anfangen lässt. Das war der Startpunkt für dieses kleine Projekt.

## Anforderungen und Konzept

Nach einigen Überlegungen habe ich folgende Anforderungen an das Setup definiert:

* Cross-Platform-Backup-Tool
* Speicherung des Backups auf einem Raspberry Pi
* Verschlüsselung der Backups (in Transit und at Rest)
* Setup ohne offene Ports oder Port-Forwarding
* Optional: Kombination von Onsite- und Offsite-Backup
* Optional: Verwendung kostenloser/freier Tools
* Optional: Versionierung ist optional

Die Kombination aus Onsite- und Offsite-Backup bietet mehrere Vorteile: Die Verbindung zu eine Offsite-Standort verfügt meist über eine geringere Bandbreite als das Onsite-Netzwerk. Wenn ein Backup von einer Workstation direkt als Offsite-Backup erstellt wird, dauert dies aufgrund der langsameren Verbindung erheblich länger. Da die Workstation möglicherweise nicht über längere Zeiträume (mehrere Stunden) durchgehend laufen soll, bietet eine Kombination aus Onsite- und Offsite-Backup den Vorteil, dass das Onsite-Backup vergleichsweise schnell erstellt und kopiert wird. Das Offsite-Backup (Kopie vom Onsite-Backup) kann dann vom zu einem späteren Zeitpunkt erfolgen. Dieser Ansatz ermöglicht zudem unterschiedliche Backup-Zyklen für Onsite- und Offsite-Backup (beispielsweise täglich Onsite, wöchentlich Offsite).  Das Offsite-Backup kann dann zu einem Zeitpunkt erfolgen, an dem mehr Bandbreite zur Verfügung steht (z. B. nachts).

Aufgrund der Vielzahl an Vorteilen dieser Kombination aus On- und Offsite-Backup habe ich mich dazu entschlossen einen weiteren Pi zu installieren, der das Ziel des Onsite-Backups ist.

## Das Hardware-Setup

[![Ein Diagram des Hardware Setup mit Onsite-Pi und Workstation in einem LAN und Offsite-Pi in einem anderen LAN.](/assets/images/posts/offsite-backup/Diagram.jpg)](/assets/images/posts/offsite-backup/Diagram.jpg)

Für dieses Proof-of-Concept nehme ich folgendes Hardware-Setup an: Die Workstation (Backup-Quelle) und ein Raspberry Pi (Onsite-Pi) befinden sich im selben Netzwerk (Onsite-LAN). Der Onsite-Pi ist das primäre Ziel des Backups. Dieses Local Area Network (Onsite-LAN) ist an ein Wide Area Network (WAN) angeschlossen, welches mit einem weiteren Local Area Network (Offsite-LAN) verbunden ist. In diesem Offsite-LAN soll sich das Offsite-Backup auf einem Raspberry Pi (Offsite-Pi) befinden. Im Proof-of-Concept habe ich das Internet als WAN genutzt.

## Das Software-Setup

Es galt, die passende Software für folgende Aufgaben zu finden:

* Cross-Platform-Backup
* Spiegeln des Onsite-Backups zum Offsite-Backup
* Verbindung von zwei LANs über ein WAN hinweg

### Onsite-Backup: Auswahl des Backup-Tools

Nach einiger Recherche fiel die Wahl auf restic. Dieses Tool schien die Anforderungen zu erfüllen und bietet zusätzliche Features: versionierte, verschlüsselte Backups, Übertragung via SSH/SFTP und Cross-Platform-Unterstützung.

Nach der Installation von restic auf der Workstation und dem Onsite-Pi (dort nicht zwingend erforderlich) wurde von der Workstation aus ein neues Repository initialisiert:

```text
restic -r sftp:pi@onsite-pi:/restic init
```

Anschließend wurde ein Passwort vergeben, das zur Verschlüsselung der Daten benötigt wird. Wichtig: Dieses Passwort muss sicher aufbewahrt werden, da es keine Möglichkeit gibt, die Daten ohne Passwort zu entschlüsseln.

Das Tool erstellt am gewählten Ort ein Repository mit folgender Verzeichnisstruktur:

```text
pi@onsite-pi:~/restic $ ls
config  data  index  keys  locks  snapshots
```

An dieser Stelle wurde mir klar, dass restic das Backup als Dateistruktur ablegt. Aus diesem Grund ist es nicht zwingend notwendig, dass restic auf dem Onsite-Pi oder auf dem Offsite-Pi installiert wird. Das Backup wird auf der Workstation erstellt und per SFTP übertragen. Wenn man jedoch auf dem Onsite- oder Offsite-Pi prüfen möchte, wann ein Snapshot erstellt wurde, wie groß ein Snapshot ist oder ob das Backup Fehler aufweist, dann muss das Tool auch auf den Pis installiert werden. Allerdings können diese Checks auch remote von der Workstation erfolgen.

### Automatisierung des Onsite-Backups

Um das Onsite-Backup von der Workstation zum Onsite-Pi zu automatisieren, habe ich mich an einem PowerShell-Skript versucht. Dabei stieß ich aber direkt auf ein Problem: Restic fragt bei jeder Interaktion mit dem Backup-Repository nach dem Passwort. Das ist natürlich sinnvoll, aber wie sollte ich das in einem Skript automatisieren? Nach etwas Recherche fand ich das Flag --password-file, mit dem man das Passwort in eine Textdatei auslagern kann. Allerdings war mir sofort bewusst, dass das Ablegen des Passworts im Klartext in einer Datei natürlich ein erhebliches Sicherheitsrisiko darstellt. Für dieses Proof-of-Concept habe ich das erst mal so gelassen, aber für den produktiven Einsatz müsste ich mir da definitiv noch etwas Besseres überlegen.

```text
restic -r sftp://pi@onsite-pi:/restic backup ".\Documents" --password-file ".\pw.txt" --compression auto
restic -r sftp://pi@onsite-pi:/restic forget --keep-last 2 --prune --password-file ".\pw.txt"
```

Im Zuge der Skripterstellung und beim Testen des Backups fiel mir dann auf, dass restic standardmäßig unendlich viele Snapshots anlegt. Das bedeutet, dass jede Änderung an einer Datei potenziell als eigener Snapshot gespeichert wird. Da Versionierung für dieses Projekt aber keine Priorität hatte, suchte ich nach einer Möglichkeit, die Anzahl der Snapshots zu begrenzen. Schließlich fand ich den Befehl, mit dem man festlegen kann, wie viele Snapshots behalten werden sollen. Ich habe das Skript dann so angepasst, dass immer nur die letzten zwei Snapshots aufbewahrt werden, um den Speicherplatz auf dem Pi nicht unnötig zu füllen.

### Interkonnektivität

Nachdem das Onsite-Backup nun funktionierte, stand ich vor der Frage, wie ich die Verbindung zwischen dem Onsite-Pi und dem Offsite-Pi realisieren sollte, ohne irgendwelche Ports öffnen oder weiterleiten zu müssen. Da offene Ports immer ein potenzielles Sicherheitsrisiko darstellen wollte ich dies in jedem Fall vermeiden. Also begann ich, mich nach Alternativen umzusehen. Dabei stieß ich auf Twingate, Tailscale und NordVPN Meshnet. Diese Tools versprachen eine Peer-to-Peer-Verbindung ohne offene Ports oder statische IPs, was ideal schien.

Für dieses Proof-of-Concept fiel meine Wahl schließlich auf Meshnet von NordVPN.

Nachdem ich Meshnet dann auf der Workstation (optional, aber für den direkten Zugriff auf den Offsite-Pi ganz nützlich) und dem Onsite-Pi installiert und konfiguriert hatte, gab es allerdings ein Problem: Die erste Raspberry Pi Generation, die ich eigentlich als Offsite-Pi vorgesehen hatte, wurde von Meshnet nicht unterstützt. Daher habe ich mir kurzfristig ein Pi der 3. Generation organisiert.

Nach erfolgreicher Einrichtung wurde der Offsite-Pi mit dem Offsite-LAN verbunden und die beiden Pis konnten erfolgreich miteinander kommunizieren.

Bei Tests traten zwei Probleme auf, die nach einiger Recherche gelöst werden konnten:
Unter Umständen konnte der Onsite-Pi nicht per SSH mit dem Offsite-Pi verbunden werden. Die Lösung war, in der SSH-Konfiguration spezifisch den zu verwendenden Verschlüsselungsalgorithmus anzugeben. Auf dem Onsite-Pi wurde eine Config-Datei im .ssh-Ordner angelegt, die für den Offsite-Pi den Kex-Algorithmus ```curve25519-sha256``` festlegt:

```text
pi@onsite-pi:~/.ssh $ cat config
Host offsite-pi
    KexAlgorithms curve25519-sha256
```

Das zweite Problem betraf ebenfalls die SSH-Verbindung. Bei Befehlen, die eine größere Textausgabe erzeugten (z. B. ```htop``` oder ```restic -r /restic check```), blieb die Session hängen. Es stellte sich heraus, dass dies an der MTU (Maximum Transmission Unit) lag.

Die MTU beschreibt die maximale Größe eines Datenpakets, das ohne Fragmentierung übertragen werden kann. Wenn ein Paket größer als die MTU ist, wird es fragmentiert. Wenn eine Komponente auf dem Datenweg eine andere MTU-Einstellung hat als die anderen, funktioniert die Fragmentierung bzw. Zusammensetzung der Fragmente nicht mehr korrekt.

Das Problem lässt sich einfach mit unterschiedlichen Ping-Größen erkennen. Wenn ein Ping mit Paketgröße 1200 Bytes

```text
ping -s 1200 offsite-pi
```

durchgeht, aber mit Paketgröße 1400 Bytes

```text
ping -s 1400 offsite-pi
```

nicht mehr, dann handelt es sich wahrscheinlich um ein MTU-Problem.

Über den NetworkManager habe ich die MTU für den Meshnet-Adapter auf 1300 Bytes gesetzt, wodurch das Problem behoben wurde.

[![Einstellung der MTU in nmtui](/assets/images/posts/offsite-backup/MTU.png)](/assets/images/posts/offsite-backup/MTU.png)

Im Nachhinein fand ich es auch sehr spannend, dass die Meshnet-Adapter der Pis (und auch der Workstation) eine IP-Adresse aus dem Bereich 100.64.0.0/10 erhalten. Das ist der "IPv4 Shared Address Space", der normalerweise von Internet Service Providern für das Routing zwischen Kundenroutern und der ISP-Hardware verwendet wird. Es handelt sich um einen privaten Adressbereich, der nicht weitergeroutet wird. Meshnet verhält sich in Bezug auf das IP-Routing also wie ein kleiner ISP."

### Offsite-Backup

Nachdem Onsite-Backup und die Interkonnektivität zwischen Onsite-Pi und Offsite-Pi eingerichtet sind, besteht die letzte Herausforderung darin, die Daten vom Onsite-Pi zum Offsite-Pi zu kopieren. Dies kann einerseits durch Funktionalitäten von restic erledigt werden, andererseits aber auch durch rsync.

Der Befehl

```text
rsync -avz --delete -e ssh /home/pi/restic pi@offsite-pi:/restic-offsite
```

synchronisiert neue und geänderte Dateien vom Onsite-Pi zum Offsite-Pi und löscht auf dem Offsite-Pi Dateien, die auf dem Onsite-Pi nicht mehr vorhanden sind.

Dieser Befehl (oder ein Skript für den Befehl) kann als Cronjob auf dem Onsite-Pi hinterlegt werden und regelmäßig zu einem definierten Zeitpunkt (in diesem Fall jeden Sonntagabend) ausgeführt werden:

```text
# m h  dom mon dow   command
00 23 * * 0 bash /home/pi/restic-automation/backup.sh
```

Besonders bemerkenswert fand ich, dass diese Lösung sogar einen ca. 15-minütigen Ausfall der Verbindung zwischen Onsite-LAN und Offsite-LAN problemlos überstanden hat. Nachdem die Verbindung wiederhergestellt war, setzte rsync die Synchronisation einfach fort, ohne dass ich den Prozess neu starten musste.

## Fazit

Nachdem die Daten erfolgreich vom Onsite-Pi auf den Offsite-Pi gespiegelt wurden stellte sich heraus, dass die Wiederherstellung einer Testdatei vom Offsite-Backup mit restic erfolgreich möglich war. Das war ein gutes Gefühl zu sehen, dass das Proof-of-Concept tatsächlich funktioniert.

Durch dieses Setup kann ein relativ einfaches und kostengünstiges Offsite-Backup (mit optionalem Onsite-Backup) erstellt werden. Durch das Troubleshooting konnte ich meine Netzwerkkenntnisse erweitern und auch festigen. Solche Projekte eignen sich immer besonders gut, um konkrete Problemstellungen zu bearbeiten und dazuzulernen.
