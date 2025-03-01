---
layout: single
title: "Update: Cybersecurity Analyst Toolbox"
date:   2025-03-01 
categories: lernen
tags: ressourcen tools framework
excerpt: "Erweiterung nach Abschluss des SOC Analyst Lernpfad"
toc: true
toc_sticky: true
classes: wide
header:
  overlay_image: assets/images/posts/toolbox/dan-cristian-padure-noOXRT9gfQ8-unsplash.jpg
  overlay_filter: 0.5 # same as adding an opacity of 0.5 to a black background
  caption:  "Foto von [Dan Cristian Pădureț](https://unsplash.com/@dancristianpaduret?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash) auf [Unsplash](https://unsplash.com/photos/assorted-color-plastic-tools-on-gray-wooden-table-noOXRT9gfQ8?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash)"
---
Ich habe vor kurzem den SOC Analyst Lernpfad auf TryHackMe abgeschlossen. Dies habe ich als Anlass genommen meine Cybersecurity Analyst Toolbox zu erweitern und zu optimieren.

## Hintergrund

In meinem [initialen Blogartikel zur Security Toolbox](https://fourframes.de/lernen/analyst-toolbox/) habe ich die Gründe für die Pflege dieser Ressource ausführlich dargelegt. Die Toolbox dient als zentraler Referenzpunkt für effektive und aktuelle Tools im Bereich Cybersecurity Analysis.

## Aktualisierte Toolbox

Die aktualisierte Version der Cybersecurity Analyst Toolbox ist nun auf [GitHub](https://github.com/fourframes/cybersec-analyst-toolbox) verfügbar. Die wichtigsten Änderungen umfassen:

1. **Neue Toolkategorien**: Die Liste wurde um spezifische Bereiche erweitert, die für SOC-Analysten besonders relevant sind.
2. **Erweiterte Toolauswahl**: Basierend auf den Erkenntnissen aus dem TryHackMe-Kurs wurden neue, praxiserprobte Tools hinzugefügt.
3. **Verbesserte Struktur**: Die Toolbox wurde neu gegliedert, um eine intuitivere Navigation und schnelleren Zugriff auf relevante Tools zu ermöglichen.

## Community-Beitrag und Feedback

Die Cybersecurity-Community lebt vom Austausch und der gegenseitigen Unterstützung. Daher lade ich alle Interessierten herzlich ein, zur Weiterentwicklung der Toolbox beizutragen:

- **GitHub-Funktionen nutzen**: Issues oder Pull Request ermöglichen es Verbesserungsvorschläge oder neue Tools einzubringen.
- **Direkter Kontakt**: Für ausführlicheres Feedback oder Diskussionen:  [blog@fourframes.de](mailto:blog@fourframes.de).

## Aktueller Stand der Liste:

## Frameworks & Threat Intelligence

| Tool                | Website                                                         | Description                                                                                                             |
| ------------------- | --------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| Abuse               | <https://abuse.ch/>                                             | A platform focused on threat intelligence.                                                                              |
| DomainTools         | <https://whois.domaintools.com/>                                | Provides DNS and IP information on a domain.                                                                            |
| Talos Intelligence  | <https://talosintelligence.com/>                                | A platform focused on threat intelligence provided by Cisco.                                                            |
| Censys              | <https://search.censys.io/>                                     | A search engine for discovering devices and services exposed on the internet, offering insights into vulnerabilities.   |
| Shodan              | <https://www.shodan.io/>                                        | A search engine that scans and indexes devices connected to the internet, used for identifying network vulnerabilities. |
| Mitre Attack        | <https://attack.mitre.org/>                                     | A comprehensive framework of adversarial tactics and techniques used by cyber attackers.                                |
| Mitre AEP           | <https://attack.mitre.org/resources/adversary-emulation-plans/> | Provides adversary emulation plans that simulate cyber threat actors to test and improve security defenses.             |
| Mitre CAR           | <https://car.mitre.org/>                                        | Cyber Analytics Repository that offers security analytics to help detect adversary behaviors on networks.               |
| Mitre D3fend        | <https://d3fend.mitre.org/>                                     | A knowledge base of cybersecurity countermeasures designed to help organizations protect against attacks.               |
| Mitre Engage        | <https://engage.mitre.org/>                                     | A framework designed to guide organizations in planning and executing cyber deception and engagement operations.        |
| LOKI                | <https://github.com/Neo23x0/Loki>                               | A simple scanner that checks for indicators of compromise (IoCs) using YARA rules and other heuristics.                 |
| THOR (Lite)         | <https://www.nextron-systems.com/thor-lite/>                    | A professional-grade forensic scanner that detects advanced threats and malicious activity.                             |
| Yara                | <https://virustotal.github.io/yara/>                            | A tool aimed at helping malware researchers identify and classify malware by writing flexible detection rules.          |
| FENRIR              | <https://github.com/Neo23x0/Fenrir>                             | A simple IOC scanner for Unix-based systems designed to be easily integrated into security incident response processes. |
| yarGen              | <https://github.com/Neo23x0/yarGen>                             | A tool for generating YARA rules by extracting relevant strings from malware samples.                                   |
| valhalla            | <https://valhalla.nextron-systems.com/>                         | A service offering a massive collection of curated YARA rules for detecting malware and threats.                        |
| YARAify             | <https://yaraify.abuse.ch/>                                     | Provides a feed of YARA rules and allows scanning of files against YARA rules-                                          |
| OpenCTI             | <https://www.opencti.io/>                                       | An open-source platform designed to manage, store, and share cyber threat intelligence information.                     |
| MISP                | <https://www.misp-project.org/>                                 | An open-source threat intelligence platform for sharing, storing, and correlating indicators of compromise.             |
| *IPinfo.io*         | <https://ipinfo.io/>                                            | Provides geolocation, ownership details, and privacy detection for IP addresses.                                        |
| *URLScan.io*        | <https://urlscan.io/>                                           | A web sandbox that scans and analyzes URLs for threats, generating detailed reports.                                    |
| *DomainTools Whois* | <https://whois.domaintools.com/>                                | Retrieves domain registration details, including ownership, creation date, and DNS information.                         |
| *VirusTotal*        | <https://www.virustotal.com/gui/>                               | Analyzes suspicious files and URLs to detect malware and shares findings with the security community.                   |

## Network Security

| Tool         | Website                                       | Description                                                                                                                  |
| ------------ | --------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| Zenmap       | <https://nmap.org/zenmap/>                    | The official graphical user interface (GUI) for Nmap.                                                                        |
| Snort        | <https://www.snort.org/>                      | An open-source intrusion detection and prevention system (IDS/IPS).                                                          |
| NetworkMiner | <https://www.netresec.com/?page=NetworkMiner> | A network forensic analysis tool (NFAT) for extracting and analyzing data from network traffic.                              |
| Wireshark    | <https://www.wireshark.org/>                  | A network protocol analyzer used for network troubleshooting, analysis, and protocol development.                            |
| TShark       | <https://tshark.dev/>                         | The command-line version of Wireshark, offering similar functionalities for capturing and analyzing network traffic via CLI. |
| Brim         | <https://www.brimdata.io>                     | The graphical user interface (GUI) for Zeek.                                                                                 |

## Endpoint Security & SIEM

| Tool               | Website                                                                                     | Description                                                                                                  |
| ------------------ | ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| *TCPView*          | <https://learn.microsoft.com/en-us/sysinternals/downloads/tcpview>                          | Displays active TCP and UDP connections, including process ownership and connection states.                  |
| *Process Explorer* | <https://learn.microsoft.com/en-us/sysinternals/downloads/process-explorer>                 | Provides detailed information about running processes.                                                       |
| *Wevtutil.exe*     | <https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/wevtutil> | Command-line tool for managing Windows Event Logs, including querying, exporting, and clearing logs.         |
| *Sysmon*           | <https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon>                           | Monitors and logs detailed system activity to Windows Event Logs for security analysis.                      |
| *Osquery*          | <https://www.osquery.io>                                                                    | Uses SQL-like queries to collect and analyze operating system data for monitoring, compliance, and security. |
| *Wazuh*            | <https://wazuh.com/>                                                                        | A free SIEM platform for threat detection, compliance, and IT security monitoring.                           |
| *Process Hacker*   | <https://processhacker.sourceforge.io/>                                                     | Open-source tool for monitoring processes, detecting malicious activity, and troubleshooting.                |
| *Autoruns*         | <https://learn.microsoft.com/en-us/sysinternals/downloads/autoruns>                         | Shows programs configured to run at system startup or login in detail.                                       |
| *Procdump*         | <https://learn.microsoft.com/en-us/sysinternals/downloads/procdump>                         | Captures process dumps during CPU spikes or application crashes for debugging purposes.                      |
| *Splunk*           | <https://www.splunk.com/>                                                                   | A platform for collecting, indexing, and analyzing machine-generated data in real-time.                      |

## DFIR

| Tool                            | Website                                                                                                                  | Description                                                                                                  |
| ------------------------------- | ------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------ |
| *FTK Imager*                    | <https://www.exterro.com/digital-forensics-software/ftk-imager>                                                          | A forensic imaging tool used to preview, image, and analyze digital evidence.                                |
| *RegRipper*                     | <https://github.com/keydet89/RegRipper3.0>                                                                               | Extracts and analyzes Windows registry data using plugins for incident response and forensics.               |
| *Zimmerman's Registry Explorer* | <https://ericzimmerman.github.io/>                                                                                       | Parses and analyzes Windows registry hives for forensic artifacts.                                           |
| *ShellBagExplorer*              | <https://ericzimmerman.github.io/>                                                                                       | Analyzes ShellBag registry data to track folder access and browsing history.                                 |
| *Registry Viewer*               | <https://ericzimmerman.github.io/>                                                                                       | Examines Windows registry files for forensic analysis of keys, values, and settings.                         |
| *Autopsy*                       | <https://www.autopsy.com>                                                                                                | Open-source digital forensics platform for investigating and analyzing hard drives and files.                |
| *Redline*                       | <https://fireeye.market/apps/211364>                                                                                     | Provides host investigative capabilities to detect malicious activity through memory and file analysis.      |
| *KAPE*                          | <https://www.kroll.com/en/services/cyber-risk/incident-response-litigation-support/kroll-artifact-parser-extractor-kape> | Collects and processes forensic artifacts efficiently during investigations.                                 |
| *Volatility*                    | <https://github.com/volatilityfoundation/volatility>                                                                     | An open-source memory forensics framework for analyzing RAM dumps.                                           |
| *Velociraptor*                  | <https://docs.velociraptor.app/>                                                                                         | Endpoint monitoring and digital forensics tool.                                                              |
| *The Hive*                      | <https://github.com/TheHive-Project/TheHive>                                                                             | An open-source incident response platform for managing security events collaboratively.                      |
| *PE Tree*                       | <https://github.com/blackberry/pe_tree>                                                                                  | Visualizes Portable Executable (PE) files to aid malware analysis.                                           |
| *Olevba*                        | <https://github.com/decalage2/oletools/wiki/olevba>                                                                      | Analyzes Microsoft Office documents to detect and extract malicious VBA macros and indicators of compromise. |

## Sandboxes

| Tool              | Website                                              | Description                                                                                        |
| ----------------- | ---------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| *Cuckoo Sandbox*  | <https://cuckoosandbox.org/>                         | Open-source automated malware analysis system for dynamic analysis of suspicious files and URLs.   |
| *CAPE Sandbox*    | <https://capev2.readthedocs.io/en/latest/index.html> | Malware analysis sandbox focused on unpacking and analyzing malicious payloads and executables.    |
| *Any.run*         | <https://any.run/>                                   | Interactive online malware sandbox allowing real-time analysis of suspicious files and activities. |
| *Hybrid Analysis* | <https://www.hybrid-analysis.com/>                   | Free malware analysis service powered by Falcon Sandbox for static and dynamic threat analysis.    |

## Phishing & Mails

| Tool                      | Website                                                                                                       | Description                                                                                           |
| ------------------------- | ------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| *Phish Tool*              | <https://phishtool.com/>                                                                                      | A platform designed for detecting, analyzing, and managing phishing threats.                          |
| *Message Header Analyzer* | <https://mha.azurewebsites.net/>                                                                              | Parses and analyzes email headers to trace the path of messages and identify potential issues.        |
| *Mail Header Analyzer*    | <https://mailheader.org/>                                                                                     | Makes email headers legible by parsing records for detailed analysis of message routing.              |
| *MXToolbox*               | <https://mxtoolbox.com/>                                                                                      | Provides tools to analyze DNS, MX records, and email server configurations for troubleshooting.       |
| *PhishTank*               | <https://phishtank.com/>                                                                                      | Community-driven platform to track, verify, and share information about phishing websites.            |
| *Spamhaus*                | <https://www.spamhaus.org/>                                                                                   | Offers IP and domain reputation services to detect and block spam, malware, and other threats.        |
| *Google Messageheader*    | <https://toolbox.googleapps.com/apps/messageheader/>                                                          | Analyzes email headers to identify delivery delays, their sources, and responsible parties.           |
| *Phishing IR Playbook*    | <https://github.com/counteractive/incident-response-plan-template/blob/master/playbooks/playbook-phishing.md> | A comprehensive playbook for investigating, remediating, and communicating during phishing incidents. |

## Miscellaneous

| Tool            | Website                           | Description                                                                                             |
| --------------- | --------------------------------- | ------------------------------------------------------------------------------------------------------- |
| *URL2PNG*       | <https://www.url2png.com/>        | Captures snapshots of websites through an intuitive API for integration into apps or workflows.         |
| *Wannabrowser*  | <https://www.wannabrowser.net/>   | Allows viewing HTML source code of websites using different user-agent perspectives to detect cloaking. |
| *CVE Crowd*     | <https://cvecrowd.com/>           | A platform for discussing and sharing information about CVEs and vulnerabilities.                       |
| *Fedisec Feeds* | <https://fedisecfeeds.github.io/> | Aggregates security-related data, including CVE updates, in JSON format for easy access.                |
