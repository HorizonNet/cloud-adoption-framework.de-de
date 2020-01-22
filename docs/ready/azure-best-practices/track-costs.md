---
title: Nachverfolgen von Kosten für Geschäftseinheiten, Umgebungen oder Projekte
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Nachverfolgen von Kosten für Geschäftseinheiten, Umgebungen oder Projekte
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: b9bc3a5c2b2bf62c49726a29cedbac81d1d1a96e
ms.sourcegitcommit: b166fe1621fe7e886616009e56b76873b8cce83c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/22/2020
ms.locfileid: "76520173"
---
# <a name="track-costs-across-business-units-environments-or-projects"></a>Nachverfolgen von Kosten für Geschäftseinheiten, Umgebungen oder Projekte

Für das [Schaffen einer kostenbewussten Organisation](../../organize/cost-conscious-organization.md) ist Transparenz und ein gut definierter Zugriff auf kostenbezogene Daten erforderlich (bzw. ein entsprechender Bereich). In diesem Artikel zu den bewährten Methoden werden Entscheidungen und Implementierungsansätze für die Erstellung von angemessenen Mechanismen für die Nachverfolgung beschrieben.

![Darstellung des Prozesses für Kostenbewusstsein](../../_images/ready/cost-optimization-process.png)

## <a name="establish-a-well-managed-environment-hierarchy"></a>Aufstellen einer gut verwalteten Umgebungshierarchie

Die Kostenkontrolle hängt, ähnlich wie Governance und andere Verwaltungsansätze, von einer gut verwalteten Umgebung ab. Für die Schaffung einer Umgebung dieser Art (insbesondere einer komplexen) sind einheitliche Prozesse in Bezug auf die Klassifizierung und Organisation aller Ressourcen erforderlich.

Ressourcen sind alle virtuellen Computer, Datenquellen und Anwendungen, die in der Cloud bereitgestellt werden. Azure verfügt über verschiedene Mechanismen zum Klassifizieren und Organisieren von Ressourcen. Unter [Skalieren mit mehreren Azure-Abonnements](../azure-best-practices/scaling-subscriptions.md) finden Sie ausführliche Informationen zur Organisation von Ressourcen basierend auf mehreren Kriterien zur Schaffung einer gut verwalteten Umgebung. In diesem Artikel geht es um die Anwendung von grundlegenden Azure-Konzepten, um für die Cloudkosten Transparenz zu erzielen.

### <a name="classification"></a>Klassifizierung

*Tagging* ist eine einfache Möglichkeit zum Klassifizieren von Ressourcen. Beim Tagging werden einer Ressource Metadaten zugeordnet. Diese Metadaten können verwendet werden, um die Ressource anhand verschiedener Datenpunkte zu klassifizieren. Wenn Tags im Rahmen einer Aufgabe für die Kostenverwaltung zum Klassifizieren von Ressourcen verwendet werden, benötigen Unternehmen häufig die folgenden Tags: Geschäftseinheit, Abteilung, Abrechnungscode, Geografie, Umgebung, Projekt, Workload oder „Anwendungskategorisierung“. Azure Cost Management kann diese Tags zum Erstellen von verschiedenen Ansichten der Kostendaten verwenden.

Das Tagging ist das wichtigste Verahren, wenn es um das Verständnis der Daten im Rahmen der Kostenberichterstattung geht. Es ist ein wesentlicher Bestandteil jeder gut verwalteten Umgebung. Darüber hinaus ist dies der erste Schritt zur Erzielung von Governance für eine Umgebung.

Um Kosteninformationen übergreifend für Geschäftseinheiten, Umgebungen und Projekte genau nachverfolgen zu können, muss zunächst ein Standard für das Tagging definiert werden. Im zweiten Schritt wird sichergestellt, dass dieser Standard für das Tagging einheitlich angewendet wird. Die Artikel zu den folgenden Themen enthalten Informationen zu diesen Schritten:

- [Entwickeln von Standards für Benennung und Tagging](../azure-best-practices/naming-and-tagging.md)
- [Einrichten eines Governance-MVP zum Erzwingen von Standards für das Tagging](../../govern/guides/complex/index.md)

