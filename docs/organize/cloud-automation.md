---
title: Funktionen zur Cloudautomatisierung
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um sich mit Funktionen zur Cloudautomatisierung vertraut zu machen, mit denen die Einführung und Innovationen beschleunigt werden können.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: 8e35ed2cdd90b51e13a29b0709f44ad395e9e0fb
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2020
ms.locfileid: "80428609"
---
# <a name="cloud-automation-capabilities"></a>Funktionen zur Cloudautomatisierung

Während der Cloudeinführung erschließen Funktionen für die Cloudautomatisierung das Potenzial von DevOps und einem cloudnativen Ansatz. Das Fachwissen in jedem dieser Bereiche kann die Einführung und Innovation beschleunigen.

## <a name="possible-sources-for-cloud-automation-expertise"></a>Mögliche Quellen für Fachkenntnisse der Cloudautomatisierung

Die für die Bereitstellung von Funktionen für die Cloudautomatisierung erforderlichen Qualifikationen könnten bereitgestellt werden durch:

- DevOps-Techniker
- Entwickler mit Fachwissen zu DevOps und Infrastruktur
- IT-Techniker mit Fachwissen zu DevOps und Automatisierung

Diese fachlichen Ansprechpartner bieten möglicherweise bereits Funktionen in anderen Bereichen wie Cloudeinführung, Cloudgovernance oder Cloudplattform. Nachdem sie ihre Kompetenz bei der Automatisierung komplexer Workloads unter Beweis gestellt haben, können Sie diese Experten einstellen, um einen Beitrag zur Automatisierung zu leisten.

## <a name="mindset"></a>Mindset

Vor der Aufnahme eines Teammitglieds in diese Gruppe sollte der Mitarbeiter drei wesentliche Merkmale aufweisen:

- Fachwissen zu einer Cloudplattform mit besonderem Schwerpunkt auf DevOps und Automatisierung.
- Eine wachstumsorientierte Denkweise oder Offenheit im Hinblick auf die Veränderung der heutigen Arbeitsweise der IT.
- Das Bestreben, den Geschäftswandel zu beschleunigen und traditionelle IT-Hürden zu beseitigen.

## <a name="key-responsibilities"></a>Wichtige Zuständigkeiten

Die Hauptaufgabe der Cloudautomatisierung besteht darin, den Lösungskatalog zu besitzen und weiterzuentwickeln. Der Lösungskatalog ist eine Sammlung von vordefinierten Lösungen oder Automatisierungsvorlagen. Diese Lösungen können bei Bedarf schnell verschiedene Plattformen bereitstellen, um erforderliche Workloads zu unterstützen. Diese Lösungen werden wie Bausteine verwendet, um die Einführung der Cloud zu beschleunigen und die Markteinführungszeit während der Migrations- oder Innovationstätigkeit zu verkürzen.

Beispiele für Lösungen im Katalog:

- Ein Skript zum Bereitstellen einer Containeranwendung.
- Eine Resource Manager-Vorlage zum Bereitstellen eines SQL HA AO-Clusters.
- Beispielcode zum Erstellen einer Bereitstellungspipeline mit Azure DevOps.
- Eine Azure DevTest Labs-Instanz des ERP-Systems des Unternehmens für Entwicklungszwecke.
- Automatisierte Bereitstellung einer Self-Service-Umgebung, die häufig von Geschäftsanwendern gewünscht wird.

Bei den Lösungen im Lösungskatalog handelt es sich nicht um Bereitstellungspipelines für eine Workload. Stattdessen können Sie Automatisierungsskripts im Katalog verwenden, um schnell eine Bereitstellungspipeline zu erstellen. Sie können auch eine Lösung im Katalog verwenden, um schnell Plattformkomponenten bereitzustellen, um Workloadaufgaben wie automatisierte Bereitstellung, manuelle Bereitstellung oder Migration zu unterstützen.

Die folgenden Aufgaben werden normalerweise regelmäßig von der Cloudautomatisierung ausgeführt:

### <a name="strategic-tasks"></a>Strategische Aufgaben

- Überprüfung:
  - [Geschäftsergebnisse](../strategy/business-outcomes/index.md)
  - [Finanzmodelle](../strategy/financial-models.md)
  - [Gründe für die Cloudeinführung](../strategy/motivations.md)
  - [Geschäftsrisiken](../govern/policy-compliance/risk-tolerance.md)
  - [Rationalisierung der digitalen Ressourcen](../digital-estate/index.md)
- Überwachung von Einführungplänen und Fortschritten anhand des [priorisierten Migrationsbacklogs](../migrate/migration-considerations/assess/release-iteration-backlog.md).
- Identifizieren Sie Möglichkeiten, um die Cloudeinführung zu beschleunigen, den Aufwand durch die Automatisierung zu reduzieren sowie die Sicherheit, Stabilität und Konsistenz zu verbessern.
- Priorisieren Sie einen Lösungsbacklog für den Lösungskatalog, der den größten Wert bei anderen strategischen Eingaben bietet.

### <a name="technical-tasks"></a>Technische Aufgaben

- Überprüfen oder entwickeln Sie Lösungen auf der Grundlage des priorisierten Backlogs.
- Stellen Sie sicher, dass die Lösungen auf die Plattformanforderungen abgestimmt sind.
- Stellen Sie sicher, dass Lösungen konsistent angewendet werden und die bestehenden Anforderungen an die Governance/Compliance erfüllen.
- Erstellen und validieren Sie Lösungen im Katalog.
- Überprüfen Sie die Releasepläne auf neue Möglichkeiten der Automatisierung.

## <a name="meeting-cadence"></a>Rhythmus von Besprechungen

Die Cloudautomatisierung umfasst ein funktionierendes Team. Gehen Sie davon aus, dass die Teilnehmer einen Großteil ihrer Zeit täglich für die Cloudautomatisierung einsetzen. Beiträge sind nicht auf Besprechungen und Feedbackzyklen beschränkt.

Das Cloudautomatisierungsteam sollte die Aktivitäten mit anderen Funktionsbereichen in Einklang bringen. Diese Vorgehensweise kann zu einer Besprechungsermüdung führen. Um sicherzustellen, dass die Cloudautomatisierung genügend Zeit für die Verwaltung des Lösungskatalogs hat, sollten Sie den Rhythmus von Besprechungen überprüfen, um die Zusammenarbeit zu maximieren und Störungen der Entwicklungsaktivitäten zu minimieren.

## <a name="next-steps"></a>Nächste Schritte

Wenn die wesentlichen Cloudfunktionen koordiniert wurden, können die kollektiven Teams [bei der Entwicklung der benötigten technischen Fähigkeiten](./suggested-skills.md) mitwirken.

> [!div class="nextstepaction"]
> [Entwickeln von technischen Fähigkeiten](./suggested-skills.md)
