---
title: Bewerten der digitalen Ressourcen
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Bewerten der digitalen Ressourcen
author: matticusau
ms.author: mlavery
ms.date: 08/08/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 27fa0720308910db32a340943f584a4502f52e94
ms.sourcegitcommit: 6f287276650e731163047f543d23581d8fb6e204
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/07/2019
ms.locfileid: "73753588"
---
# <a name="assess-the-digital-estate"></a>Bewerten der digitalen Ressourcen

Bei einer idealen Migration wäre jede Ressource (Infrastruktur, App oder Daten) mit einer Cloudplattform kompatibel und migrationsfähig. In der Praxis sollte jedoch nicht alles in die Cloud migriert werden. Außerdem ist nicht jede Ressource mit Cloudplattformen kompatibel. Vor der Migration einer Workload in die Cloud ist es wichtig, die Workload und alle zugehörigen Ressourcen (Infrastruktur, Apps und Daten) zu bewerten.

Anhand der Ressourcen in diesem Abschnitt können Sie Ihre Umgebung bewerten, um die Eignung für die Migration und die zu berücksichtigenden Methoden zu bestimmen.

<!-- markdownlint-disable MD025 -->

# <a name="toolstabtools"></a>[Tools](#tab/Tools)

Mit den folgenden Tools können Sie Ihre Umgebung bewerten, um die Eignung für die Migration und die beste zu verwendende Methode zu bestimmen. Hilfreiche Informationen zur Auswahl der richtigen Tools zur Unterstützung der Migration finden Sie im [Leitfaden zur Entscheidungsfindung für Migrationstools des Frameworks für die Cloudeinführung (Cloud Adoption Framework)](../../decision-guides/migrate-decision-guide/index.md).

## <a name="azure-migrate"></a>Azure Migrate

Mit dem Dienst Azure Migrate werden die lokale Infrastruktur, Anwendungen und Daten für die Migration zu Azure bewertet. Der Dienst bewertet die Migrationseignung lokaler Ressourcen, führt die leistungsbasierte Größenauslegung durch und stellt Kostenschätzungen für die Ausführung Ihrer lokalen Ressourcen in Azure bereit. Wenn Sie die Nutzung von Lift & Shift-Migrationen erwägen oder sich in einer frühen Bewertungsphase der Migration befinden, ist dieser Dienst gut für Sie geeignet. Nach Abschluss der Bewertung kann Azure Migrate verwendet werden, um die Migration auszuführen.

![Übersicht über Azure Migrate](./media/assess/azuremigrate-overview-1.png)

### <a name="create-a-new-server-migration-project"></a>Erstellen eines neuen Servermigrationsprojekts

Führen Sie diese Schritte aus, um mit Azure Migrate mit einer Servermigrationsbewertung zu beginnen:

1. Wählen Sie **Azure Migrate** aus.
1. Klicken Sie in der **Übersicht** auf **Server bewerten und migrieren**.
1. Wählen Sie **Hinzufügen** aus.
1. Klicken Sie unter **Server ermitteln, bewerten und migrieren** auf **Tools hinzufügen**.
1. Wählen Sie unter **Projekt migrieren** Ihr Azure-Abonnement aus, und erstellen Sie bei Bedarf eine Ressourcengruppe.
1. Geben Sie unter **Projektdetails** den Projektnamen und die geografische Region an, in der Sie das Projekt erstellen möchten. Klicken Sie anschließend auf **Weiter**.
1. Wählen Sie unter **Bewertungstool auswählen** die Option **Hinzufügen eines Bewertungstools vorerst überspringen > Weiter** aus.
1. Wählen Sie unter **Migrationstool auswählen** Folgendes aus: **Azure Migrate: Servermigrationsziel > Weiter**.
1. Überprüfen Sie die Einstellungen unter **Überprüfen + Tools hinzufügen**, und klicken Sie auf **Tools hinzufügen**.
1. Nachdem Sie das Tool hinzugefügt haben, wird es unter **Azure Migrate-Projekt > Server > Migrationstools** angezeigt.

::: zone target="chromeless"

::: form action="Blade[#blade/Microsoft_Azure_Migrate/AmhResourceMenuBlade/overview]" submitText="Assess and migrate servers" :::

