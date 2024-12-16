---
layout: single
title: "Netzwerksegmentierung im Heimnetz: Sicherheitsvorteile und praktische Umsetzung"
date:   2024-07-29 
categories: projekt
tags: projekt netzwerk segmentierung schwachstelle härtung
excerpt: "Reduktion von potenziellen Sicherheitsschwachstellen durch Segmentierung im Heimnetz."
header:
  overlay_image: /assets/images/posts/segmentierung/jordan-harrison-40XgDxBfYXM-unsplash.png
  overlay_filter: 0.5 # same as adding an opacity of 0.5 to a black background
  caption:  "Foto von [Jordan Harrison](https://unsplash.com/@jouwdan?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash) auf [Unsplash](https://unsplash.com/photos/blue-utp-cord-40XgDxBfYXM?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash)"
---
Netzwerksegmentierung, also das Teilen von Netzwerken in kleinere, isolierte Segmente, wird oft in großen Unternehmensnetzwerken eingesetzt. Doch auch im eigenen Heimnetzwerk kann die Segmentierung erhebliche Sicherheitsvorteile bieten. Mit der Zunahme von "smarten" Geräten, die im Heimnetz verbunden sind – von Steckdosen und Lampen bis hin zu Waschmaschinen – steigt auch die Anzahl potenzieller Sicherheitslücken.

## Warum Netzwerksegmentierung im Heimnetz?

Viele Heimrouter sind so konfiguriert, dass sie eine Firewall zwischen dem Heimnetz und dem WAN (Wide Area Network) haben, jedoch keine spezifischen Firewall-Regeln innerhalb des Heimnetzes. Dies bedeutet, dass alle Geräte im Heimnetzwerk frei miteinander kommunizieren und Daten austauschen können. Diese Konfiguration erleichtert zwar die Nutzung, da keine zusätzlichen Einstellungen nötig sind, um beispielsweise ein Notebook mit einem NAS zu verbinden, birgt jedoch auch Risiken.

## Sicherheitsrisiken eines unsegmentierten Heimnetzes

In einem unsegmentierten Heimnetzwerk kann ein kompromittiertes Gerät, wie etwa eine smarte Steckdose mit bösartiger Software, einen Netzwerkscan durchführen und diese Daten an Angreifer weiterleiten. Über Pings und andere Protokolle können Informationen darüber gesammelt werden, wie viele und welche Geräte im Netz sind. Wenn diese Geräte keine Nutzerauthentifizierung für bestimmte Dienste wie Dateiaustausch oder Drucker haben, könnte bösartige Software auf diese Dienste zugreifen und Daten exfiltrieren.
Ein weiterer Angriffsvektor besteht darin, dass ein böswilliges Gerät überwachen kann, welche Geräte zu welcher Zeit im Netz sind. Durch zusätzliche Informationen, wie den Hostnamen, lässt sich oft herausfinden, um welche Art von Gerät es sich handelt. Diese Informationen können über einen Zeitraum hinweg analysiert werden, um festzustellen, wann ein Mobiltelefon im WLAN ist und wann nicht. Daraus lässt sich ableiten, ob der Besitzer des Smartphones zu Hause ist oder nicht – Daten, die für Einbruchs- und Diebstahlversuche sehr relevant sind.

## Umsetzung der Netzwerksegmentierung im Heimnetz

Nicht alle Router bieten Netzwerksegmentierung an, aber Modelle wie die FRITZ!Box ermöglichen es, neben dem Heimnetz auch ein Gastnetzwerk einzurichten. Das Gastnetzwerk ist ein separates Subnetz, das vom Heimnetz isoliert ist. Es kann als zusätzliches WLAN-Netzwerk oder über einen Netzwerkport der FRITZ!Box verfügbar gemacht werden. Dieses Gastnetzwerk kann so konfiguriert werden, dass nicht nur eine logische Trennung vom Heimnetz besteht, sondern auch der Kontakt zwischen den Geräten im Gastnetzwerk unterbunden wird. Dadurch wird das Ausspionieren des Netzwerks erheblich erschwert.
Geräte, die als weniger vertrauenswürdig gelten oder keinen Kontakt zu anderen Geräten benötigen, können einfach in das Gastnetzwerk eingebunden werden, während vertrauenswürdige Geräte im Heimnetzwerk verbleiben. Diese anfängliche Netzwerkeinteilung erfordert zwar etwas Aufwand, aber der laufende Betrieb des Netzwerks bleibt überschaubar einfach. Neue Geräte werden entweder mit dem Heimnetzwerk oder dem Gastnetzwerk verbunden, und schon sind die jeweiligen Sicherheitsmaßnahmen aktiv.

## Persönliche Erfahrungen mit der Netzwerksegmentierung

Ich habe die Netzwerksegmentierung nun seit gut zwei Monaten im Einsatz und bin sehr zufrieden. Die zusätzliche Sicherheit und die Kontrolle über die Kommunikation zwischen den Geräten im Netzwerk geben mir ein gutes Gefühl. Die Einrichtung war zwar etwas zeitaufwändig, aber der tägliche Betrieb ist unkompliziert und effizient.
