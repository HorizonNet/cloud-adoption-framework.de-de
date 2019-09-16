---
title: 'Governanceleitfaden für komplexe Unternehmen: Mehrere Governance-Ebenen'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Governanceleitfaden für komplexe Unternehmen: Mehrere Governance-Ebenen'
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: a0a2674a91b963154d757eb35290b8aeead5c503
ms.sourcegitcommit: 5846ed4d0bf1b6440f5e87bc34ef31ec8b40b338
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/11/2019
ms.locfileid: "70909053"
---
# <a name="governance-guide-for-complex-enterprises-multiple-layers-of-governance"></a>Governanceleitfaden für komplexe Unternehmen: Mehrere Governance-Ebenen

Wenn große Unternehmen mehrere Governance-Ebenen benötigen, gibt es ein höheres Maß an Komplexität, das in den Governance MVP und spätere Verbesserungen der Governance einfließen muss.

Dies sind einige allgemeine Beispiele für solche Komplexität:

- Verteilte Governance-Funktionen.
- Eine Unternehmens-IT, die IT-Organisationen von Geschäftseinheiten unterstützt.
- Eine Unternehmens-IT, die geografisch verteilte IT-Organisationen unterstützt.

Dieser Artikel untersucht einige Möglichkeiten, in dieser Komplexität die Orientierung zu bewahren.

## <a name="large-enterprise-governance-is-a-team-sport"></a>Governance in großen Unternehmen ist ein Mannschaftssport

Große, etablierte Unternehmen verfügen oft über Teams oder Mitarbeiter, die sich auf die in diesem Leitfaden erwähnten Fachrichtungen spezialisiert haben. Dieser Leitfaden veranschaulicht einen Ansatz, um Governance zu einem Mannschaftssport zu machen.

In vielen großen Unternehmen können sich die fünf Disziplinen der Cloud-Governance als Einführungshindernisse erweisen. Die Entwicklung von Cloudexpertise in den Bereichen Identität, Sicherheit, Betrieb, Bereitstellung und Konfiguration in einem gesamten Unternehmen erfordert Zeit. Eine ganzheitliche Implementierung von IT-Governance-Richtlinien und IT-Sicherheit kann Innovationen um Monate oder sogar Jahre verzögern. Das Gleichgewicht zwischen dem Innovationsbedarf des Unternehmens und dem Governance-Bedarf zum Schutz der vorhandenen Ressourcen ist schwierig.

Die inhärenten Fähigkeiten der Cloud können Innovationshemmnisse beseitigen, aber die Risiken erhöhen. In diesem Governanceleitfaden haben wir gezeigt, wie unser Beispielunternehmen Sicherungsmaßnahmen eingerichtet hat, um die Risiken zu minimieren. Anstatt sich mit jeder der Disziplinen zu befassen, die zum Schutz der Umgebung benötigt werden, verfolgt das Cloudgovernanceteam einen risikobasierten Ansatz, um zu steuern, was sich einsetzen lässt, während die anderen Teams die erforderliche Cloudreife aufbauen. Besonders wichtig ist dabei, dass Governance die Lösungen der einzelnen Teams ganzheitlich übernimmt, sobald sie die Cloudreife erreicht haben. Mit zunehmender Reife der Teams und ihrem zunehmenden Anteil an der Gesamtlösung kann das Cloudgovernanceteam Stage Gates öffnen, wodurch Innovation und Akzeptanz zusätzlichen Schub erhalten.

Dieses Modell veranschaulicht die wachsende Partnerschaft zwischen dem Cloudgovernanceteam und bestehenden Unternehmensteams (Sicherheit, IT Governance, Netzwerk, Identität und andere). Dieser Leitfaden beginnt mit dem Governance-MVP und wächst dank der Governanceiterationen zu einem ganzheitlichen Endzustand.

## <a name="requirements-to-supporting-such-a-team-sport"></a>Anforderungen zur Unterstützung von Governance als Mannschaftssport

Die erste Anforderung an ein mehrschichtiges Governancemodell ist das Verständnis der Governancehierarchie. Die Antworten auf die folgenden Fragen helfen Ihnen, die allgemeine Governance-Hierarchie zu verstehen:

- Wie ist die Cloudabrechnung (Abrechnung von Clouddiensten) auf die Geschäftseinheiten verteilt?
- Wie sind die Governance-Zuständigkeiten zwischen der Unternehmens-IT und den einzelnen Geschäftseinheiten verteilt?
- Welche Arten von Umgebungen verwalten die einzelnen IT-Einheiten?

## <a name="central-governance-of-a-distributed-governance-hierarchy"></a>Zentrale Governance einer verteilten Governance-Hierarchie

Mithilfe von Tools wie Verwaltungsgruppen kann die Unternehmens-IT eine Hierarchiestruktur erstellen, die der Governance-Hierarchie entspricht. Tools wie Azure Blueprints können Ressourcen auf verschiedene Ebenen dieser Hierarchie anwenden. Azure Blueprints können versioniert werden, und verschiedene Versionen können auf Verwaltungsgruppen, Abonnements oder Ressourcengruppen angewendet werden. Die einzelnen Konzepte sind im Governance-MVP ausführlicher erläutert.

Der wichtige Aspekt jedes dieser Tools ist seine Fähigkeit, mehrere Blaupausen auf eine Hierarchie anzuwenden. Dadurch kann Governance zu einem mehrstufigen Prozess werden. Hier folgt ein Beispiel dieser hierarchischen Anwendung von Governance:

- **Unternehmens-IT:** Die Unternehmens-IT erstellt eine Reihe von Standards und Richtlinien, die die gesamte Cloudeinführung betreffen. Dies wird in einer "Baseline"-Blaupause festgehalten. Die Unternehmens-IT besitzt dann die Hierarchie der Verwaltungsgruppen, was sicherstellt, dass eine Version der Baseline auf alle Abonnements in der Hierarchie angewendet wird.
- **Regionale oder Geschäftseinheits-IT:** Verschiedene IT-Teams können eine zusätzliche Governance-Ebene anwenden, indem sie ihre eigene Blaupause erstellen. Mithilfe dieser Blaupausen werden zusätzliche Richtlinien und Standards erstellt. Nach der Entwicklung kann die Unternehmens-IT diese Blaupausen auf die entsprechenden Knoten innerhalb der Verwaltungsgruppenhierarchie anwenden.
- **Cloudeinführungsteams:** Detaillierte Entscheidungen und Implementierungen von Anwendungen oder Workloads können von den Cloudeinführungsteams im Kontext von Governanceanforderungen getroffen bzw. vorgenommen werden. Gegebenenfalls kann das Team auch zusätzliche Azure Resource Consistency Templates anfordern, um die Einführungsbemühungen zu beschleunigen.

Die Einzelheiten der Umsetzung der Governance auf jeder Ebene erfordern eine Koordination zwischen den einzelnen Teams. Die in diesem Leitfaden skizzierten Governance-MVP und Governanceverbesserungen können zur Abstimmung dieser Koordination beitragen.

