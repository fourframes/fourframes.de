---
layout: single
title: "Bounce-Mail Mystery"
date:   2025-06-15 
categories: projekt
tags: phish email
excerpt: "Wie eine ungewöhnliche Spam-E-Mail zur Cyber-Security-Analyse wurde."
toc: true
toc_sticky: true
header:
  overlay_image: assets/images/posts/bounce-mail/erica-steeves-G_lwAp0TF38-unsplash.jpg
  overlay_filter: 0.5 # same as adding an opacity of 0.5 to a black background
  caption:  "Foto von [erica steeves](https://unsplash.com/@ecees?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash) auf [Unsplash](https://unsplash.com/photos/person-showing-white-envelope-G_lwAp0TF38?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash)"
---

Vor Kurzem stieß ich im Spam-Ordner meines E-Mail-Postfachs auf eine sehr ungewöhnliche Nachricht. Da ich mich bereits länger mit der Analyse von Spam- und Phishing-E-Mails beschäftige und ein eigenes Tool zur Klassifikation von Phishing-E-Mails mittels KI entwickelt habe, war meine Neugier sofort geweckt. Einen Bericht zu diesem Projekt ist hier zu finden: <https://fourframes.de/projekte/ai-phishing/>

Bei der fraglichen E-Mail handelte es sich um eine sogenannte Bounce-E-Mail. Diese werden von Mailservern versendet, wenn eine Nachricht aus verschiedenen Gründen nicht zugestellt werden konnte – ähnlich wie bei einem zurückgesendeten Brief mit einem Hinweis zum Zustellungsproblem. Je intensiver ich diesen Fall analysierte, desto komplexer erschien er mir. Zum Schutz der beteiligten Akteure und aus Gründen der Datensparsamkeit folgt zunächst eine Übersicht der wichtigsten Beteiligten:

- `myDomain`: Eine von mir verwaltete Domain.
- `myMailServer`: Der Mailserver dieser Domain.
- `unknownDomain`: Eine mir bis zur Analyse unbekannte, aber legitime Website.
- `subdomain.unknownDomain`: Eine Subdomain der oben genannten unbekannten Domain.
- `unknownMailServer`: Der Mailserver dessen IP, die auf `unknownDomain` als auch `subdomain.unknownDomain` auflöst.
- `recipientMailAddress`: Eine mir unbekannte E-Mail-Adresse.
- `recipientMailServer`: Der Server, der diese E-Mail-Adresse verwaltet.

## Der Auslöser: Die Bounce-E-Mail

Der Anstoß zur Analyse war eine Bounce-E-Mail, die vom `unknownMailServer` an ein nicht existierendes Postfach auf `myDomain` gesendet wurde. Das Postfach konnte die Nachricht nur aufgrund einer Catch-All-Regel empfangen. Dies ist bereits ein erstes Indiz für Spam oder Phishing, da Catch-All-Mechanismen häufig für Massenmails genutzt werden – Angreifer können so beliebige Adressen einer Domain verwenden und erhalten dennoch Zustellung.

Die Bounce-E-Mail gab an, dass eine Nachricht von einem angeblichen Postfach auf `myDomain` nicht an `recipientMailAddress` zugestellt werden konnte, weil die IP des `unknownMailServer` beim `recipientMailServer` aufgrund eines hohen E-Mail-Volumens blockiert war. Dieser Grund spielte im weiteren Verlauf der Analyse eine interessante Rolle. Die ursprünglichen Anhänge der E-Mail – eine .html-, eine .swf- und eine .mp4-Datei – waren ebenfalls Bestandteil der Bounce-E-Mail.

Zunächst lag der Verdacht nahe, dass jemand – möglicherweise mit Hilfe eines LLM – eine Bounce-E-Mail gefälscht hatte, um den Empfänger zum Öffnen der Anhänge zu verleiten. Das Postfach auf `myDomain` könnte einfach geraten und die Catch-All-Konfiguration ausgenutzt worden sein, um einen Administrator zu phishen.

Allerdings war der angegebene Bounce-Grund ungewöhnlich. Wer eine Bounce-E-Mail fälschen möchte, würde vermutlich einen „Empfänger unbekannt“-Fehler vortäuschen, nicht einen Grund wie „zu hohes Mail-Volumen“. Ein solcher Grund würde bei Administratoren eher Misstrauen wecken. Aus diesem Grund wurde der Mail-Header der Bounce-E-Mail genauer analysiert.

## Der Header der Bounce-E-Mail

