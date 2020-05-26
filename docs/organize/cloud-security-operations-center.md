---
title: Cloud-SOC-Funktionen
description: Informationen zum Verständnis von Cloud-SOC-Funktionen (Security Operations Center).
author: JanetCThomas
ms.author: janet
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.topic: conceptual
ms.date: 04/30/2020
ms.openlocfilehash: c966129e01d9cf97af0ac1db0a8ac7bec8efb751
ms.sourcegitcommit: 5d6a7610e556f7b8ca69960ba76a3adfa9203ded
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/14/2020
ms.locfileid: "83401130"
---
<!-- cSpell:ignore CISO MTTA MTTR SIEM NIST SOCs CDOC -->

# <a name="cloud-soc-functions"></a>Cloud-SOC-Funktionen

Das Hauptziel eines Cloud Security Operations Centers (SOC) besteht darin, aktive Angriffe auf Unternehmensressourcen zu erkennen, darauf zu reagieren und diese zu beheben.

Mit zunehmender Reife des SOCs sollten Sicherheitsvorgänge Folgendes leisten:

- Reaktives Reagieren auf von Tools erkannte Angriffe
- Proaktives Suchen nach Angriffen, die der reaktiven Erkennung entgangen sind

## <a name="modernization"></a>Modernisierung

Das Erkennen von Bedrohungen und die Reaktion darauf wird zurzeit einer bedeutenden Modernisierung auf allen Ebenen unterzogen.

- **Aufwertung zum Geschäftsrisikomanagement:** SOC wächst sich zu einer zentralen Komponente des Managements von Geschäftsrisiken für die Organisation aus.
- **Metriken und Ziele:** Die Nachverfolgung der Effektivität des SOC entwickelt sich von der „Erkennungsgeschwindigkeit“ zu diesen Schlüsselindikatoren weiter:
  - *Reaktionsfähigkeit* über die durchschnittliche Bestätigungszeit (MTTA)
  - *Korrekturgeschwindigkeit* über die durchschnittliche Korrekturzeit (MTTR)
- **Technologieentwicklung:** Die SOC-Technologie entwickelt sich von der exklusiven Verwendung statischer Analysen von Protokollen in einem SIEM-Tool hin zur zusätzlichen Verwendung spezieller Tools und komplexer Analysetechniken. Dies bietet umfassende Erkenntnisse zu Ressourcen, die hochwertige Warnungen sowie eine Untersuchungserfahrung bereitstellen, die die breite Ansicht des SIEM-Tools ergänzen. Beide Tooltypen verwenden zunehmend KI/Maschinelles Lernen (Machine Learning), Verhaltensanalysen und integrierte Threat Intelligence (TI), um ungewöhnliche Aktionen zu erkennen und zu priorisieren, bei denen es sich um einen böswilligen Angreifer handeln könnte.
- **Bedrohungssuche:** SOCs fügen hypothesengestützte Bedrohungssuchen hinzu, um komplexe Angreifer proaktiv zu identifizieren und störende Fehlalarme aus den Warteschlangen der Analytiker an vorderster Front zu entfernen.
- **Incident Management:** Disziplin wird so formalisiert, dass nicht technische Elemente von Vorfällen mit juristischen, Kommunikations- und anderen Teams koordiniert werden.
**Integration von internem Kontext:** Um bei der Priorisierung von SOC-Aktivitäten zu helfen, wie relative Risikobewertungen von Benutzerkonten und Geräten, Vertraulichkeit von Daten und Anwendungen sowie wichtige Grenzen der Sicherheitsisolation, um eine enge Verteidigung zu gewährleisten.

 Weitere Informationen finden Sie unter

- [Standards für Strategie und Architektur: Sicherheitsvorgänge](https://docs.microsoft.com/security/compass/security-operations-videos-and-decks)
- [CISO-Workshop-Modul 4b: Bedrohungsschutzstrategie](https://docs.microsoft.com/security/ciso-workshop/ciso-workshop-module-4b)
- Blogreihe des Cyber Defense Operations Center (CDOC)[Teil 1](https://www.microsoft.com/security/blog/2019/02/21/lessons-learned-from-the-microsoft-soc-part-1-organization/), [Teil 2a](https://www.microsoft.com/security/blog/2019/04/23/lessons-learned-microsoft-soc-part-2-organizing-people/), [Teil 2b](https://www.microsoft.com/security/blog/2019/06/06/lessons-learned-from-the-microsoft-soc-part-2b-career-paths-and-readiness/), [Teil 3a](https://www.microsoft.com/security/blog/2019/10/07/ciso-series-lessons-learned-from-the-microsoft-soc-part-3a-choosing-soc-tools/), [Teil 3b](https://www.microsoft.com/security/blog/2019/12/23/ciso-series-lessons-learned-from-the-microsoft-soc-part-3b-a-day-in-the-life)
- [NIST-Leitfaden für den Umgang mit Computersicherheitsvorfällen](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-61r2.pdf) (NIST Computer Security Incident Handling Guide)
- [NIST-Leitfaden für die Wiederherstellung von Cybersicherheitsereignissen](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-184.pdf) (NIST Guide for Cybersecurity Event Recovery)

## <a name="team-composition-and-key-relationships"></a>Teamzusammensetzung und wichtige Beziehungen

Das Cloud Security Operations Center besteht im Allgemeinen aus den folgenden Typen von Rollen.

- IT-Betrieb (enger, regelmäßiger Kontakt)
- Bedrohungsanalyse
- Sicherheitsarchitektur
- Insider-Risiko-Programm
- Juristisches und Personalverwaltung
- Kommunikationsteams
- Risikoorganisation (falls vorhanden)
- Branchenspezifische Vereinigungen, Communitys und Lieferanten (vor Auftreten eines Vorfalls)

## <a name="next-steps"></a>Nächste Schritte

Informieren Sie sich über die Funkt der [Sicherheitsarchitektur](./cloud-security-architecture.md).
