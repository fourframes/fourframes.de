---
layout: single
title: "Honaipot Reloaded - Honeypot Webapp mit automatisiertem Blocking"
date: 2025-08-18
categories: projekt
tags: honeypot ai web cloudflare
excerpt: "Honeypot Webapp mit automatisiertem Blocking dank Canary Token und Cloudflare Workers"
toc: true
toc_sticky: true
header:
  overlay_image: assets/images/posts/honaipot/jj-ying-8bghKxNU1j0-unsplash.jpg
  overlay_filter: 0.5 # same as adding an opacity of 0.5 to a black background
  caption:  "Foto von [JJ Ying](https://unsplash.com/@jjying?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash) auf [Unsplash](https://unsplash.com/photos/purple-and-blue-light-digital-wallpaper-8bghKxNU1j0?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash)"
---

Nach der ersten erfolgreichen Honeypot-Aktion mit Vibe Coding folgt jetzt der nächste Schritt: Automatisches Blockieren von Angreifer-IPs direkt nach dem Canary-Token-Trigger. Nach meinem initialen [Blogartikel](/projekt/honaipot/) über das Honey-Pot-Projekt habe ich das Projekt konsequent weiterentwickelt und in den letzten Wochen eine spannende Erweiterung eingebaut.

## Rückblick: So lief die erste Honeypot-Phase

Das Setup war bewusst realitätsnah gestaltet und wartete – gemeinsam mit zwei Canary Tokens – auf neugierige Besucher. Es dauerte über einen Monat, bis ein Canary Token ausgelöst wurde: Jemand fand die Website, las vermutlich den Code und stieß dabei auf die Klartext-Credentials. Ich halte es für wahrscheinlich, dass der Quelltext gezielt untersucht und die Credentials entnommen wurden. Ein klassischer Bruteforce-Angriff ist dagegen eher unwahrscheinlich – die Website war zusätzlich durch die Cloudflare WAF abgesichert, die solche Attacken in der Regel unterbindet. Interessant war, dass beide Canary Tokens ausgelöst wurden – einmal direkt nach erfolgreichem Login, einmal nach Klick auf den fingierten Download-Link. Der Akteur besuchte die Honeypot-Seite mehrfach und zu unterschiedlichen Uhrzeiten.

## Next Level: Angreifer automatisch blockieren

Die Canary Tokens liefern beim Auslösen eine IP-Adresse – und können via Webhook direkt einen Worker triggern. Meine Idee: Die verdächtige IP sofort per Cloudflare-API auf eine Blockliste setzen. So wird jedem Angreifer, der sich am Honeypot anmeldet, der Zugriff auf die Seite augenblicklich entzogen.

[![Schema der automatisierten Blockierung](/assets/images/posts/honaipot/auto_block.png)](/assets/images/posts/honaipot/auto_block.png)

Bonus: Die IPs sammeln sich automatisch auf einer Liste, die gemeldet oder beobachtet werden kann. Eigentliches Ziel: Mein Know-how rund um Cloudflare Workers und deren Webhook-Handling vertiefen.

### KI als Entwicklungspartner: Worker mit Vibe Coding, Perplexity & ChatGPT

Auch dieses Mal startete ich mit Vibe Coding und nutzte Perplexity und ChatGPT als Coding-Assistenten. Das Grundgerüst des Workers entstand zügig: Anforderungen skizziert, Wunsch nach Python-Implementierung ausgesprochen – und schon lag der erste Worker-Entwurf vor. Doch die Praxis zeigte, wie wertvoll menschliche Interaktion beim KI-Coding bleibt:

- Das Canary-Webhook-JSON bereitete Parsing-Schwierigkeiten, die ohne Debugging nicht zu lösen waren.
- Perplexity wollte sensible Account-Daten als Variablen im Code verwalten – ein kurzer Sicherheitshinweis („Nutze Worker-Secrets!“) genügte, und der Code wurde angepasst.
- Weder ChatGPT noch Perplexity konnten die extrahierte IP korrekt an die Cloudflare-API übergeben. Hier half klassisches Troubleshooting und eine kurze Google-Recherche (StackOverflow sei Dank).

### Testlauf: Blockierte IP, direkter Effekt

Als der Worker endlich alle Canary-IP-Trigger verlässlich an die Cloudflare-API übergab und diese die IPs automatisch auf die Blockliste setzte, folgten Praxistests. Ergebnis: Die Blockierung läuft in Echtzeit – der Besucher merkt sofort, dass sein Zugriff gesperrt ist (sofern kein Browser-Cache genutzt wird).

[![Schema der automatisierten Blockierung](/assets/images/posts/honaipot/blocked.png)](/assets/images/posts/honaipot/blocked.png)

## Fazit & Ausblick

Das Projekt war extrem lehrreich: Canary Tokens, Cloudflare Workers und KI-basiertes Coding bilden ein starkes Setup für modernes Security-Prototyping. Die KI hilft beim Grundgerüst, aber der Feinschliff kommt immer noch vom Entwickler. Wer das Projekt ausbauen will: Die blockierten IPs könnten künftig auch direkt an Dienste wie AbuseIPDB gemeldet werden – schließlich deutet das Auslesen und Verwenden von Credentials im Quellcode selten auf gute Absichten hin.
Im Praxiseinsatz ist mir aufgefallen, dass manche DNS-Blocker die URLs von Canary Tokens herausfiltern oder blockieren. Das hat zur Folge, dass ein Token gar nicht auslöst und somit auch keine IP gesperrt wird. Um dieses Problem zu umgehen, plane ich die Entwicklung eines Worker-Proxys, der den Canary-Trigger unabhängig vom originalen Token-Link ausführt. So wird der Token-Trigger über einen eigenen Endpunkt gesendet und intern an Canary weitergeleitet, ohne die eigentliche Canary-URL direkt aufzurufen. So lässt sich die Mechanik auch dann nutzen, wenn Angreifer oder Infrastruktur aktiv gängige Canary-Domains blockieren – der Honaipot bleibt damit effektiver und kann auch verdeckt arbeiten.

Den gesamten Worker-Quellcode integriere ich zeitnah ins Honaiblock-Repo auf Github:  <https://github.com/fourframes/honaiblock>
Eine ausführliche Anleitung für den eigenen Honeypot folgt – Stay tuned!
