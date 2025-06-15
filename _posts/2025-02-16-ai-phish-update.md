---
layout: single
title: "Weiterentwicklung des KI-gestützten Phishing-Analyse-Tools"
date:   2025-02-16 
categories: projekte
tags: ai phishing python email
excerpt: "Das Python Tool hat einige neuen Features und Verbesserungen erhalten."
toc: true
toc_sticky: true
header:
  overlay_image: assets/images/posts/ai-phish/joanna-kosinska-uGcDWKN91Fs-unsplash.jpg
  overlay_filter: 0.5 # same as adding an opacity of 0.5 to a black background
  caption:  "Foto von [Joanna Kosinska](https://unsplash.com/@joannakosinska?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash) auf [Unsplash](https://unsplash.com/photos/envelope-paper-lot-uGcDWKN91Fs?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash)"
---

Ich habe mein Tool zur automatisierten Phishing-Analyse von E-Mails erweitert und verbessert. Die neueste Version des Skripts ist nun auf [GitHub](https://github.com/fourframes/perplexity-phish-check) verfügbar.

## Neue Features und Verbesserungen

### Direkte Antwortfunktion mit Whitelisting

Ein wesentliches neues Feature ist die Möglichkeit, die Phishing-Evaluierung direkt als Antwort an den ursprünglichen Absender zu senden. Um die Sicherheit und Kontrolle über den Service zu gewährleisten, wurde ein Whitelisting-System implementiert:

- Nur E-Mails von definierten Adressen oder Domains werden verarbeitet.
- Dies verhindert unbefugten Zugriff und schützt vor möglichem Missbrauch des API-Kontingents.
- So erhalten Spammer beispielsweise keine Analyse ihrer E-Mails, was potenzielle Sicherheitsrisiken minimiert.

### Verbessertes Logging und Exception Handling

Um die Transparenz und Zuverlässigkeit des Skripts zu erhöhen, wurden folgende Verbesserungen vorgenommen:

- **Integriertes Logging**: Ermöglicht eine detaillierte Nachverfolgung der Skriptaktivitäten.
- **Verbessertes Exception Handling**: Erhöht die Robustheit des Skripts und erleichtert die Fehlerdiagnose.

## Weitere Informationen

Für detaillierte Informationen zur Einrichtung und Nutzung des Tools verweise ich auf das [GitHub-Repository](https://github.com/fourframes/perplexity-phish-check) und den ausführlichen [Projektbericht](https://fourframes.de/projekte/ai-phishing/).
