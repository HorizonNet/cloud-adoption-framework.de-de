---
title: Qualifikationsbereitschaft für Cloudüberwachung
description: Qualifikationsbereitschaft für Cloudüberwachung
author: BrianBlanchard
ms.author: magoedte
ms.date: 05/05/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: c32ecde3bc5929bc8ed360b1d792e5f2345bfd8f
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83223676"
---
<!-- cSpell:ignore kusto ITIL -->

# <a name="skills-readiness-for-cloud-monitoring"></a>Qualifikationsbereitschaft für Cloudüberwachung

Das Ziel der Phase „Planung“ Ihrer Migrationsjourney besteht darin, die notwendigen Pläne für die Implementierung zu entwickeln. In den Plänen muss auch festgelegt werden, wie Sie diese Workloads abarbeiten, bevor die Umstellung bzw. die Freigabe für die Produktion erfolgt (und nicht danach). Die Beteiligten im Unternehmen erwarten nützliche Dienste, die ohne Störungen funktionieren. IT-Mitarbeiter merken, dass sie neue Qualifikationen erwerben und sich anpassen müssen, damit sie die integrierten Azure-Dienste sicher verwenden können, um Ressourcen in Azure und in Hybridumgebungen effektiv zu überwachen.

Die Entwicklung der erforderlichen Qualifikationen kann mit den folgenden Lernpfaden beschleunigt werden:

- In der Einführung in [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/management/overview) werden die grundlegenden Konzepte der Verwaltung und Bereitstellung von Azure-Ressourcen beschrieben. Die IT-Mitarbeiter, die die Überwachungsumgebung im gesamten Unternehmen verwalten, sollten mit Verwaltungsbereichen, rollenbasierter Zugriffssteuerung (RBAC), Azure Resource Manager-Vorlagen und der Verwaltung von Ressourcen per Azure CLI und Azure PowerShell vertraut sein.

