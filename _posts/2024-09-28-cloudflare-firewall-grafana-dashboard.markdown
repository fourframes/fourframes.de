---
layout: single
title: "Projektbericht: Visualisierung von Cloudflare Firewall-Daten mit Grafana"
date:   2024-09-28 
categories: projekt
tags: dashboard grafana cloudflare firewall
excerpt: "Visualisierung von Cloudflare Firewall Events in einem Grafana Dashboard"
header:
  overlay_image: /assets/images/posts/cf-dashboard/markus-winkler-IrRbSND5EUc-unsplash.jpg
  overlay_filter: 0.5 # same as adding an opacity of 0.5 to a black background
  caption:  "Foto von [Markus Winkler](https://unsplash.com/@markuswinkler?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash) auf [Unsplash](https://unsplash.com/photos/black-and-silver-laptop-computer-IrRbSND5EUc?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash)"
---
Der Einsatz der Cloudflare Firewall bietet viele Vorteile, insbesondere durch detaillierte Informationen zu Sicherheitsereignissen und ergriffenen Gegenmaßnahmen. Ein Beispiel hierfür ist die Hotlink Protection, die verhindert, dass Bilder direkt verlinkt werden, und stattdessen eine Fehlerseite anzeigt. Auch Systeme, die nach Schwachstellen suchen (außer Suchmaschinen-Bots), erhalten nur eine Fehlermeldung, anstatt Zugriff auf die Seite.

Um mein Wissen über Grafana aufzufrischen, suchte ich nach einem passenden Projekt und entschied mich, die Cloudflare-Daten zu visualisieren.

## Die Idee hinter dem Projekt

Obwohl Cloudflare eine Übersicht über alle Firewall-Ereignisse bietet, fehlen in der kostenlosen Version umfassende Visualisierungsmöglichkeiten. Meine Idee war es, diese Ereignisse in Form von Karten und verschiedenen Grafiken darzustellen. Damit lässt sich auf einen Blick erkennen, wo die Sicherheitsereignisse ihren Ursprung haben, welche Gegenmaßnahmen ergriffen wurden, welche (Sub-)Seiten betroffen waren und welche Technologien eingesetzt wurden.

Dabei war es mir besonders wichtig, eine minimalistische Lösung zu finden, die keinen zusätzlichen Infrastrukturaufwand oder weitere Kosten verursacht.

## Der Lösungsweg: Von der Idee zur Umsetzung

Ich habe schnell die GraphQL-Schnittstelle von Cloudflare entdeckt, die es ermöglicht, Firewall-Daten gezielt abzufragen. Viele öffentliche Cloudflare-Dashboards verwenden die „Infinity Datasource“, um GraphQL-Abfragen durchzuführen. Mit einem API-Token konnte ich problemlos die Daten meines Accounts abrufen. Für erste Tests habe ich Altair verwendet, um die Abfragen durchzuführen.

Obwohl Abfragen in einem Basis-Account von Cloudflare teilweise eingeschränkt sind, sind sie dennoch ausreichend, um grundlegende Informationen im Dashboard darzustellen. In einigen Fällen müssen die Daten jedoch transformiert werden, um sie optimal zu visualisieren.

## Das Ergebnis: Ein übersichtliches Dashboard für Cloudflare-Daten

[![Dashboard zur Visualisierung von Cloudflare Firewall-Daten mit Grafana](/assets/images/posts/cf-dashboard/Dashboard.png)](/assets/images/posts/cf-dashboard/Dashboard.png)

Das resultierende Dashboard zeigt eine geografische Karte, auf der die Ursprünge der Sicherheitsereignisse visualisiert werden. Zu den weiteren Visualisierungen gehören:

- Die absolute Anzahl der Ereignisse
- Der spezifische Pfad, auf den sich das Ereignis bezog
- Der User-Agent, der hinter dem Ereignis steht
- Die Maßnahmen, die durch die Firewall ergriffen wurden
- Ein Zeitverlauf der Ereignisse, der es ermöglicht, die Aktivitäten stündlich zu verfolgen

## Fazit: Ein praktisches Dashboard für Cloudflare-Nutzer

Das Dashboard bietet eine einfache und effektive Visualisierung der Cloudflare Firewall-Daten. Es hilft, aktuelle Sicherheitsereignisse und die Reaktionen der Firewall auf einen Blick zu erfassen. Ein kleiner Nachteil ist, dass nur ein Zeitraum von 24 Stunden betrachtet werden kann, was jedoch eine Einschränkung für kostenlose Cloudflare-Accounts ist. Abonnenten haben die Möglichkeit, längere Zeiträume auszuwählen.

Falls du das Dashboard selbst nutzen möchtest, habe ich es zusammen mit einer englischen Kurzanleitung auf GitHub veröffentlicht: [Grafana Cloudflare Firewall Dashboard auf GitHub](https://github.com/fourframes/grafana-cloudflare-firewall-dashboard).