### <a name="resource-organization"></a>Ressourcenorganisation

Es gibt mehrere Ansätze zum Organisieren von Ressourcen. In diesem folgenden Abschnitt wird eine bewährte Methode anhand der Anforderungen eines großen Unternehmens beschrieben, dessen Kostenstrukturen auf Geschäftseinheiten, geografische Regionen und IT-Organisationen verteilt sind. Eine ähnliche bewährte Methode für eine kleinere, weniger komplexe Organisation finden Sie unter [Governanceleitfaden für Standardunternehmen](../../govern/guides/standard/index.md).

Bei einem großen Unternehmen erstellt das folgende Modell für Verwaltungsgruppen, Abonnements und Ressourcengruppen eine Hierarchie, die jedem Team die richtige Transparenz zum Ausführen seiner Aufgaben ermöglicht. Wenn das Unternehmen Kostenkontrolle benötigt, um eine Budgetüberschreitung zu verhindern, kann es Governancetools wie Azure Blueprints oder Azure Policy auf die Abonnements der Struktur anwenden, um zukünftige Fehler bei den Kosten zu vermeiden.

![Abbildung der Ressourcenorganisation für ein großes Unternehmen](../../_images/govern/large-enterprise-resource-organization.png)

In der Abbildung obem enthält der Stamm der Hierarchie mit den Verwaltungsgruppen jeweils einen Knoten pro Geschäftseinheit. In diesem Beispiel benötigt ein multinationales Unternehmen transparenten Einblick in die regionalen Geschäftseinheiten, und für jede Geschäftseinheit der Hierarchie wird ein Knoten für eine geografische Region erstellt.

Jede geografische Region enthält einen separaten Knoten für Produktionsumgebungen und andere Umgebungen, um die Steuerung der Kosten, des Zugriffs und der Governance zu isolieren. Damit effizientere Abläufe ermöglicht und bessere Investitionsentscheidungen getroffen werden können, verwendet das Unternehmen Abonnements, um Produktionsumgebungen weiter zu isolieren – mit unterschiedlichen Zusicherungen in Bezug auf die betriebliche Leistung. Schließlich verwendet das Unternehmen Ressourcengruppen, um bereitstellbare Funktionseinheiten zu erfassen, die Anwendungen genannt werden.

Die Abbildung zeigt bewährte Methoden, enthält jedoch nicht die folgenden Optionen:

- Viele Unternehmen beschränken Vorgänge auf eine einzelne geopolitische Region. Diese Vorgehensweise verringert die Notwendigkeit, Governancedisziplinen oder Kostendaten basierend auf den Anforderungen an die lokale Datenhoheit zu diversifizieren. In diesen Fällen ist kein Geografieknoten erforderlich.
- Einige Unternehmen ziehen es vor, Umgebungen für die Entwicklung, Tests und die Qualitätslenkung weiter auf separate Abonnements aufzuteilen.
- Beim Integrieren eines Cloudkompetenzzentrum-Teams (Cloud Center of Excellence, CCoE) durch ein Unternehmen können Abonnements mit gemeinsamen Diensten in jedem Geografieknoten eine Duplizierung von Ressourcen vermeiden.
- Weniger umfangreiche Einführungsprojekte verfügen ggf. über eine viel kleinere Verwaltungshierarchie. Es kommt häufig vor, dass nur ein einzelner Stammknoten für die IP-Abteilung des Unternehmens und nur eine Ebene mit untergeordneten Knoten in der Hierarchie für unterschiedliche Umgebungen vorhanden ist. Dies ist keine Verletzung von bewährten Methoden für eine gut verwaltete Umgebung. Aber die Bereitstellung eines Zugriffsmodells mit den geringstmöglichen Rechten für die Kostenkontrolle und andere wichtige Funktionen wird erschwert.

