---
layout: single
title: "Netbird als Alternative zu NordVPN Meshnet für Offsite-Backup"
date:   2025-09-23 
categories: projekt
tags: backup rpi meshnet netbird
excerpt: "Netbird als Alternative zu NordVPN Meshnet für Offsite-Backup"
toc: true
toc_sticky: true
header:
  overlay_image: assets/images/posts/netbird/jordan-harrison-40XgDxBfYXM-unsplash.jpg
  overlay_filter: 0.5 # same as adding an opacity of 0.5 to a black background
  caption:  "Foto von [Jordan Harrison](https://unsplash.com/@jouwdan?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash) auf [Unsplash](https://unsplash.com/photos/blue-utp-cord-40XgDxBfYXM?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash)"
---
Im April 2025 wurde auf meinem [Blog](/projekt/offsite-backup/) ein Ansatz vorgestellt, wie sich mit zwei Raspberry Pis und minimalem Budget ein zuverlässiges Offsite-Backup realisieren lässt. Die Lösung basierte auf NordVPN Meshnet, da damit ein virtuelles Peer-Netzwerk aufgebaut werden konnte, das offene Ports an Firewalls überflüssig machte. Geräte blieben so vor direkter Exponierung im Internet geschützt – ein zentraler Aspekt bei sensiblen Backup-Anforderungen.
Mit der Ankündigung, dass NordVPN Meshnet zum Jahresende 2025 wegen zu geringer Nutzerzahlen eingestellt wird, entsteht jedoch Handlungsbedarf für bestehende Setups.
Im persönlichen Umfeld wurde Netbird als Open-Source-Lösung empfohlen, die den Funktionsumfang von Meshnet weitgehend abdeckt.

## Installation und Einrichtung von Netbird

Die Registrierung bei Netbird gestaltete sich unkompliziert. Für den Hausgebrauch genügt die kostenfreie Variante, sofern auf High-Availability-Routing verzichtet werden kann. Die Installation des Services auf den Raspberry Pis verlief zügig. Besonders praktisch ist die Möglichkeit, Geräte per Einmal-Code und URL mit dem Netbird-Account zu verknüpfen – gerade für SSH-only erreichbare Systeme ein deutlicher Vorteil.
Nach Abschluss der Registrierung erscheinen die eingebundenen Systeme im Peer-Netzwerk. Im administrativen Dashboard fällt auf, dass Netbird, analog zu Meshnet, IP-Adressbereiche aus dem öffentlichen Raum nutzt, die für Heimnetze typischerweise nicht relevant sind. Das reduziert Konfliktpotenzial deutlich.
Für die Anpassung des bestehenden Backup-Skripts genügt es, den von Netbird automatisch vergebenen Hostnamen im Format `[Hostname].netbird.cloud` zu übernehmen.

[![Schema der automatisierten Blockierung](/assets/images/posts/netbird/netbird-dashboard.jpg)](/assets/images/posts/netbird/netbird-dashboard.jpg)

## Praxiserfahrungen und Sitzungsverwaltung

Im 14-tägigen Dauerbetrieb zeigte sich ein nicht unwesentlicher Unterschied zu Meshnet: Standardmäßig laufen Netbird-Sitzungen nach einer gewissen Zeit ab, was zu Verbindungsabbrüchen zwischen den Hosts führt. Die Option zum dauerhaften Authentifizieren ist aber in den Einstellungen schnell gefunden und kann in wenigen Schritten aktiviert werden.

## Funktionen und Vergleich zu Meshnet

Die Funktionsvielfalt fällt positiv auf. Netbird bietet granulare Steuerungsmöglichkeiten für die Kommunikation zwischen einzelnen Hosts und stellt Werkzeuge bereit, die auch für größere und heterogene Netzwerke relevant sind. In Punkto Kontrolle und Erweiterbarkeit werden gegenüber Meshnet sogar zusätzliche Optionen sichtbar. Fehlende Features oder Limitationen im Vergleich zur bisherigen Lösung zeigten sich im Testverlauf nicht.

## Fazit

Netbird präsentiert sich als solide, schnell aufgesetzte Alternative zu Meshnet für den Aufbau privater Peer-to-Peer-VPNs. Die Einrichtung ist modern und durchdacht, der Betrieb stabil. In Kombination mit Open-Source-Charakter und ausbaufähigem Funktionsumfang empfiehlt sich Netbird als zukunftstaugliche Lösung für sichere Offsite-Backups nach Auslauf von Meshnet.
