---
title: Cloudrationalisierung
description: Beschreibt die Optionen, bei der Rationalisierung eines digitales Umfelds zur Verfügung stehen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/16/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.custom: governance
ms.openlocfilehash: 1a74487a77388e6260c177096d9563dbe6646cf2
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76806559"
---
# <a name="cloud-rationalization"></a>Cloudrationalisierung

Cloudrationalisierung bezeichnet die Untersuchung von Ressourcen, um die bestmögliche Migrations- oder Modernisierungsmethode für die jeweilige Ressource in der Cloud zu ermitteln. Weitere Informationen zum Rationalisierungsprozess finden Sie unter [Worum handelt es sich bei digitalen Ressourcen?](./index.md).

## <a name="rationalization-context"></a>Rationalisierungskontext

Die in diesem Artikel aufgeführten „fünf Phasen der Rationalisierung“ sind eine großartige Möglichkeit zur Bezeichnung eines potenziellen zukünftigen Zustands für jede Workload, die als Cloudkandidat betrachtet wird. Dieser Bezeichnungsprozess sollte jedoch in den richtigen Kontext gesetzt werden, bevor Sie versuchen, eine Umgebung zu rationalisieren. Überprüfen Sie die folgenden Mythen, um diesen Kontext bereitzustellen:

- **Mythos: Es ist einfach, Rationalisierungsentscheidungen in einem frühen Stadium des Prozesses zu treffen.** Eine genaue Rationalisierung erfordert ein fundiertes Wissen in Bezug auf die Workload und die damit verbundenen Ressourcen (Apps, VMs und Daten). Am wichtigsten ist, dass genaue Rationalisierungsentscheidungen Zeit in Anspruch nehmen. Wir empfehlen die Verwendung [eines inkrementellen Rationalisierungsprozesses](./rationalize.md#incremental-rationalization).

- **Mythos: Die Cloudeinführung muss darauf warten, dass alle Workloads rationalisiert sind.** Die Rationalisierung eines gesamten IT-Portfolios oder sogar eines einzelnen Rechenzentrums kann die Realisierung des Geschäftswerts um Monate oder sogar Jahre verzögern. Eine vollständige Rationalisierung sollte nach Möglichkeit vermieden werden. Verwenden Sie stattdessen den [10er-Ansatz für die Releaseplanung](./rationalize.md#release-planning), um kluge Entscheidungen zu den nächsten 10 Workloads zu treffen, die für die Cloudeinführung vorgesehen sind.

- **Mythos: Die geschäftliche Begründung muss warten, bis alle Workloads rationalisiert sind.** Um eine geschäftliche Begründung für eine Cloudeinführung zu entwickeln, machen Sie ein paar grundlegende Annahmen auf Portfolioebene. Wenn die Beweggründe an Innovationen ausgerichtet sind, gehen Sie von einer Umstrukturierung aus. Wenn die Beweggründe an der Migration ausgerichtet sind, gehen Sie vom Rehosten aus. Diese Annahmen können den Prozess der geschäftlichen Begründung beschleunigen. Annahmen werden dann in Frage gestellt und die Budgets während der Bewertungsphase der Einführungszyklen für die einzelnen Workloads optimiert.

Überprüfen Sie jetzt die folgenden fünf Phasen der Rationalisierung, um sich mit dem zeitintensiven Prozess vertraut zu machen. Wählen Sie bei der Entwicklung Ihres Cloudeinführungsplans die Option aus, die am besten zu Ihren Beweggründen, Geschäftsergebnissen und der aktuellen Situation passt. Das Ziel der Rationalisierung digitaler Ressourcen ist es, Grundwerte festzulegen, und nicht die Rationalisierung sämtlicher Workloads.

## <a name="the-five-rs-of-rationalization"></a>Die fünf Phasen der Rationalisierung

Die hier aufgeführten fünf Phasen der Rationalisierung beschreiben die gängigsten Optionen für die Rationalisierung.

## <a name="rehost"></a>Rehosten

Auch _Lift & Shift_-Migration genannt. Beim Rehosten wird die Ressource im aktuellen Zustand zum gewählten Cloudanbieter migriert. Die Architektur bleibt dabei größtenteils unverändert.

Häufige Motive können Folgendes umfassen:

- Reduzieren der Investitionskosten
- Freigeben von Platz im Rechenzentrum
- Erzielen eine schnelle Rendite in der Cloud

Faktoren für die quantitative Analyse:

- VM-Größe (CPU, Arbeitsspeicher, Speicherplatz)
- Abhängigkeiten (Netzwerkdatenverkehr)
- Ressourcenkompatibilität

Faktoren für die qualitative Analyse:

- Änderungstoleranz
- Geschäftliche Prioritäten
- Kritische Unternehmensereignisse
- Prozessabhängigkeiten

## <a name="refactor"></a>Refactoring

PaaS-Optionen (Platform-as-a-Service) können zur Senkung der Betriebskosten zahlreicher Anwendungen beitragen. Es empfiehlt sich, eine Anwendung geringfügig umzugestalten, um sie an ein PaaS-basiertes Modell anzupassen.

„Umgestalten“ (Refactoring) bezieht sich auch auf den Anwendungsentwicklungsprozess der Codeumgestaltung, damit eine Anwendung neue Geschäftsmöglichkeiten erschließen kann.

Häufige Motive können Folgendes umfassen:

- Schnellere und kürzere Updates
- Codeportabilität
- Höhere Cloudeffizienz (Ressourcen, Geschwindigkeit, Kosten, verwaltete Vorgänge)

Faktoren für die quantitative Analyse:

- Größe der Anwendungsressource (CPU, Arbeitsspeicher, Speicherplatz)
- Abhängigkeiten (Netzwerkdatenverkehr)
- Benutzerdatenverkehr (Seitenaufrufe, Verweildauer auf der Seite, Ladezeit)
- Entwicklungsplattform (Sprachen, Datenplattform, Dienste der mittleren Ebene)
- Datenbank (CPU, Arbeitsspeicher, Speicherplatz, Version)

Faktoren für die qualitative Analyse:

- Laufende Unternehmensinvestitionen
- Burstoptionen/-zeitpläne
- Geschäftsprozessabhängigkeiten

## <a name="rearchitect"></a>Rearchitect (Überarbeiten)

Einige ältere Anwendungen sind aufgrund der architekturbezogenen Entscheidungen, die bei der Entwicklung der Anwendung getroffen wurden, mit Cloudanbietern nicht kompatibel. In diesem Fall muss die Anwendung vor der Transformation ggf. überarbeitet werden.

In anderen Fällen können Anwendungen, die zwar mit der Cloud kompatibel, aber keine nativen Cloudanwendungen sind, unter Umständen kostengünstiger und effizienter betrieben werden, indem die Lösung überarbeitet und in eine native Cloudanwendung umgewandelt wird.

Häufige Motive können Folgendes umfassen:

- Skalierbarkeit und Flexibilität der Anwendung
- Einfachere Einführung neuer Cloudfunktionen
- Verwendung verschiedener Technologiestapel

Faktoren für die quantitative Analyse:

- Größe der Anwendungsressource (CPU, Arbeitsspeicher, Speicherplatz)
- Abhängigkeiten (Netzwerkdatenverkehr)
- Benutzerdatenverkehr (Seitenaufrufe, Verweildauer auf der Seite, Ladezeit)
- Entwicklungsplattform (Sprachen, Datenplattform, Dienste der mittleren Ebene)
- Datenbank (CPU, Arbeitsspeicher, Speicherplatz, Version)

Faktoren für die qualitative Analyse:

- Steigende Unternehmensinvestitionen
- Betriebskosten
- Potenzielle Feedbackschleifen und DevOps-Investitionen.

## <a name="rebuild"></a>Neu erstellen

In manchen Szenarien kann die Kluft, die für die Weiterverwendung einer Anwendung überwunden werden muss, zu groß sein, um weitere Investitionen zu rechtfertigen. Dies gilt insbesondere für Anwendungen, die die Anforderungen eines Unternehmens bereits erfüllen, aber jetzt nicht mehr unterstützt werden oder an die aktuellen Geschäftsprozesse nicht angepasst sind. In diesem Fall wird eine neue Codebasis erstellt, die auf einen [cloudnativen](https://azure.microsoft.com/overview/cloudnative) Ansatz ausgerichtet ist.

Häufige Motive können Folgendes umfassen:

- Beschleunigung von Innovationen
- Schnellere App-Erstellung
- Senkung der Betriebskosten

Faktoren für die quantitative Analyse:

- Größe der Anwendungsressource (CPU, Arbeitsspeicher, Speicherplatz)
- Abhängigkeiten (Netzwerkdatenverkehr)
- Benutzerdatenverkehr (Seitenaufrufe, Verweildauer auf der Seite, Ladezeit)
- Entwicklungsplattform (Sprachen, Datenplattform, Dienste der mittleren Ebene)
- Datenbank (CPU, Arbeitsspeicher, Speicherplatz, Version)

Faktoren für die qualitative Analyse:

- Sinkende Endbenutzerzufriedenheit
- Einschränkung von Geschäftsprozessen aufgrund des Funktionsumfangs
- Potenzielle Verbesserungen bei Kosten, Erfahrung oder Umsatz

## <a name="replace"></a>Replace

Lösungen werden in der Regel mit der besten Technologie und Methode implementiert, die zu diesem Zeitpunkt zur Verfügung steht. Manchmal können SaaS-Anwendungen (Software-as-a-Service) alle erforderlichen Funktionen für die gehostete Anwendung bereitstellen. In diesem Fall kann eine Workload zukünftig ersetzt werden, wodurch sie bei der Transformation praktisch nicht weiter berücksichtigt werden muss.

Häufige Motive können Folgendes umfassen:

- Standardisierung auf der Grundlage bewährter Branchenmethoden
- Beschleunigung der Einführung geschäftsprozessbasierter Ansätze
- Umverteilung von Entwicklungsinvestitionen für Anwendungen, die Alleinstellungsmerkmale oder Wettbewerbsvorteile generieren

Faktoren für die quantitative Analyse:

- Senkung der allgemeinen Betriebskosten
- VM-Größe (CPU, Arbeitsspeicher, Speicherplatz)
- Abhängigkeiten (Netzwerkdatenverkehr)
- Auszumusternde Ressourcen
- Datenbank (CPU, Arbeitsspeicher, Speicherplatz, Version)

Faktoren für die qualitative Analyse:

- Kosten-Nutzen-Analyse der aktuellen Architektur im Vergleich zu einer SaaS-Lösung
- Geschäftsprozesszuordnungen
- Datenschemas
- Benutzerdefinierte oder automatisierte Prozesse

## <a name="next-steps"></a>Nächste Schritte

Gemeinsam können Sie diese fünf Phasen der Rationalisierung auf digitale Ressourcen anwenden, damit Sie Rationalisierungsentscheidungen zum zukünftigen Status der einzelnen Anwendungen einfacher treffen können.

> [!div class="nextstepaction"]
> [Worum handelt es sich bei digitalen Ressourcen?](./index.md)
