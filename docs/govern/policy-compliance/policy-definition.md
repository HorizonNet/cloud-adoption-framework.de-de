---
title: Definieren von Unternehmensrichtlinien für Cloudgovernance
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: In diesem Artikel wird erläutert, wie Sie eine Richtlinie einrichten, um Risiken wiederzugeben und zu mindern.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.openlocfilehash: 4184ccdd4a0efa06d6a842f7ba1d9cbf0dc77ea6
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/24/2019
ms.locfileid: "71223730"
---
# <a name="define-corporate-policy-for-cloud-governance"></a>Definieren von Unternehmensrichtlinien für Cloudgovernance

Nachdem Sie die bekannten Risiken und damit verbundene Risikotoleranzen für den Weg Ihrer Organisation in die Cloud analysiert haben, besteht Ihr nächster Schritt darin, eine Richtlinie einzurichten, die diese Risiken explizit behandelt und die Schritte, um sie nach Möglichkeit zu verringern, definiert.

<!-- markdownlint-disable MD026 -->

## <a name="how-can-corporate-it-policy-become-cloud-ready"></a>Wie kann für die IT-Unternehmensrichtlinie die Bereitschaft für die Cloud erzielt werden?

Bei herkömmlichen und inkrementellen Governanceverfahren wird die Arbeitsdefinition der Governance mithilfe einer Unternehmensrichtlinie erstellt. Die meisten IT-Governanceaktionen sind darauf ausgelegt, Technologien zum Überwachen, Durchsetzen, Ausführen und Automatisieren dieser Unternehmensrichtlinien zu implementieren. Cloudgovernance basiert auf ähnlichen Konzepten.

![Unternehmensgovernance und Governancedisziplinen](../../_images/operational-transformation-govern-highres.png)

*Abbildung 1: Unternehmensgovernance und Governancedisziplinen*

Das vorstehende Bild veranschaulicht den Zusammenhang zwischen Geschäftsrisiko, Richtlinie und Compliance sowie Überwachungs- und Erzwingungsmechanismen, die als Teil Ihrer Governancestrategie interagieren müssen. Mit den fünf Disziplinen von Cloudgovernance können Sie diese Interaktionen verwalten und Ihrer Strategie umsetzen.

Cloudgovernance ist das Resultat kontinuierlicher Bemühungen zur Einführung, da eine nachhaltige Transformation nicht über Nacht geschieht. Der Versuch, mit einer schnellen, aggressiven Methode vollständige Cloudgovernance herzustellen, bevor zentrale Änderungen der Unternehmensrichtlinien durchdacht und umgesetzt wurden, führt nur selten zu den gewünschten Ergebnissen. Stattdessen empfiehlt sich ein inkrementeller Ansatz.

Ein Framework für die Einführung der Cloud hebt sich durch seinen Kaufzyklus sowie durch die Ermöglichung einer authentischen Transformation ab. Da keine umfangreichen Kapitalinvestitionen für Anschaffungen erforderlich sind, können Techniker bereits früher mit dem Test- und Einführungsprozess beginnen. In den meisten Unternehmenskulturen kann die Tatsache, dass Kapitalausgaben kein Hindernis für die Einführung mehr sind, zu kürzeren Feedbackschleifen, einem organischen Wachstum und inkrementeller Ausführung führen.

Die Einführung der Cloud erfordert ein Umdenken bei der Governance. In vielen Organisationen sorgt die Transformation der Unternehmensrichtlinien für verbesserte Governance und eine umfassendere Einhaltung durch inkrementelle Richtlinienänderungen sowie automatisierte Erzwingung dieser Änderungen, gestützt durch die neu definierten Funktionen, die Sie mit Ihrem Clouddienstanbieter konfigurieren.

<!-- markdownlint-enable MD026 -->

## <a name="review-existing-policies"></a>Überprüfen vorhandener Richtlinien

Governance ist ein fortlaufender Prozess, und Richtlinien sollten regelmäßig daher gemeinsam mit den IT-Mitarbeitern und Projektbeteiligten überprüft werden, um sicherzustellen, dass in der Cloud gehostete Ressourcen die allgemeinen Unternehmensziele und -anforderungen weiterhin einhalten. Das Wissen um neue Risiken und akzeptable Toleranzgrenzen kann eine [Überprüfung der vorhandenen Richtlinien](./cloud-policy-review.md) vorantreiben, bei der ermittelt werden soll, welches Maß an Governance für Ihre Organisation geeignet ist.

