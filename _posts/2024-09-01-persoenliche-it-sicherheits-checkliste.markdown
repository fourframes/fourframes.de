---
layout: single
title: "Persönliche Checkliste für IT-Sicherheit"
date:   2024-09-01 
categories: lernen
tags: härtung ressourcen
excerpt: "Eine Checkliste für die eigene persönliche IT-Sicherheit."
header:
  overlay_image: https://media.fourframes.de/blog/checklist/philipp-katzenberger-iIJrUoeRoCQ-unsplash.png
  overlay_filter: 0.5 # same as adding an opacity of 0.5 to a black background
  caption:  "Foto von [Philipp Katzenberger](https://unsplash.com/@fantasyflip?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash) auf [Unsplash](https://unsplash.com/photos/closeup-photo-of-turned-on-blue-and-white-laptop-computer-iIJrUoeRoCQ?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash)"
---
## Einleitung

In der heutigen digitalen Welt ist es wichtiger denn je, sich vor Bedrohungen im Internet zu schützen. Cyberangriffe, Datenlecks und Phishing sind nur einige der Gefahren, denen wir täglich ausgesetzt sind. Ein sicheres Online-Verhalten und der richtige Umgang mit persönlichen Daten sind daher unerlässlich.

>Diese umfassende Checkliste basiert auf dem Projekt [personal-security-checklist](https://github.com/Lissy93/personal-security-checklist/) von [Alicia Sykes](https://github.com/Lissy93) und wurde ins Deutsche übersetzt und angepasst.

Die Checkliste bietet dir wertvolle Tipps und bewährte Praktiken, um deine digitale Sicherheit zu erhöhen. Egal ob es um die Sicherung deiner Passwörter, das sichere Surfen im Internet oder den Schutz deiner E-Mail-Konten geht.

## Authentifizierung

- Verwende für jedes Konto ein langes, sicheres und eindeutiges Passwort (hier kannst du es prüfen: [How Secure is my Password?](https://www.security.org/how-secure-is-my-password/)).
- Nutze einen sicheren Passwortmanager, der Zugangsdaten sicher und verschlüsselt speichert. Beispiele: [Bitwarden](https://bitwarden.com), [KeePass](https://keepass.info) oder [KeePassXC](https://keepassxc.org).
- Aktiviere 2-Faktor-Authentifizierung überall, wo es möglich ist, und nutze eine *Authenticator App* oder einen *Hardware Token*.
- Sichere die Wiederherstellungscodes, die du bei der Aktivierung von der 2-Faktor-Authentifizierung erhältst, als Ausdruck an einem sicheren Ort oder auf einem verschlüsselten Datenträger.
- Registriere dich für Benachrichtigungen zur Veröffentlichung deiner Zugangsdaten. Dienste wie [Firefox Monitor](https://monitor.firefox.com) oder [HaveIBeenPwned](https://haveibeenpwned.com) informieren dich darüber, wenn deine Zugangsdaten veröffentlicht wurden.

## Sicheres Surfen

- Nutze einen sicheren Webbrowser wie [Brave](https://brave.com) oder [Firefox](https://www.mozilla.org/de/firefox/new/) und aktiviere eine datenschutzfreundliche Suchmaschine wie [DuckDuckGo](https://duckduckgo.com).
- Gib niemals Informationen auf Webseiten ein, die keine Verschlüsselung nutzen (HTTP statt HTTPS). Browser zeigen ein Schloss-Symbol an, wenn die Verschlüsselung aktiviert ist. Zudem bieten Browser wie Firefox, Chrome, Edge und Safari dedizierte HTTPS-Sicherheitsfeatures an, die beispielsweise nur das Browsern auf sicheren Webseiten (HTTPS) erlauben.
- Nutze Browser-Erweiterungen, die Drittanbieter-Tracker und Werbung blockieren, wie [Privacy Badger](https://privacybadger.org) oder [uBlock](https://github.com/gorhill/uBlock).
- Halte deinen Browser stets auf dem neuesten Stand und installiere Updates. Prüfe die Sicherheits- und Privatsphäreneinstellungen und deinstalliere unnötige Erweiterungen/Add-ons.
- Trenne dein Surfverhalten in Kategorien wie Arbeit, Soziales, Shopping etc. Nutze hierfür [Firefox Containers](https://support.mozilla.org/de/kb/firefox-tab-container), separate Browser oder separate Browser-Profile.
- Überlasse das Speichern von Passwörtern nicht deinem Browser, sondern deinem Passwortmanager (siehe Authentifizierung). Deaktiviere auch das Speichern/automatische Ausfüllen weiterer Daten (wie Adressen, Zahlungsdaten etc.).
- Lösche regelmäßig deine Cookies, Session-Daten und deinen Cache. Erweiterungen wie [Cookie-Auto-Delete](https://github.com/Cookie-AutoDelete/Cookie-AutoDelete) können dies automatisch erledigen.
- Melde dich nicht in deinem Browser an, da dies weitere private Daten von dir verlinken kann. Für das Synchronisieren von Lesezeichen gibt es auch Open-Source-Lösungen.
- Dienste wie [Decentraleyes](https://decentraleyes.org) können deine Trackbarkeit über CDNs reduzieren.
- Services wie [FirstpartySimulator](https://firstpartysimulator.org/), [BrowserLeaks](https://browserleaks.com) oder [Am I Unique](https://amiunique.org/fp) können prüfen, wie dein Browser getrackt werden kann und welche Daten er preisgibt.
- Für anonymes Browsen kann der [Tor Browser](https://www.torproject.org/) genutzt werden. Vermeide jedoch, dich damit in persönliche Accounts einzuloggen.

## Mobiltelefon

- Setze eine lange, zufällige Geräte-PIN. Aktiviere die Fingerabdruck-Authentifizierung, aber vermeide die Authentifizierung mit dem Gesicht.
- Verschlüssele die Daten auf deinem Mobiltelefon. Auf Android-Geräten findest du die Option unter `Einstellungen --> Sicherheit & Standort --> Verschlüsselung`. Auf iOS-Geräten ist die Datenverschlüsselung aktiv, wenn biometrische Authentifizierungsmethoden wie Touch ID oder Face ID aktiviert sind (`Einstellungen --> TouchID & Passcode`).
- Halte dein System immer auf dem neuesten Stand und installiere Updates für das Betriebssystem und Apps so früh wie möglich.
- Prüfe die Zugriffsrechte der Apps und erlaube keinen Zugriff auf Funktionen und Daten, die die App nicht benötigt.
- Deaktiviere alle Verbindungsfunktionen (WLAN, Bluetooth etc.), wenn du sie nicht benötigst. "Vergiss" WLAN-Netzwerke, die du nicht mehr nutzt.
- Der Standortverlauf sollte deaktiviert werden. Android und iOS können den Verlauf deines Standorts speichern. Drittanbieter-Apps können den Standort jedoch auch loggen und speichern (über Mobilfunknetz, Wi-Fi oder Bluetooth).
- Eine *Application Firewall* kann genutzt werden, um bestimmten Apps den Zugriff auf das Internet zu sperren. Auf Android gibt es z.B. [NetGuard](https://www.netguard.me/), auf iOS z.B. [Lockdown](https://apps.apple.com/in/app/lockdown-apps/id1469783711).
- Apps können Tracker enthalten, die Daten sammeln und weiterleiten.

## E-Mail

Eine der größten Gefahren für die IT-Sicherheit ist immer noch Phishing. Es ist sehr wichtig, deinen E-Mail-Account sicher zu halten. Wenn ein Angreifer Zugriff auf dein Postfach erhält, kann er sich als dich ausgeben und die Passwörter deiner Accounts zurücksetzen, sofern diese keine Multifaktorauthentifizierung aktiviert haben.

- Nutze ein langes, starkes und einzigartiges Passwort für deinen E-Mail-Account und aktiviere die 2-Faktor-Authentifizierung.
- Ziehe einen sicheren Mailprovider in Betracht, der Mails verschlüsselt, z.B. [ProtonMail](https://protonmail.com) oder [Tutanota](https://tutanota.com).
- Nutze Email-Aliase, um deine eigentliche Mailadresse zu verstecken. Diese Aliase ermöglichen, dass alle E-Mails im Posteingang landen, ohne die eigentliche Mailadresse preiszugeben.
- Deaktiviere das automatische Laden von Medien in E-Mails. Diese Medien können Nutzerverhalten tracken und Schadsoftware enthalten.
- Durch die Nutzung einer eigenen Domain für E-Mails können Mail-Adressen weiterhin genutzt werden, wenn der Mail-Provider seinen Dienst einstellt.
- Nutze einen sicheren Mail-Client, z.B. [Thunderbird](https://www.thunderbird.net), der auch zur Sicherung von E-Mails verwendet werden kann.

## Sichere Nachrichtenübermittlung

- Nutze einen sicheren Messenger, der Open Source ist und Nachrichten Ende-zu-Ende mit *perfect forward secrecy* verschlüsselt, z.B. [Signal](https://www.signal.org/).
- Entscheide dich für eine stabile und aktiv gewartete Messaging-Plattform, die von seriösen Entwicklern unterstützt wird und über ein transparentes Einnahmemodell verfügt. Die Plattform sollte idealerweise in einem Land mit neutraler Gerichtsbarkeit ansässig sein und einer unabhängigen Sicherheitsprüfung unterzogen worden sein.
- Stelle sicher, dass die Geräte des Senders und Empfängers frei von Malware sind, verschlüsselt sind und mit einem starken Passwort geschützt sind.
- Deaktiviere Companion-Apps (z.B. Webversionen) und Cloud-Backups, um die Angriffsfläche zu reduzieren.
- Lösche Metadaten von Medien, bevor du sie verschickst, da diese Informationen über User, Geräte, Standort etc. enthalten können.
- Verifiziere die Identität der Empfänger, z.B. physisch oder durch Messenger-Funktionen, die dies unterstützen.
- Vermeide SMS. Wenn SMS genutzt werden müssen, verschlüssele diese.
- Nutze Apps, die selbstlöschende Nachrichten unterstützen und möglicherweise auch anonym verwendet werden können.

## Netzwerk

- Nutze einen vertrauenswürdigen VPN-Service, um deine IP zu schützen und die Daten, die dein Internetprovider speichern kann, zu minimieren. Verstehe aber auch die Limitierungen eines VPN-Services.
- Ändere das Standardpasswort deines Routers. Jeder, der im WLAN ist, kann den Netzwerkverkehr überwachen. Vermeide, dass Unbekannte dein Netzwerk nutzen, indem du WPA2-Verschlüsselung und ein starkes Passwort verwendest.
- Nutze einen sicheren DNS-Provider, z.B. [Cloudflare's 1.1.1.1](https://1.1.1.1/dns/), um Nutzer-Tracking zu reduzieren. Diese Einstellung kannst du im besten Fall im Router vornehmen oder auf jedem Gerät.

*Die ursprünglichen Inhalte stammen von [Alicia Sykes](https://aliciasykes.com) und sind hier zu finden: [personal-security-checklist](https://github.com/Lissy93/personal-security-checklist/). Diese Inhalte sind lizenziert unter der [Creative Commons, CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Bei der Erstellung dieses Blogartikels wurden die Inhalte angepasst und verändert.*