Im restlichen Artikel wird vorausgesetzt, dass der Ansatz mit der bewährten Methode aus der Abbildung oben verfolgt wird. Die folgenden Artikel enthalten hilfreiche Informationen zum Anwenden des Ansatzes für die Ressourcenorganisation, der für Ihr Unternehmen am besten geeignet ist:

- [Skalieren mit mehreren Azure-Abonnements](../azure-best-practices/scaling-subscriptions.md)
- [Deploying a Governance MVP to govern well-managed environment standards](../../govern/guides/complex/index.md) (Bereitstellen eines Governance-MVP zur Steuerung von Standards für gut verwaltete Umgebungen)

## <a name="provide-the-right-level-of-cost-access"></a>Ermöglichen eines angemessenen Zugriffs auf die Kosten

Die Verwaltung der Kosten ist eine Teamaktivität. Im Abschnitt zur Bereitschaft von Organisationen des Frameworks für die Cloudeinführung (Cloud Adoption Framework) ist eine geringe Anzahl von Kernteams definiert. Es wird beschrieben, wie diese Teams die Schritte der Cloudeinführung unterstützen. In diesem Artikel werden die Teamdefinitionen eingehender erläutert, um den Bereich und die Rollen zu definieren, die den Mitgliedern der einzelnen Teams zugewiesen werden müssen, um für die Kostenverwaltungsdaten den richtigen Transparenzgrad zu erzielen.

- Mit *Rollen* wird definiert, welche Schritte ein Benutzer für verschiedene Ressourcen ausführen kann.
- *Bereich* definiert, für welche Ressourcen (Benutzer, Gruppe, Dienstprinzipal oder verwaltete Identität) ein Benutzer diese Aufgaben ausführen kann.

Die generell empfohlene bewährte Methode besteht darin, ein Modell mit geringstmöglichen Rechten zu verwenden, um Personen verschiedenen Rollen und Bereichen zuzuweisen.

### <a name="roles"></a>Rollen

Azure Cost Management unterstützt für jeden der Bereiche die folgenden integrierten Rollen:

