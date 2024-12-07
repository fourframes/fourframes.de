---
layout: single
title: "Cybersecurity Analyst Toolbox"
date:   2024-12-07 
categories: lernen
tags: ressourcen tools framework
excerpt: "Meine Cybersecurity Toolbox fokussiert auf Cyber Security Analyse"
header:
  overlay_image: assets\images\posts\toolbox\matt-artz-4mAcustUNPs-unsplash.jpg
  overlay_filter: 0.5 # same as adding an opacity of 0.5 to a black background
  caption:  "Foto von [Matt Artz](https://unsplash.com/de/@mattartz?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash) auf [Unsplash](https://unsplash.com/de/fotos/grauer-verstellbarer-schlussel-und-graue-rohrzange-4mAcustUNPs?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash)"
---

Im [Blogpost zu meinem Zwischenfazit des SOC Analyst Lernpfads](https://fourframes.de/lernen/soc-analyst-lernpfad-zwischenfazit/) habe ich bereits erwähnt, dass ich für die Vielzahl der erlernten Tools, Frameworks und Plattformen sowie ihre spezifischen Anwendungsfälle einen persönlichen Werkzeugkasten erstellen möchte.

## Die Idee hinter der Toolbox

In dieser Toolbox dokumentiere ich alle Werkzeuge, die ich kennengelernt habe, zusammen mit einer Kurzbeschreibung. Ursprünglich handelte es sich dabei nur um eine einfache Notiz in meiner Notiz-App. Doch schnell kam mir die Idee, diese Informationen auch der Community zugänglich zu machen. Meine Hoffnung ist, dass die Liste nicht nur mir, sondern auch anderen Menschen hilft, neue Tools zu entdecken, bekannte Werkzeuge besser zu verstehen und die Liste durch eigene Vorschläge zu erweitern.

Die aktuelle Version meiner Cybersecurity-Toolbox pflege ich in einem [GitHub-Repository](https://github.com/fourframes/cybersec-analyst-toolbox). Dort halte ich die Informationen in einer einfachen Markdown-Datei fest, um die Wartung und Erweiterung so unkompliziert wie möglich zu gestalten.

## Momentaufnahme der Toolbox

Hier ist eine Momentaufnahme der aktuellen Tools und Frameworks in meiner Liste, die ich auf Englisch pflege:

### Frameworks & Threat Intelligence

| Tool               | Website                                                         | Description                                                                                                             |
| ------------------ | --------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| Abuse              | <https://abuse.ch/>                                             | A platform focused on threat intelligence.                                                                              |
| DomainTools        | <https://whois.domaintools.com/>                                | Provides DNS and IP information on a domain.                                                                            |
| Talos Intelligence | <https://talosintelligence.com/>                                | A platform focused on threat intelligence provided by Cisco.                                                            |
| Censys             | <https://search.censys.io/>                                     | A search engine for discovering devices and services exposed on the internet, offering insights into vulnerabilities.   |
| Shodan             | <https://www.shodan.io/>                                        | A search engine that scans and indexes devices connected to the internet, used for identifying network vulnerabilities. |
| Mitre Attack       | <https://attack.mitre.org/>                                     | A comprehensive framework of adversarial tactics and techniques used by cyber attackers.                                |
| Mitre AEP          | <https://attack.mitre.org/resources/adversary-emulation-plans/> | Provides adversary emulation plans that simulate cyber threat actors to test and improve security defenses.             |
| Mitre CAR          | <https://car.mitre.org/>                                        | Cyber Analytics Repository that offers security analytics to help detect adversary behaviors on networks.               |
| Mitre D3fend       | <https://d3fend.mitre.org/>                                     | A knowledge base of cybersecurity countermeasures designed to help organizations protect against attacks.               |
| Mitre Engage       | <https://engage.mitre.org/>                                     | A framework designed to guide organizations in planning and executing cyber deception and engagement operations.        |
| LOKI               | <https://github.com/Neo23x0/Loki>                               | A simple scanner that checks for indicators of compromise (IoCs) using YARA rules and other heuristics.                 |
| THOR (Lite)        | <https://www.nextron-systems.com/thor-lite/>                    | A professional-grade forensic scanner that detects advanced threats and malicious activity.                             |
| Yara               | <https://virustotal.github.io/yara/>                            | A tool aimed at helping malware researchers identify and classify malware by writing flexible detection rules.          |
| FENRIR             | <https://github.com/Neo23x0/Fenrir>                             | A simple IOC scanner for Unix-based systems designed to be easily integrated into security incident response processes. |
| yarGen             | <https://github.com/Neo23x0/yarGen>                             | A tool for generating YARA rules by extracting relevant strings from malware samples.                                   |
| valhalla           | <https://valhalla.nextron-systems.com/>                         | A service offering a massive collection of curated YARA rules for detecting malware and threats.                        |
| YARAify            | <https://yaraify.abuse.ch/>                                     | Provides a feed of YARA rules and allows scanning of files against YARA rules-                                          |
| OpenCTI            | <https://www.opencti.io/>                                       | An open-source platform designed to manage, store, and share cyber threat intelligence information.                     |
| MISP               | <https://www.misp-project.org/>                                 | An open-source threat intelligence platform for sharing, storing, and correlating indicators of compromise.             |

### Network Security

| Tool         | Website                                       | Description                                                                                                                  |
| ------------ | --------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| Zenmap       | <https://nmap.org/zenmap/>                    | The official graphical user interface (GUI) for Nmap.                                                                        |
| Snort        | <https://www.snort.org/>                      | An open-source intrusion detection and prevention system (IDS/IPS).                                                          |
| NetworkMiner | <https://www.netresec.com/?page=NetworkMiner> | A network forensic analysis tool (NFAT) for extracting and analyzing data from network traffic.                              |
| Wireshark    | <https://www.wireshark.org/>                  | A network protocol analyzer used for network troubleshooting, analysis, and protocol development.                            |
| TShark       | <https://tshark.dev/>                         | The command-line version of Wireshark, offering similar functionalities for capturing and analyzing network traffic via CLI. |
| Brim         | <https://www.brimdata.io>                     | The graphical user interface (GUI) for Zeek.                                                                                 |

### Mails

| Tool       | Website                  | Description                                                                  |
| ---------- | ------------------------ | ---------------------------------------------------------------------------- |
| Phish Tool | <https://phishtool.com/> | A platform designed for detecting, analyzing, and managing phishing threats. |

## Mitmachen und Feedback geben

Ich freue mich über Korrekturen, Ergänzungen oder andere Hinweise zur Toolbox! Gemeinsam können wir die Liste verbessern und sie zu einer wertvollen Ressource für Cybersecurity-Interessierte machen. Egal ob du Tools hinzufügen, bestehende Beschreibungen präzisieren oder Tipps zu ihren Anwendungsfällen geben möchtest – jede Unterstützung ist willkommen.
