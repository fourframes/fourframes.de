---
layout: single
title: "Projektbericht: AI-gestützte Phishing-Analyse mit Perplexity"
date:   2024-11-16 
categories: projekte
tags: phishing ai python email
excerpt: "Die Perplexity API nutzen um eine Einschätzung zum Phishing-Status einer Mail zu erhalten."
toc: true
toc_sticky: true
header:
  overlay_image: /assets/images/posts/ai-phish/stephen-phillips-hostreviews-co-uk-F8QgtxUc6-E-unsplash.jpg
  overlay_filter: 0.5 # same as adding an opacity of 0.5 to a black background
  caption:  "Foto von [Stephen Phillips](https://unsplash.com/@hostreviews?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash) auf [Unsplash](https://unsplash.com/photos/mail-icon-F8QgtxUc6-E?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash)"
---

In diesem Projektbericht teile ich meine Erfahrungen bei der Entwicklung eines Tools zur automatisierten Phishing-Analyse von E-Mails. Grundlage dafür ist die Nutzung der API der KI-gestützten Suchmaschine [Perplexity](https://www.perplexity.ai/), die präzise Antworten liefert, indem sie das Internet in Echtzeit durchsucht und ihre Quellen transparent darstellt.

## Inspiration durch Perplexity

Bereits nach wenigen Suchanfragen hat mich Perplexity mit seinen Fähigkeiten überzeugt. Besonders interessant fand ich die Möglichkeit, die Suchmaschine über eine API in eigene Projekte zu integrieren. Da ich meine Python-Kenntnisse vertiefen wollte, bot sich hier die perfekte Gelegenheit für mein Vorhaben.

## Die Idee

Mir hilft es, beim Lernen neuer Fähigkeiten ein klares Ziel vor Augen zu haben. Als ich die Perplexity-Suchmaschine fragte, welches Projekt ich umsetzen könnte, schlug sie eine AI-gestützte E-Mail-Phishing-Analyse vor. Die Idee überzeugte mich: Ein Python-Skript sollte regelmäßig ein bestimmtes Postfach überwachen, neue E-Mails analysieren und die Ergebnisse an eine vorab definierte E-Mail-Adresse senden. Nutzer könnten so verdächtige E-Mails an dieses Postfach weiterleiten und binnen kürzester Zeit eine Einschätzung erhalten.

## Der Mailempfang

Anstatt das gesamte Skript von der KI erstellen zu lassen, entschied ich mich, selbst zu programmieren und nur spezifische Fragen oder Hürden durch Perplexity klären zu lassen. So fand ich heraus, dass die `imaplib` in Python alle notwendigen Funktionen bietet, um E-Mails zu verarbeiten.

Um das Risiko unbeabsichtigter Zugriffe zu minimieren, richtete ich ein separates Postfach ein, das ausschließlich für diesen Service genutzt wird. Das Skript überwacht das Postfach und reiht ungelesene Mails zur weiteren Verarbeitung ein.

## Die Analyse: Evaluierung der E-Mails

Die API von Perplexity bietet in der Dokumentation einige Beispiele, wie Anfragen strukturiert werden können. Neben dem eigentlichen Text der Anfrage kann ein **Kontext** übermittelt werden, der die Antwort fokussiert. Für meine Analyse nutze ich folgende Daten aus einer eingehenden E-Mail:

- **Betreff**
- **Inhalt der E-Mail**
- **Ein definierter Kontext**, der Perplexity dazu auffordert, die Wahrscheinlichkeit eines Phishing-Versuchs einzuschätzen und darauf hinweist, dass es sich um eine weitergeleitete E-Mail handelt.

Das KI-Modell analysiert die Anfrage und liefert eine Bewertung zurück, die als Grundlage für die weitere Verarbeitung dient.

## Verarbeitung der Antworten

Die von Perplexity generierte Antwort wird zusammen mit der ursprünglichen E-Mail an eine festgelegte E-Mail-Adresse weitergeleitet. Ursprünglich plante ich, die Ergebnisse direkt an den Absender der weitergeleiteten E-Mail zu senden. Aus Sicherheitsgründen habe ich mich jedoch dagegen entschieden, da dies eine potenziell unkontrollierte Nutzung des Services ermöglichen würde.

## Betrieb des Tools

Eine praktische Möglichkeit, das Skript regelmäßig auszuführen, ist die Verwendung eines *Raspberry Pi*. Diese kostengünstige Hardware eignet sich hervorragend als ständig laufendes Gerät. Nach der Konfiguration der erforderlichen Parameter über Umgebungsvariablen kann das Skript als *Cron-Job* eingerichtet werden, der in festgelegten Abständen ausgeführt wird.

## Live-Test und Ergebnisse

Um das Tool zu testen, habe ich eine potenziell verdächtige E-Mail an das überwachte Postfach weitergeleitet. Die Analyse ergab folgende Bewertung durch die KI:

**Original-E-Mail:**  
[![Die ursprüngliche Mail die analysiert wurde](/assets/images/posts/ai-phish/mail.png)](/assets/images/posts/ai-phish/mail.png)

**Ergebnis der AI:**  
[![Die Einschätzung zum Phishing-Status von Perplexity](/assets/images/posts/ai-phish/response2.png)](/assets/images/posts/ai-phish/response2.png)

## Potenzielle Erweiterungen

Da jede API-Anfrage Kosten verursacht, möchte ich den Zugriff in Zukunft über eine **Whitelist** reglementieren. Nur E-Mails von genehmigten Absendern oder Domains sollen verarbeitet werden. Nach der Implementierung könnte das Skript so erweitert werden, dass die Analyseergebnisse direkt an den ursprünglichen Absender der E-Mail zurückgesendet werden, sofern dieser auf der Whitelist steht.

## Verfügbarkeit und Weiterentwicklung

Das Skript steht auf [GitHub](https://github.com/fourframes/perplexity-phish-check) zur freien Nutzung und Erweiterung bereit. Ich freue mich über Feedback und Vorschläge zur Verbesserung der Funktionalität. In einem zukünftigen Blogpost werde ich detailliert darauf eingehen, wie das Tool betrieben werden kann.
