---
layout: single
title: "Netzwerksegmentierung mit OpenWRT und VLANs – Erfahrungsbericht"
date:   2025-10-15 
categories: projekt
tags: projekt netzwerk segmentierung
excerpt: "Nutzung von VLANs zur weiteren Segmentierung des Heimnetzes."
toc: true
toc_sticky: true
header:
  overlay_image: /assets/images/posts/segmentierung/jordan-harrison-40XgDxBfYXM-unsplash.png
  overlay_filter: 0.5 # same as adding an opacity of 0.5 to a black background
  caption:  "Foto von [Jordan Harrison](https://unsplash.com/@jouwdan?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash) auf [Unsplash](https://unsplash.com/photos/blue-utp-cord-40XgDxBfYXM?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash)"
---
Im [vergangenen Jahr](/projekt/netwerksegmentierung-im-heimnetz/) ging es darum, wie eine Fritzbox zur einfachen Netzwerksegmentierung im Heimnetz verwendet werden kann. Dabei stand vor allem das Gastnetzwerk im Fokus, das sich über einen separaten LAN-Port ausgeben lässt. Allerdings offenbart dieses Vorgehen auch praktische Einschränkungen: Beide Netze müssen physisch separat verkabelt werden, was schnell in einen Kabel- und Geräteaufwand ausartet. Um mehr Flexibilität zu bekommen und die eigenen Kenntnisse im Bereich VLANs auszubauen, war der nächste Schritt die Integration von VLAN-fähigen Switchen ins Netzwerk.

## Hardware und Firmware

Durch ein günstiges Angebot sind zwei Netgear GS308T ins Haus gekommen. Zwar sind sie offiziell abgekündigt, mit OpenWRT gibt es aber eine alternative Firmware, deren Funktionsumfang und Aktualität das Gerät noch einmal stark aufwerten kann. Das Aufspielen von OpenWRT war unkompliziert: Nach dem Flashen des Basis-Images und anschließendem Upgrade auf die vollständige Version stand dem nächsten Netzwerkexperiment nichts mehr im Weg. Der Zugang zu den Geräten erfolgt nach wie vor klassisch – also Rechner ins 192.168.1.0/24-Netz bringen – und weiter geht’s.

## Grundlagen: Tagged und Untagged

Für den Umgang mit VLANs ist es hilfreich, die Begriffe „tagged“ und „untagged“ zu verstehen. Als untagged-Port konfiguriert, verhält sich ein Switchport wie ein klassischer LAN-Port: Das angeschlossene Gerät bekommt keinerlei VLAN-Informationen mit; das Netzwerk fühlt sich für das Endgerät exakt wie ein „normales“ Netz an. Ein Beispiel: Ist Port 3 als untagged für VLAN 20 gesetzt, sehen Geräte an Port 3 nur das VLAN 20, ohne selbst etwas vom VLAN-Konzept zu bemerken.

Wird ein Port hingegen als tagged konfiguriert, passieren Pakete mit VLAN-Kennung am Port. Das angeschlossene Gerät muss VLAN-Tags verarbeiten können. Der Vorteil: Auf einem Port können so mehrere VLANs gleichzeitig übertragen werden. Dies wird im Heimbereich typischerweise genutzt, um mit einem sogenannten Trunk-Kabel beliebig viele VLANs zwischen Switches zu führen. Geräte ohne VLAN-Unterstützung (zum Beispiel einfache PCs, Drucker oder IoT-Geräte) kommen weiterhin untagged ins Netz, während VLAN-fähige Devices mit mehreren Netzen parallel umgehen können.

## VLAN-Setup

In der Praxis landen bei diesem Setup das „normale“ Heimnetz (hinter der Fritzbox) im VLAN 20, das Gästenetzwerk wird als VLAN 30 geführt – beides als untagged an den entsprechenden Ports. Der Trick: Mit einem getaggten Port können beide Netze über ein einziges Netzwerkkabel zum zweiten Switch geführt werden. Nun lässt sich jedem Port individuell zuweisen, in welches Netz ein Gerät einsortiert wird – entweder ins Heimnetz oder ins Gäste-Netz.

[![Konfiguration der Ports und VLANs](/assets/images/posts/vlan-segmentierung/port-vlan-tagging.png)](/assets/images/posts/vlan-segmentierung/port-vlan-tagging.png)

Es empfiehlt sich, das Default-VLAN 1 unangetastet zu lassen und – sofern ein dediziertes Management-Netz benötigt wird – ein weiteres, separates VLAN dafür anzulegen. In vielen Anleitungen und Community-Diskussionen wird dies zur besseren Übersicht dringend angeraten.

## Management und Firewall

Initial war auf dem Switch jeweils ein Interface in jedem der VLANs aktiv, entsprechend war der Switch über mehrere Netze ansprechbar. Nach etwas Recherche zeigte sich jedoch: Für das einfache Heimnetz genügt es, das Switch-Management auf ein VLAN zu beschränken. In diesem Fall war das VLAN 20. Firewall-Regeln, die den Zugang aus anderen VLANs sperren, sorgen für zusätzliche Sicherheit – obwohl sie bei nur einem aktiven Management-Interface eher eine zweite Verteidigungslinie darstellen.

[![Konfiguration Interfaces](/assets/images/posts/vlan-segmentierung/network-interfaces.png)](/assets/images/posts/vlan-segmentierung/network-interfaces.png)

## Inbetriebnahme und Test

Jedes VLAN wurde separat getestet, angefangen mit einfachen Ping-Tests von einem Segment ins andere. Auch die Trunk-Konnektivität zeigte sich zuverlässig: Beide Switche tauschen auf dem definierten Port VLAN-getaggte Pakete ohne Probleme aus. Die Konfiguration ließ sich so schrittweise überprüfen und anpassen.

## Fazit und Ausblick

Die Erweiterung des Heimnetzes um VLANs und OpenWRT hat keinen riesigen materiellen Aufwand bedeutet, aber viele neue Perspektiven auf Netzwerksegmente, Firewall-Regeln und OpenSource-Firmware eröffnet. Das Thema Netzwerküberwachung – beispielsweise mit Zeek und Port-Mirroring – steht als nächstes auf der persönlichen Testliste und verspricht weitere spannende Einblicke.
