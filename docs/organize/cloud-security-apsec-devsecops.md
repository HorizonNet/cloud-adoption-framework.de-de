---
title: Grundlegendes zu Anwendungssicherheit und DevSecOps-Funktionen
description: Grundlegendes zu Anwendungssicherheit und DevSecOps-Funktionen.
author: JanetCThomas
ms.author: janet
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.topic: conceptual
ms.date: 05/15/2020
ms.openlocfilehash: 3211c0a923d292b15b67ffd6734b97261307a199
ms.sourcegitcommit: 9a84c2dfa4c3859fd7d5b1e06bbb8549ff6967fa
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/21/2020
ms.locfileid: "83755531"
---
# <a name="application-security-and-devsecops-functions"></a>Anwendungssicherheit und DevSecOps-Funktionen

Das Ziel von Anwendungssicherheit und DevSecOps besteht darin, Sicherheitsgarantien in Entwicklungsprozesse und benutzerdefinierte branchenspezifische Anwendungen (Line of Business, LOB) zu integrieren.

## <a name="modernization"></a>Modernisierung

Die Anwendungsentwicklung wird schnell in mehreren Aspekten gleichzeitig neu strukturiert, darunter das DevOps-Teammodell, der schnelle Freigaberhythmus von DevOps und die technische Zusammensetzung von Anwendungen über Clouddienste und APIs. Weitere Informationen zu diesen Änderungen finden Sie unter „Ändern der Sicherheitsbeziehungen und Zuständigkeiten durch die Cloud“.

Diese Modernisierung von veralteten Entwicklungsmodellen bietet sowohl Gelegenheit als auch Erfordernis zur Modernisierung der Sicherheit von Anwendungen und Entwicklungsprozessen. Die Fusion der Sicherheit in DevOps-Prozesse wird häufig als DevSecOps bezeichnet und treibt Änderungen an, einschließlich:

<!-- TODO: Link needed below? -->
- **Sicherheit ist integriert, nicht außerhalb der Genehmigung:** Die schnelle Geschwindigkeit von Änderungen bei der Anwendungsentwicklung bewirkt, dass klassische Ansätze mit „Überprüfen und Melden“ auf Sichtweite überflüssig werden. Diese älteren Ansätze sind nicht in der Lage, mit Releases Schritt zu halten, ohne die Entwicklung zu blockieren und Verzögerungen bei der Markteinführung, Unterauslastung von Entwicklern und Zunahme des Backlogs bei Problemen zu verursachen.
  - **Verschiebung nach links**, um die Sicherheit früher in Anwendungsentwicklungsprozesse einzubeziehen, da frühzeitiges Beheben von Problemen billiger, schneller und effektiver ist. Wenn Sie warten, bis das Kind in den Brunnen gefallen ist, ist es schwieriger, es wieder herauszuholen.
  - **Native Integration:** Sicherheitspraktiken müssen nahtlos integriert werden, um nachteilige Reibung in Entwicklungsworkflows und Continuous Integration/Continuous Deployment-Prozessen (CI/CD) zu vermeiden. Informationen dazu, welche Ansätze GitHub hierbei verfolgt, finden Sie unter [Sichern von Software – gemeinsam](https://github.blog/2019-09-18-securing-software-together/).
  - **Sicherheit von hoher Qualität:** Sicherheit muss qualitativ hochwertige Ergebnisse und Anleitungen bereitstellen, die es Entwicklern ermöglichen, Probleme schnell zu beheben, und die keine Entwicklerzeit mit falsch positiven Ergebnissen verschwenden.
  - **Vereinigte Kultur:** Sicherheits-, Entwicklungs- und Betriebsrollen sollten wichtige Elemente in einer gemeinsamen Kultur, geteilten Werten und Zielen sowie Zuständigkeiten einbringen.
- **Agile-Sicherheit:** Die Verlagerung der Sicherheit von der Ansicht, dass „es für die Auslieferung perfekt sein muss“, hin zu einem Agile-Ansatz, der mit der minimal machbaren Sicherheit für Anwendungen (und für die Prozesse zu deren Entwicklung) beginnt und diese dann kontinuierlich inkrementell verbessert.
- **Verinnerlichen von cloudnativen** Infrastruktur- und Sicherheitsfeatures, um Entwicklungsprozesse zu optimieren und gleichzeitig die Sicherheit zu integrieren.
- **Risikomanagement der Lieferkette:** Verfolgen Sie einen „Zero Trust“-Ansatz für Open Source-Software (OSS) und Komponenten von Drittanbietern, der deren Integrität überprüft und sicherstellt, dass Fehlerkorrekturen und Updates auf diese Komponenten angewendet werden.
- **Kontinuierliches Lernen:** Das schnelle Releasetempo von Entwicklerdiensten (auch als Platform-as-a-Service-Dienste (PaaS) bezeichnet) und das Ändern der Zusammensetzung von Anwendungen bedeutet, dass Mitglieder der Entwicklungs-, Betriebs- und Sicherheitsteams ständig neue Technologien erlernen müssen.
- **Programmgesteuerte Vorgehensweise** bei der Anwendungssicherheit, um eine fortlaufende Verbesserung des Agile-Ansatzes sicherzustellen.

Weitere Kontextinformationen finden Sie unter [Sicherer Lebenszyklus der Entwicklung von Microsoft](https://www.microsoft.com/sdl).

## <a name="team-composition-and-key-relationships"></a>Teamzusammensetzung und wichtige Beziehungen

Anwendungssicherheit und DevSecOps-Funktionen werden idealerweise von sicherheitsgeschulten Entwicklern und Betriebsteams (mit Unterstützung von Sicherheitsexperten) ausgeführt.

Diese Funktion interagiert häufig mit anderen Funktionen und Experten, einschließlich:.

- Sicherheitsarchitektur und -betrieb
- Sicherheit der Infrastruktur
- Kommunikation (Schulung und Tools)
- Personensicherheit
- Identität und Schlüssel
- Compliance-/Risikomanagementteams
- Wichtige Führungskräfte oder deren Vertretungen

## <a name="next-steps"></a>Nächste Schritte

Informieren Sie sich über die Funktion der [Datensicherheit](./cloud-security-data-security.md).
