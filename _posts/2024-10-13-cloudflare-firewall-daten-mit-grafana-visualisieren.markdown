---
layout: single
title: "Anleitung: Visualisierung von Cloudflare Firewall-Daten mit Grafana"
date:   2024-10-13 
categories: projekt
tags: dashboard grafana cloudflare firewall
excerpt: "Anleitung zur Visualisierung von Cloudflare Firewall Events in einem Grafana Dashboard"
header:
  overlay_image: /assets/images/posts/cf-dashboard-tut/choong-deng-xiang--WXQm_NTK0U-unsplash.jpg
  overlay_filter: 0.5 # same as adding an opacity of 0.5 to a black background
  caption:  "Foto von [Choong Deng Xiang](https://unsplash.com/@dengxiangs?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash) auf [Unsplash](https://unsplash.com/photos/graphical-user-interface--WXQm_NTK0U?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash)"
---
[![Einstellungen der API Tokens im Cloudflare Account Bereich](/assets/images/posts/cf-dashboard-tut/Dashboard.png)](/assets/images/posts/cf-dashboard-tut/Dashboard.png)

Im letzten Blogpost wurden die Erfahrungen bei der Erstellung eines Grafana-Dashboards zur Visualisierung von Cloudflare Firewall-Events geteilt. Der Artikel ist [hier](https://fourframes.de/projekt/cloudflare-firewall-grafana-dashboard/) zu finden. Dieser Beitrag erklärt Schritt für Schritt, wie das Dashboard selbst für einen Cloudflare-Account genutzt werden kann.

## API-Token für Cloudflare generieren

[![Einstellungen der API Tokens im Cloudflare Account Bereich](/assets/images/posts/cf-dashboard-tut/cf_token.png)](/assets/images/posts/cf-dashboard-tut/cf_token.png)

Für die Nutzung des Dashboards wird ein API-Token benötigt, um Daten vom Cloudflare API-Endpunkt über die Infinity Data Source in Grafana abzurufen.

1. **Token erstellen**: Im Cloudflare-Dashboard unter `My Profile` -> `API Tokens` den Bereich für die API-Tokens aufrufen.
2. **Neuen Token anlegen**: Ein neues Token kann durch Klick auf „Create Token“ erstellt werden. Dabei empfiehlt es sich, das Template „Read analytics and logs“ auszuwählen, da es die erforderlichen Berechtigungen für den Zugriff auf die notwendigen Daten enthält.

## Datenquelle in Grafana konfigurieren

[![Konfiguration der Infinity Data Source in Grafana](/assets/images/posts/cf-dashboard-tut/infinity.png)](/assets/images/posts/cf-dashboard-tut/infinity.png)

Nachdem die Infinity Data Source als neue Datenquelle in Grafana hinzugefügt wurde, ist folgende Konfiguration erforderlich:

1. **Datenquelle hinzufügen**: Die Infinity Data Source als Datenquelle auswählen.
2. **Authentication**: Der zuvor erstellte Bearer Token muss in den Einstellungen unter „Authentication“ eingetragen werden.
3. **Host angeben**: In der Konfiguration sollte der Host für den GraphQL-Endpunkt eingetragen werden: `https://api.cloudflare.com/client/v4/graphql`.

## Dashboard konfigurieren und anpassen

[![Einstellungen des Dashboards in Grafana](/assets/images/posts/cf-dashboard-tut/dashboard_settings.png)](/assets/images/posts/cf-dashboard-tut/dashboard_settings.png)

Zur Konfiguration des Dashboards sind folgende Schritte notwendig:

1. **Dashboard importieren**: Das Dashboard kann mit der JSON-Datei aus dem [GitHub-Projekt](https://github.com/fourframes/grafana-cloudflare-firewall-dashboard) importiert werden.
2. **Datenquelle verknüpfen**: Es ist sicherzustellen, dass das Dashboard mit der zuvor eingerichteten Infinity Data Source verknüpft ist.
3. **Account ID hinterlegen**: Die Account ID, die im Cloudflare-Dashboard zu finden ist, sollte im Dashboard hinterlegt werden. Der Accountname im Dashboard kann nach Belieben angepasst werden.

## Beiträge zur Dashboard-Entwicklung

Beiträge zur Weiterentwicklung, Optimierung oder Korrektur des Dashboards sind willkommen. Dabei ist darauf zu achten, dass das Dashboard weiterhin mit kostenlosen Cloudflare-Accounts kompatibel bleibt. Für Fragen und Anmerkungen steht die E-Mail-Adresse <blog@fourframes.de> zur Verfügung.