Die Analyse des Headers war schnell abgeschlossen. Die Nachricht landete im Spam-Ordner, weil Sicherheitsmechanismen wie SPF, DKIM und DMARC fehlgeschlagen waren und `myMailServer` die E-Mail deshalb als Spam markierte. Zuvor lief die Nachricht über den `unknownMailServer` und wurde von einem lokalen Client (lokale IP) versendet. Damit schwächte sich der Verdacht auf eine gefälschte Bounce-E-Mail etwas ab: Es könnte sich tatsächlich um eine echte Bounce-E-Mail handeln, bei der auch der angegebene Grund des Rate-Limitings zutrifft. Um dies zu klären, wurde die Analyse vertieft.

## Der `unknownMailServer`

Im nächsten Schritt wurde untersucht, welcher Mailserver die Bounce-E-Mail versendet hatte. Der `unknownMailServer` enthielt in der URL die Adresse von `subdomain.unknownDomain`. Eine Recherche ergab, dass `unknownDomain` eine legitime, in Deutschland gehostete Website ist, die bestimmte Produkte bewirbt und verkauft. Die Website befand sich laut Recherche in der „Startup“-Phase, war aber nicht gänzlich unbekannt. Es gab keine Hinweise darauf, dass die Infrastruktur oder der Shop gefälscht ist.

Die Sicherheitsmerkmale SPF, DKIM und DMARC waren für die Hauptdomain korrekt gesetzt und zeigten keine Auffälligkeiten. Allerdings werden diese Mechanismen nicht automatisch an Subdomains vererbt. Da der `unknownMailServer` auf `subdomain.unknownDomain` verwies, waren SPF, DKIM und DMARC für diese Subdomain nicht konfiguriert. Vermutlich wurde die Bounce-E-Mail deshalb als Spam markiert.

Beim direkten Aufruf von `subdomain.unknownDomain` im Browser landete man auf einer Login-Seite, die ausschließlich über HTTP und nicht über HTTPS erreichbar war. Dies verstärkte den Verdacht, dass auf der Subdomain ein Service – inklusive Mailserver – gehostet wurde, der nicht ausreichend konfiguriert und abgesichert war. Laut Talos Intelligence war das E-Mail-Volumen von `unknownMailServer` in den letzten Tagen ungewöhnlich angestiegen, was diese Theorie zusätzlich stützt.

## Das Zwischenfazit

[![Flow der Emails](/assets/images/posts/bounce-mail/diagram.png)](/assets/images/posts/bounce-mail/diagram.png)

Obwohl der Fall nicht vollständig aufgeklärt wurde, erscheint folgende Erklärung am plausibelsten:

- Auf `subdomain.unknownDomain` wurde durch den Betreiber ein Service gehostet, der einen Mailserver bereitstellt. Dieser war jedoch nicht ausreichend abgesichert.
- Angreifer nutzten diese Fehlkonfiguration, um im Namen fremder Domains Spam-Mails zu versenden (Domain Spoofing).
- Aufgrund der hohen Anzahl an E-Mails wurde die IP des `unknownMailServer` beim `recipientMailServer` gesperrt.
- Infolge der Sperrung erfolgte eine Bounce-E-Mail, die durch die Catch-All-Regel an die gespoofte Absenderadresse auf `myDomain` zugestellt wurde.

Es ist jedoch wichtig zu betonen, dass auch andere Erklärungen möglich sind:

- Der `unknownMailServer` wurde ausschließlich genutzt, um Bounce-Mail-Spam zu versenden, und die Inhalte der Bounce-E-Mail sind vollständig gefälscht.
- Der Fall enthält gefälschte Header in der Bounce-E-Mail und müsste anders interpretiert werden.

## Die Anhänge

Wie bereits erwähnt, enthielt die Bounce-E-Mail die Anhänge der ursprünglichen Nachricht, die der Angreifer über den `unknownMailServer` an den `recipientMailServer` gesendet hatte. Erwartungsgemäß wurde zunächst vermutet, dass es sich um Malware handelt. Die Analyse der drei Anhänge ergab jedoch, dass die .html-Datei tatsächlich eine HTML-Seite war. Auch die .swf- und .mp4-Dateien waren lediglich HTML-Dateien mit entsprechenden Dateiendungen. In den Dateien fanden sich keine Skripte, sondern ausschließlich HTML-Inhalt. Eine Übersetzung der Texte deutete darauf hin, dass es sich um Gedichte oder Kurzgeschichten handelte. Dies könnte darauf hindeuten, dass getestet wurde, welche Dateiendungen über den Mailserver versendet werden können.