- [Besitzer](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner). Ermöglicht das Anzeigen von Kosten und das Verwalten sämtlicher Aspekte, einschließlich Kostenkonfiguration.
- [Mitwirkender](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor). Ermöglicht das Anzeigen von Kosten und das Verwalten sämtlicher Aspekte, z. B. der Kostenkonfiguration, aber ausschließlich der Zugriffssteuerung.
- [Leser](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#reader). Ermöglicht das Anzeigen sämtlicher Daten, z.B. der Kostendaten und Konfiguration, aber nicht das Vornehmen von Änderungen.
- [Cost Management: Mitwirkender](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#cost-management-contributor). Ermöglicht das Anzeigen der Kosten und das Verwalten der Kostenkonfiguration.
- [Cost Management: Leser](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#cost-management-reader): Ermöglicht das Anzeigen der Kostendaten und der Konfiguration.

Die allgemeine bewährte Methode besteht darin, Mitgliedern aller Teams die Rolle „Kostenverwaltung: Mitwirkender“ zuzuweisen. Mit dieser Rolle wird der Zugriff für die Erstellung und Verwaltung von Budgets und Exporten gewährt, um die Kosten effektiver zu überwachen und zu dokumentieren. Mitglieder des [Cloudstrategieteams](../../organize/cloud-strategy.md) sollten jedoch nur auf „Cost Management: Leser“ festgelegt werden. Das liegt daran, dass Sie nicht am Einrichten von Budgets innerhalb des Azure Cost Management-Tools beteiligt sind.

### <a name="scope"></a>`Scope`

Mit den folgenden Bereichs- und Rolleneinstellungen wird die erforderliche Transparenz in Cost Management geschaffen. Bei dieser bewährten Methode sind ggf. einige geringfügige Änderungen erforderlich, um eine Ausrichtung auf die Entscheidungen zu erzielen, die im Hinblick auf die Ressourcenorganisation getroffen wurden.

- [Cloudeinführungsteam](../../organize/cloud-adoption.md). Personen, die für die Durchführung von Änderungen im Rahmen der fortlaufenden Optimierung verantwortlich sind, benötigen Zugriff vom Typ „Cost Management: Mitwirkender“ auf Ressourcengruppenebene.

  - **Arbeitsumgebung**: Das Cloudeinführungsteam sollte bereits über Zugriff vom Typ [Mitwirkender](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor) auf alle betroffenen Ressourcengruppen oder zumindest auf die Gruppen verfügen, die für die Entwicklung bzw. das Testen oder die Aktivitäten zur fortlaufenden Bereitstellung zuständig sind. Es ist keine zusätzliche Bereichseinstellung erforderlich.
  - **Produktionsumgebungen**: Wenn eine geeignete Trennung der Zuständigkeiten erzielt wurde, ist es eher unwahrscheinlich, dass das Cloudeinführungsteam weiterhin Zugriff auf die Ressourcengruppen seiner Projekte hat. Für die Ressourcengruppen, die die Produktionsinstanzen ihrer Workloads unterstützen, wird ein zusätzlicher Bereich benötigt, damit dieses Team über Einblick in die Auswirkungen seiner Entscheidungen auf die Produktionskosten verfügt. Die Festlegung des Bereichs [Cost Management: Mitwirkender](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#cost-management-contributor) für Produktionsressourcengruppen für dieses Team ermöglicht den Mitgliedern das Überwachen von Kosten und das Festlegen von Budgets basierend auf der Nutzung und den fortlaufenden Investitionen in die unterstützten Workloads.

- [Cloudstrategieteam](../../organize/cloud-strategy.md). Personen, die für die übergreifende Nachverfolgung der Kosten für mehrere Projekte und Geschäftsbereiche zuständig sind, benötigen Zugriff vom Typ „Cost Management: Leser“ auf der Stammebene der Verwaltungsgruppenhierarchie.

  - Weisen Sie diesem Team für die Verwaltungsgruppe Zugriff vom Typ [Kostenverwaltung: Leser](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#cost-management-reader) zu. So wird sichergestellt, dass fortlaufend transparenter Einblick in alle Bereitstellungen besteht, die den mit dieser Verwaltungsgruppenhierarchie gesteuerten Abonnements zugeordnet sind.

- [Cloudgovernanceteam](../../organize/cloud-governance.md). Personen, die für die Verwaltung von Kosten, die Budgetausrichtung und die Berichterstellung für alle Einführungsaufgaben zuständig sind, benötigen Zugriff vom Typ „Cost Management: Mitwirkender“ auf der Stammebene der Verwaltungsgruppenhierarchie.

  - In einer gut verwalteten Umgebung verfügt das Cloudgovernanceteam vermutlich über einen höheren Zugriffsgrad, sodass eine zusätzliche Bereichszuweisung für [Cost Management: Mitwirkender](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#cost-management-contributor) nicht erforderlich ist.

- [Cloudkompetenzzentrum](../../organize/cloud-center-of-excellence.md). Personen, die für die Verwaltung von Kosten in Bezug auf gemeinsam verwendete Dienste zuständig sind, benötigen Zugriff vom Typ „Cost Management: Mitwirkender“ auf Abonnementebene. Darüber hinaus benötigt dieses Team unter Umständen auch Zugriff vom Typ „Cost Management: Mitwirkender“ auf Ressourcengruppen oder Abonnements, die per CCoE-Automatisierung bereitgestellte Ressourcen enthalten, um zu verstehen, wie sich diese Automatisierungen auf die Kosten auswirken.

  - **Gemeinsame Dienste**: Bei Einbindung eines Cloudkompetenzzentrums besteht die bewährte Methode darin, dass die über das Zentrum verwalteten Ressourcen mit einem zentralisierten Abonnement für gemeinsame Dienste im Rahmen eines Hub-and-Spoke-Modells unterstützt werden. In diesem Szenario verfügt das CCoE meist über Zugriff vom Typ „Mitwirkender“ oder „Besitzer“ auf dieses Abonnement, sodass es nicht erforderlich ist, zusätzlich [Kostenverwaltung: Mitwirkender](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#cost-management-contributor) zuzuweisen.
  - **CCoE-Automatisierung/-Steuerung**. Vom CCoE werden für Cloudeinführungsteams normalerweise Steuerungen und automatisierte Bereitstellungsskripts bereitgestellt. Das CCoE ist dafür verantwortlich, ein Verständnis zu entwickeln, wie sich diese Beschleunigungselemente (Accelerators) auf die Kosten auswirken. Um sich diesen Einblick zu verschaffen, benötigt das Team Zugriff vom Typ [Kostenverwaltung: Mitwirkender](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#cost-management-contributor) auf alle Ressourcengruppen oder Abonnements, unter denen diese Accelerators ausgeführt werden.

- **Cloudbetriebsteam**: Personen, die für die Verwaltung der laufenden Kosten von Produktionsumgebungen zuständig sind, benötigen Zugriff vom Typ „Cost Management: Mitwirkender“ auf alle Produktionsabonnements.

  - Die allgemeine Empfehlung besteht darin, Produktions- und Nichtproduktionsressourcen in separaten Abonnements zu platzieren, deren Steuerung über die Knoten der Verwaltungsgruppenhierarchie erfolgt, die Produktionsumgebungen zugeordnet sind. In einer gut verwalteten Umgebung verfügen Mitglieder des Betriebsteams meist bereits über Zugriff vom Typ „Besitzer“ oder „Mitwirkender“ auf Produktionsabonnements, sodass die Rolle [Cost Management: Mitwirkender](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#cost-management-contributor) nicht benötigt wird.

## <a name="additional-cost-management-resources"></a>Zusätzliche Ressourcen für die Kostenverwaltung

Azure Cost Management ist ein gut dokumentiertes Tool zum Festlegen von Budgets und Erhalten von Einblick in die Cloudkosten für Azure oder AWS. Nachdem Sie Zugriff auf eine gut verwaltete Umgebungshierarchie eingerichtet haben, helfen Ihnen die folgenden Artikel weiter, wenn es um die Verwendung dieses Tools zum Überwachen und Kontrollieren von Kosten geht.

### <a name="get-started-with-azure-cost-management"></a>Erste Schritte mit Azure Cost Management

Weitere Informationen zu den ersten Schritten mit Azure Cost Management finden Sie unter [Optimieren der Cloudinvestitionen mit Azure Cost Management](https://docs.microsoft.com/azure/cost-management/cost-mgt-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json).

### <a name="use-azure-cost-management"></a>Azure Cost Management verwenden

- [Erstellen und Verwalten von Budgets](https://docs.microsoft.com/azure/cost-management/tutorial-acm-create-budgets)
- [Exportieren von Kostendaten](https://docs.microsoft.com/azure/cost-management/tutorial-export-acm-data)
- [Optimieren von Kosten anhand von Empfehlungen](https://docs.microsoft.com/azure/cost-management/tutorial-acm-opt-recommendations)
- [Verwenden von Kostenwarnungen zum Überwachen von Verbrauch und Ausgaben](https://docs.microsoft.com/azure/cost-management/cost-mgt-alerts-monitor-usage-spending)

### <a name="use-azure-cost-management-to-govern-aws-costs"></a>Verwenden von Azure Cost Management zum Steuern von AWS-Kosten

- [Einrichten und Konfigurieren der Integration von AWS-Kosten- und -Nutzungsberichten](https://docs.microsoft.com/azure/cost-management-billing/costs/aws-integration-set-up-configure)
- [Verwalten von AWS-Kosten](https://docs.microsoft.com/azure/cost-management/aws-integration-manage)

### <a name="establish-access-roles-and-scope"></a>Einrichten von Zugriff, Rollen und Bereich

- [Verstehen von und Arbeiten mit Bereichen](https://docs.microsoft.com/azure/cost-management/understand-work-scopes)
- [Tutorial: Gewähren des Zugriffs auf Azure-Ressourcen für einen Benutzer mit RBAC und dem Azure-Portal](https://docs.microsoft.com/azure/role-based-access-control/quickstart-assign-role-user-portal)