> [!TIP]
> Wenn Ihre Organisation Anbieter oder andere vertrauenswürdige Geschäftspartner einsetzt, kann eines der größten zu berücksichtigenden Geschäftsrisiken darin bestehen, dass diese externen Unternehmen die [gesetzlichen Vorschriften](./regulatory-compliance.md) nicht einhalten. Dieses Risiko kann oft nicht korrigiert werden und erfordert stattdessen die strikte Einhaltung der Anforderungen durch alle Beteiligten. Stellen Sie sicher, dass Sie alle Complianceanforderungen von Drittanbietern identifiziert und verstanden haben, bevor Sie mit einer Überprüfung der Richtlinie beginnen.

## <a name="create-cloud-policy-statements"></a>Erstellen von Cloudrichtlinienanweisungen

Cloudbasierte IT-Richtlinien legen die Anforderungen, Standards und Ziele fest, die Ihre IT-Mitarbeiter und automatisierten Systeme unterstützen müssen. Richtlinienentscheidungen sind einer der wichtigsten Faktoren in Ihrem [Cloudarchitekturentwurf](./governance-alignment.md) und der Implementierung Ihrer [Richtlinieneinhaltungsprozesse](./processes.md).

Einzelne Cloudrichtlinienanweisungen sind Anleitungen für den Umgang mit bestimmten Risiken, die während Ihres Risikobewertungsprozesses identifiziert wurden. Diese Richtlinien können in die Dokumentation Ihrer Unternehmensrichtlinien integriert werden, jedoch bieten Cloudrichtlinienanweisungen, die im Cloud Adoption Framework-Leitfaden erläutert werden, meist eine präzisere Zusammenfassung der Risiken und der Pläne für den Umgang mit ihnen. Jede Definition sollte diese Informationen enthalten:

- **Geschäftsrisiko:** Eine Zusammenfassung des Risikos, das diese Richtlinie behandelt.
- **Richtlinienanweisung:** Eine knappe Erläuterung der Richtlinienanforderungen und -ziele.
- **Entwurfs- oder technischer Leitfaden:** Direkt umsetzbare Empfehlungen, Spezifikationen oder andere Anleitungen zur Unterstützung und Erzwingung dieser Richtlinie, auf die IT-Teams und Entwickler beim Entwerfen und Erstellen ihrer Cloudbereitstellungen zurückgreifen können.

Wenn Sie Unterstützung bei den ersten Schritten der Definition von Richtlinien benötigen, lesen Sie die [Governancedisziplinen](../governance-disciplines.md), die in der Übersicht des Governanceabschnitts eingeführt werden. Die Artikel für die einzelnen Disziplinen enthalten Beispiele verbreiteter Geschäftsrisiken, die bei der Umstellung in die Cloud auftreten können, und Beispielrichtlinien zum Vermindern dieser Risiken (Beispiel: die [Beispielrichtliniendefinitionen](../cost-management/policy-statements.md) für die Disziplin von Cost Management).

## <a name="incremental-governance-and-integrating-with-existing-policy"></a>Inkrementelle Governance und Integration in vorhandene Richtlinien

Geplante Ergänzungen Ihrer Cloudumgebung sollten immer auf die Einhaltung vorhandener Richtlinien überprüft werden, und die Richtlinien sollten aktualisiert werden, sodass sie bisher nicht behandelte Probleme berücksichtigen. Sie sollten auch regelmäßig [Ihre Cloudrichtlinie überprüfen](./cloud-policy-review.md), um sicherzustellen, dass diese auf dem neuesten Stand und im Einklang mit neuen Unternehmensrichtlinien ist.

Die Notwendigkeit, Cloudrichtlinien in Ihre bereits bestehenden IT-Richtlinien zu integrieren, hängt hauptsächlich von der Ausgereiftheit Ihrer Cloudgovernanceprozesse und der Größe Ihrer Cloudumgebung ab. Eine umfassendere Erläuterung zur Richtlinienintegration während der Cloudtransformation finden Sie im Artikel zu [inkrementeller Governance und dem Richtlinien-MVP](./index.md).

## <a name="next-steps"></a>Nächste Schritte

Entwerfen Sie nach dem Definieren Ihrer Richtlinien ein Architekturentwurfshandbuch, um für IT-Mitarbeiter und Entwickler umsetzbare Anleitungen bereitzustellen.

> [!div class="nextstepaction"]
> [Ausrichten Ihres Governance-Entwurfshandbuchs an der Unternehmensrichtlinie](./governance-alignment.md)