::: zone-end

::: zone target="docs"

### <a name="learn-more"></a>Weitere Informationen

- [Übersicht über Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-services-overview)
- [Migrieren von physischen oder virtuellen Servern zu Azure](https://docs.microsoft.com/azure/migrate/tutorial-migrate-physical-virtual-machines)
- [Azure Migrate im Azure-Portal](https://portal.azure.com/#blade/Microsoft_Azure_Migrate/AmhResourceMenuBlade/overview)

::: zone-end

## <a name="service-map"></a>Dienstzuordnung

Service Map ermittelt automatisch Anwendungskomponenten auf Windows- und Linux-Systemen und stellt die Kommunikation zwischen Diensten dar. Mit Service Map können Sie die Server Ihrer Vorstellung gemäß anzeigen – als verbundene Systeme, die wichtige Dienste bereitstellen. Dienstzuordnung zeigt Verbindungen zwischen Servern, Prozessen, ein- und ausgehende Verbindungslatenz und Ports über die gesamte TCP-Verbindungsarchitektur an. Außer der Installation eines Agents ist keine weitere Konfiguration erforderlich.

Für Azure Migrate wird die Dienstzuordnung verwendet, um die Berichterstellungsfunktionen und Abhängigkeiten für die Umgebung zu verbessern. Diese Integration ist unter [Visualisierung von Abhängigkeiten](https://docs.microsoft.com/azure/migrate/concepts-dependency-visualization) ausführlich beschrieben. Wenn Sie den Azure Migrate-Dienst verwenden, können Sie ohne weitere Schritte die Dienstzuordnung konfigurieren und ihre Vorteile nutzen. Die folgenden Anweisungen dienen als Referenz, falls Sie die Dienstzuordnung für andere Zwecke oder Projekte verwenden möchten.

### <a name="enable-dependency-visualization-using-service-map"></a>Aktivieren der Visualisierung von Abhängigkeiten mithilfe der Dienstzuordnung

Zur Verwendung der Abhängigkeitsvisualisierung müssen Sie Agents auf alle lokalen Computer, die Sie analysieren möchten, herunterladen und dort installieren.

- Der [Microsoft Monitoring Agent (MMA)](https://docs.microsoft.com/azure/log-analytics/log-analytics-agent-windows) muss auf jedem Computer installiert werden.
- Der [Microsoft Dependency-Agent](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-enable-hybrid-cloud#install-the-dependency-agent-on-windows) muss auf jedem Computer installiert werden.
- Falls Sie über Computer ohne Internetverbindung verfügen, ist es außerdem erforderlich, auf diesen das Log Analytics-Gateway herunterzuladen und zu installieren.

<!-- markdownlint-disable MD024 -->

### <a name="learn-more"></a>Weitere Informationen

- [Verwenden der Dienstzuordnungslösung in Azure](https://docs.microsoft.com/azure/azure-monitor/insights/service-map)
- [Azure Migrate und Dienstzuordnung: Visualisierung von Abhängigkeiten](https://docs.microsoft.com/azure/migrate/concepts-dependency-visualization)

# <a name="scenarios-and-stakeholderstabscenarios"></a>[Szenarien und Beteiligte](#tab/Scenarios)

## <a name="scenarios"></a>Szenarien

Dieser Leitfaden konzentriert sich auf die folgenden Szenarien:

- **Ältere Hardware:** Sie führen die Migration durch, um eine Abhängigkeit von älterer Hardware zu entfernen, deren Support oder Lebensdauer bald endet.
- **Kapazitätserweiterung:** Sie möchten die Kapazität für Ressourcen (Infrastruktur, Apps und Daten), erhöhen, die in der aktuellen Infrastruktur nicht ausreichend bereitgestellt werden kann.
- **Modernisierung des Rechenzentrums:** Sie möchten Ihr Rechenzentrum erweitern oder mit Cloudtechnologie modernisieren, um sicherzustellen, dass Ihr Unternehmen modern und wettbewerbsfähig bleibt.
- **Anwendungs- oder Dienstmodernisierung:** Sie möchten Ihre Anwendungen aktualisieren, um cloudnative Funktionen nutzen zu können. Auch wenn eine Migration mit Rehostingstrategie Ihr ursprüngliches Ziel ist, stellt die Möglichkeit, Pläne für die Überprüfung von Anwendungen oder Diensten und für eine potenzielle Modernisierung zu erstellen, einen gängigen Vorgang bei jeder Migration dar.

### <a name="organizational-alignment-and-stakeholders"></a>Ausrichtung der Organisation und Projektbeteiligte

Die vollständige Liste der Projektbeteiligten variiert je nach Migrationsprojekt. Am ehesten ist davon auszugehen, dass Sie zu Beginn der Planung einer Migration nicht alle Projektbeteiligten kennen, da Projektbeteiligte oft erst in bestimmten Projektphasen identifiziert werden. Vor Beginn von Migrationsprojekten können Sie jedoch wichtige Führungskräfte der Finanz-, IT-Infrastruktur- und Anwendungsgruppen identifizieren, die ein Interesse an den gesamten Cloudmigrationsaktivitäten Ihres Unternehmens haben.

Durch den Aufbau eines Cloudstrategieteams aus diesen wichtigen Projektbeteiligten auf höchster Ebene können Sie Ihr Unternehmen auf die Cloudeinführung vorbereiten und Ihre gesamten Cloudmigrationsaktivitäten steuern. Dieses Team ist zuständig für die Einschätzung von Cloudtechnologien und Migrationsprozessen, die Identifizierung der geschäftlichen Begründung für Migrationen und die Festlegung der besten allgemeinen Lösungen für Migrationsmaßnahmen. Das Team hilft auch bei der Identifizierung und Zusammenarbeit mit spezifischen Projektbeteiligten von Anwendungen und des Unternehmens, um eine erfolgreiche Migration zu gewährleisten.

Weitere Informationen zur Vorbereitung Ihrer Organisation auf die Cloudmigration finden Sie im Artikel [Erstausrichtung der Organisation](../../plan/initial-org-alignment.md) des Frameworks für die Cloudeinführung.

# <a name="timelinestabtimelines"></a>[Zeitpläne](#tab/Timelines)

Allgemein lässt sich sagen, dass Kunden das in dieser Anleitung beschriebene Migrationsszenario in einem bis sechs Monaten umsetzen können.

Bei der Bewertung des Zeitplans der Migration sind u. a. folgende Faktoren zu berücksichtigen:

- **Zu migrierende Ressourcen (Infrastruktur, Apps und Daten):** Anzahl und Vielfalt der Ressourcen.
- **Bereitschaft der Mitarbeiter:** Sind Ihre Mitarbeiter in der Lage, die neue Umgebung zu verwalten, oder benötigen sie Schulungen?
- **Finanzierung:** Verfügen Sie über die entsprechende Genehmigung und das entsprechende Budget für die Migration?
- **Change Management:** Hat Ihr Unternehmen spezifische Anforderungen an die Implementierung und Genehmigung von Änderungen?
- **Branchenvorschriften:** Müssen Sie Segment- oder Branchenvorschriften einhalten?

# <a name="cost-managementtabmanagecost"></a>[Cost Management](#tab/ManageCost)

Die Bewertung Ihrer Umgebung bietet eine ideale Gelegenheit, auch die Kostenanalyse einzubinden. Anhand der bei den Bewertungsprozessen erfassten Daten sollten Sie in der Lage sein, die Kosten zu analysieren und vorherzusagen. Diese Kostenvorhersage sollte sowohl die verbrauchsbasierten Dienstkosten als auch alle einmaligen Kosten (z. B. erhöhter Dateneingang) berücksichtigen.

Während der Migration wirken sich bestimmte Faktoren auf Entscheidungen und Ausführungsaktivitäten aus:

- **Größe der digitalen Ressourcen:** Die Kenntnis der Größe Ihrer digitalen Ressourcen hat direkten Einfluss auf Entscheidungen und die für die Durchführung der Migration erforderlichen Ressourcen.
- **Kostenrechnungsmodelle:** Wechsel von einem strukturierten Investitionskostenmodell zu einem fließenden Betriebskostenmodell.

::: zone target="docs"

Entsprechende Informationen finden Sie in den folgenden Ressourcen:

- [Schätzen der Cloudkosten](../migration-considerations/assess/estimate.md)

::: zone-end