- Informieren Sie sich über das Schützen von Ressourcen mit Richtlinien, rollenbasierter Zugriffssteuerung und anderen Azure-Diensten, indem Sie den Artikel [Implementieren der Sicherheit für die Ressourcenverwaltung in Azure](https://docs.microsoft.com/learn/paths/implement-resource-mgmt-security) lesen.

- In der Einführung in [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) wird beschrieben, wie Sie Azure Policy zum Erstellen, Zuweisen und Verwalten von Richtlinien verwenden können. Mit Azure Policy können Sie die Azure Monitor-Agents bereitstellen und konfigurieren, die Überwachung mit Azure Monitor für VMs und Azure Security Center ermöglichen, Diagnoseeinstellungen bereitstellen, Gastkonfigurationseinstellungen überwachen und vieles mehr.

- Lesen Sie die Einführung in die [Azure-Befehlszeilenschnittstelle (CLI)](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli?view=azure-cli-latest). Hierbei handelt es sich um unsere plattformübergreifende Befehlszeilenumgebung zum Verwalten von Azure-Ressourcen. Sehen Sie sich auch die Einführung in [Azure PowerShell](https://docs.microsoft.com/powershell/azure/?view=azps-3.6.1) an. Im Rahmen des Anfängerkurses zum [Erlernen von Azure-Verwaltungstools](https://www.linkedin.com/learning/learning-azure-management-tools) werden von LinkedIn Sitzungen zur Azure CLI und zu PowerShell-Programmiersprachen angeboten:

  - [Verwenden der Azure CLI](https://www.linkedin.com/learning/learning-azure-management-tools/use-the-azure-cli)
  - [Erste Schritte mit Azure PowerShell](https://www.linkedin.com/learning/learning-azure-management-tools/understand-azure-powershell)

- Informieren Sie sich darüber, wie Sie [Protokollabfragen in Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/log-query/get-started-queries) schreiben. Die Kusto-Abfragesprache ist die Hauptressource für das Schreiben von Azure Monitor-Protokollabfragen, um Protokolldaten für die erfassten Daten aus Azure und die Abhängigkeiten von Hybridressourcenanwendungen (einschließlich Liveanwendung) zu untersuchen und zu analysieren.

- Informieren Sie sich darüber, wie [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) Ihnen das Anzeigen der Verfügbarkeit und Leistung Ihrer Anwendungen und Dienste an einem zentralen Ort ermöglicht. Von Pluralsight werden die folgenden Kurse angeboten:

  - Unter [Überwachen von Microsoft Azure-Ressourcen und -Workloads](https://app.pluralsight.com/library/courses/microsoft-azure-resources-workloads-monitoring-update/table-of-contents) wird beschrieben, wie Sie Microsoft Azure-Überwachungstools zum Überwachen von Azure-Netzwerkressourcen sowie lokalen Ressourcen verwenden.

  - Unter [Microsoft Azure DevOps-Techniker: Optimieren von Feedbackmechanismen](https://www.pluralsight.com/courses/microsoft-azure-optimize-feedback-mechanisms) können Sie sich darauf vorbereiten, Azure Monitor, einschließlich Application Insights und Log Analytics, für die Überwachung und Optimierung Ihrer Webanwendungen zu verwenden.

  - Unter [Microsoft Azure-Datenbanküberwachung: Playbook](https://www.pluralsight.com/courses/microsoft-azure-database-playbook-monitoring) wird beschrieben, wie Sie die Überwachung von Azure SQL-Datenbank, Azure SQL Data Warehouse und Azure Cosmos DB implementieren und nutzen.

  - In dem Kurs [Instrumentieren von Anwendungen mit Azure Monitor Application Insights](https://app.pluralsight.com/library/courses/microsoft-azure-application-insights-web-application-instrument) wird ausführlich beschrieben, wie Sie das Application Insights SDK zum Sammeln von Telemetriedaten und Ereignissen einer App mit Angular- und Node.js-Komponenten verwenden.

- Der Artikel [Azure Arc für Server](https://docs.microsoft.com/azure/azure-arc/servers/overview) enthält eine Beschreibung dazu, wie Sie Ihre außerhalb von Azure gehosteten Windows- und Linux-Computer auf ähnliche Weise wie Ihre nativen virtuellen Azure-Computer verwalten können.

## <a name="deeper-skills-exploration"></a>Ausführlichere Untersuchung von Fähigkeiten

Neben diesen ersten Möglichkeiten zur Entwicklung von Fähigkeiten steht eine Vielzahl von Lernoptionen zur Verfügung.

### <a name="typical-mappings-of-cloud-it-roles"></a>Typische Zuordnungen von Cloud-IT-Rollen

Microsoft und seine Partner bieten eine Vielzahl von Optionen für alle Zielgruppen zur Erweiterung ihrer Fähigkeiten mit Azure-Diensten:

- [Microsoft IT Pro Career Center](https://www.microsoft.com/itpro): Kostenlose Onlineressource zur Begleitung Ihres Karrierewegs in der Cloud. Profitieren Sie von den Empfehlungen von Branchenexperten für Ihre Cloudrolle und zu den Fähigkeiten, mit denen Sie sie erreichen. Folgen Sie in Ihrem eigenen Tempo einem Lehrplan, um die Fähigkeiten zu erlangen, die Sie am meisten benötigen, um auf dem aktuellen Stand zu bleiben.

Mit unseren [Microsoft Azure-Zertifizierungstrainings und -prüfungen]( https://www.microsoft.com/learning/certification-overview.aspx) können Sie Ihr Wissen rund um Azure belegen und sich offizielle Anerkennung verschaffen.

## <a name="azure-devops-and-project-management"></a>Azure DevOps und Projektmanagement

Die Hybrid Cloud-Umgebung bedeutet für die IT-Abteilung, dass nicht definierte Rollen, Zuständigkeiten und Aktivitäten bewältigt werden müssen. Organisationen müssen die Umstellung auf moderne Dienstverwaltungsverfahren vollziehen, z. B. in Bezug auf Agile- und DevOps-Methodiken, um die Transformations- und Optimierungsanforderungen heutiger Unternehmen schneller und effizienter erfüllen zu können.

Im Rahmen der Migration zu einer Cloudüberwachungsplattform muss das IT-Team, das im Unternehmen für die Verwaltung der Überwachung zuständig ist, für flexible Schulungs- und Beteiligungsmöglichkeiten in Bezug auf DevOps-Aktivitäten sorgen. Hierbei kommt auch die _Dev_-Komponente von DevOps ins Spiel. Die üblichen Anforderungen werden in organisierte flexible Anforderungen umgewandelt, um minimal ausgestattete Überwachungslösungen bereitzustellen, die iterativ optimiert werden und die Bedürfnisse des Unternehmens erfüllen. Verknüpfen Sie Ihr Azure DevOps Server-Projekt mit einem GitHub Enterprise-Server-Repository, um die Verwaltung der iterativen Überwachungslösungspakete und anderer zugehöriger Materialien per Quellcodeverwaltung zu ermöglichen. Hierdurch wird eine Verknüpfung zwischen GitHub-Commits und Pull Requests für Arbeitselemente hergestellt. Sie können GitHub Enterprise für die Entwicklung verwenden, um Continuous Integration/Deployment zu Überwachungszwecken zu unterstützen, während Sie Azure Boards nutzen, um Ihre Arbeit zu planen und nachzuverfolgen.

Weitere Informationen finden Sie in den folgenden Artikeln:

- [Erste Schritte mit Azure DevOps](https://docs.microsoft.com/learn/modules/get-started-with-devops)

- [Informationen zur White Belt Foundation des DevOps-Dojos](https://docs.microsoft.com/learn/paths/devops-dojo-white-belt-foundation)

- [Weiterentwickeln Ihrer DevOps-Methoden](https://docs.microsoft.com/learn/paths/evolve-your-devops-practices)

- [Automatisieren von Bereitstellungen mit Azure DevOps](https://docs.microsoft.com/learn/paths/automate-deployments-azure-devops)

## <a name="other-considerations"></a>Weitere Überlegungen

Kunden haben häufig Schwierigkeiten, für die von der IT-Abteilung bereitzustellenden Dienste die erwarteten Geschäftsergebnisse (einschließlich der Ergebnisse für die IT-Abteilung) zu verwalten und zu erzielen. Die Überwachung wird als Kernaspekt der Verwaltung der Infrastruktur und des Unternehmens betrachtet, und der Fokus liegt auf der Messung der Qualität des Diensts und der Kundenerfahrung. Schaffen Sie die Basis für die Erreichung dieser Ziele, indem Sie ITSM in Verbindung mit DevOps verwenden. Auf diese Weise kann das Überwachungsteam seine Leistung beim Verwalten, Bereitstellen und Unterstützen des Überwachungsdiensts verbessern. Durch die Einführung eines ITSM-Frameworks kann das Überwachungsteam als Anbieter fungieren und sich Anerkennung als vertrauenswürdiger Geschäftsmotor erwerben, indem es die strategischen Ziele und Anforderungen der Organisation aufeinander abstimmt.

Lesen Sie das [Whitepaper zu ITIL v4 und Cloud Computing](https://www.axelos.com/case-studies-and-white-papers/itil-4-and-the-cloud) um sich mit den Updates vertraut zu machen, die für das beliebteste ITSM-Framework durchgeführt wurden. Es wird beschrieben, wie die vorhandene ITIL-Anleitung mit den bewährten Methoden von DevOps, Agile und Lean verbunden werden kann. Informieren Sie sich auch über die [IT4IT-Referenzarchitektur](https://www.opengroup.org/it4it), bei der es sich um eine alternative Blaupause für die IT-Transformation mithilfe eines prozessagnostischen Frameworks handelt.

## <a name="learn-more"></a>Weitere Informationen

Weitere Lernpfade finden Sie im [Microsoft Learn-Katalog](https://docs.microsoft.com/learn/browse). Verwenden Sie den Filter „Rollen“, um Lernpfade an ihrer Rolle auszurichten.
