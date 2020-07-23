---
title: Bewerten der einzelnen Workloads und Optimieren von Plänen
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um zu bewerten, wie gut Ihre Umgebung für die Migration geeignet ist und welche Methoden beachtet werden sollten.
author: matticusau
ms.author: mlavery
ms.date: 02/25/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 0a3288c992c09ebd4da7285225da7b295b1cc626
ms.sourcegitcommit: 08d6d5bda45814745fc181b0a07bcb8c415bf342
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/14/2020
ms.locfileid: "86373049"
---
# <a name="assess-workloads-and-refine-plans"></a>Bewerten von Workloads und Optimieren von Plänen

Die Ressourcen in diesem Handbuch helfen Ihnen, die einzelnen Workloads zu bewerten, Annahmen über die Eignung der einzelnen Workloads für die Migration zu hinterfragen und anschließend Architekturentscheidungen zu Migrationsoptionen zu treffen.

<!-- markdownlint-disable MD025 -->

## <a name="tools"></a>[Tools](#tab/Tools)

Wenn Sie die Anweisungen in den obigen Links nicht befolgt haben, benötigen Sie wahrscheinlich Daten und ein Bewertungstool, um fundierte Migrationsentscheidungen treffen zu können. Azure Migrate ist das native Tool für die Bewertung **und** die Migration zu Azure. Führen Sie diese Schritte aus (sofern nicht bereits geschehen), um ein neues Servermigrationsprojekt zu erstellen und die erforderlichen Daten zu erfassen.

### <a name="azure-migrate"></a>Azure Migrate

Mit Azure Migrate werden die lokale Infrastrukturen, Anwendungen und Daten für die Migration zu Azure bewertet. Dieser Dienst:

- Bewertet die Migrationstauglichkeit lokaler Ressourcen
- Führt eine leistungsbasierte Größenanpassung durch
- Bietet Kostenschätzungen für die Ausführung lokaler Ressourcen in Azure

Wenn Sie einen Lift & Shift-Ansatz verwenden möchten oder sich in einer frühen Bewertungsphase der Migration befinden, ist dieser Dienst gut für Sie geeignet. Nach Abschluss der Bewertung kann Azure Migrate verwendet werden, um die Migration auszuführen.

![Übersicht über Azure Migrate](./media/assess/azure-migrate-overview-1.png)

#### <a name="create-a-new-server-migration-project"></a>Erstellen eines neuen Servermigrationsprojekts

Führen Sie diese Schritte aus, um mit Azure Migrate mit einer Servermigrationsbewertung zu beginnen:

1. Wählen Sie **Azure Migrate** aus.
1. Wählen Sie in der **Übersicht** die Option **Server bewerten und migrieren** aus.
1. Wählen Sie **Hinzufügen** aus.
1. Wählen Sie unter **Server ermitteln, bewerten und migrieren** die Option **Tools hinzufügen** aus.
1. Wählen Sie unter **Projekt migrieren** Ihr Azure-Abonnement aus, und erstellen Sie anschließend bei Bedarf eine Ressourcengruppe.
1. Geben Sie unter **Projektdetails** den Projektnamen und die geografische Region an, in der Sie das Projekt erstellen möchten. Wählen Sie anschließend **Weiter** aus.
1. Wählen Sie unter **Bewertungstool auswählen** die Option **Hinzufügen eines Bewertungstools vorerst überspringen** >  und anschließend **Weiter** aus.
1. Wählen Sie unter **Migrationstool auswählen** Folgendes aus: **Azure Migrate: Servermigration** > **Weiter**.
1. Überprüfen Sie die Einstellungen unter **Überprüfen + Tools hinzufügen**, und wählen Sie anschließend **Tools hinzufügen** aus.
1. Nachdem Sie das Tool hinzugefügt haben, wird es unter **Azure Migrate-Projekt** > **Server** > **Migrationstools** angezeigt.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Migrate/AmhResourceMenuBlade/overview]" submitText="Assess and migrate servers" :::

::: zone-end

::: zone target="docs"

#### <a name="learn-more"></a>Weitere Informationen

- [Übersicht über Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-services-overview)
- [Migrieren von physischen oder virtuellen Servern zu Azure](https://docs.microsoft.com/azure/migrate/tutorial-migrate-physical-virtual-machines)
- [Azure Migrate im Azure-Portal](https://portal.azure.com/#blade/Microsoft_Azure_Migrate/AmhResourceMenuBlade/overview)

::: zone-end

### <a name="service-map"></a>Dienstzuordnung

Service Map ermittelt automatisch Anwendungskomponenten auf Windows- und Linux-Systemen und stellt die Kommunikation zwischen Diensten dar. Mit Service Map können Sie die Server Ihrer Vorstellung gemäß anzeigen – als verbundene Systeme, die wichtige Dienste bereitstellen. Dienstzuordnung zeigt Verbindungen zwischen Servern, Prozessen, ein- und ausgehende Verbindungslatenz und Ports über die gesamte TCP-Verbindungsarchitektur an. Außer der Installation eines Agents ist keine weitere Konfiguration erforderlich.

Für Azure Migrate wird die Dienstzuordnung verwendet, um die Berichterstellungsfunktionen und Abhängigkeiten für die Umgebung zu verbessern. Diese Integration ist unter [Visualisierung von Abhängigkeiten](https://docs.microsoft.com/azure/migrate/concepts-dependency-visualization) ausführlich beschrieben. Wenn Sie den Azure Migrate-Dienst verwenden, können Sie ohne weitere Schritte die Dienstzuordnung konfigurieren und ihre Vorteile nutzen. Die folgenden Anweisungen dienen als Referenz, falls Sie die Dienstzuordnung für andere Zwecke oder Projekte verwenden möchten.

#### <a name="enable-dependency-visualization-using-service-map"></a>Aktivieren der Visualisierung von Abhängigkeiten mithilfe der Dienstzuordnung

Zur Verwendung der Visualisierung von Abhängigkeiten müssen Sie Agents auf alle lokalen Computer, die Sie analysieren möchten, herunterladen und dort installieren.

- Der [Microsoft Monitoring Agent](https://docs.microsoft.com/azure/log-analytics/log-analytics-agent-windows) muss auf jedem Computer installiert werden.
- Der [Microsoft Dependency-Agent](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-enable-hybrid-cloud#install-the-dependency-agent-on-windows) muss auf jedem Computer installiert werden.
- Falls Sie über Computer ohne Internetverbindung verfügen, ist es erforderlich, auf diese das Log Analytics-Gateway herunterzuladen und dort zu installieren.

<!-- markdownlint-disable MD024 -->

#### <a name="learn-more"></a>Weitere Informationen

- [Verwenden der Dienstzuordnungslösung in Azure](https://docs.microsoft.com/azure/azure-monitor/insights/service-map)
- [Azure Migrate und Dienstzuordnung: Visualisierung von Abhängigkeiten](https://docs.microsoft.com/azure/migrate/concepts-dependency-visualization)

## <a name="challenge-assumptions"></a>[Hinterfragen von Annahmen](#tab/Challenge-Assumptions)

Bei einer idealen Migration wäre jede Ressource (Infrastruktur, App oder Daten) mit einer Cloudplattform kompatibel und migrations- oder modernisierungsfähig. In der Praxis sollte jedoch nicht jede Workload in die Cloud migriert werden. Nicht jede Ressource ist mit Cloudplattformen kompatibel. Vor der Migration einer Workload in die Cloud ist es wichtig, alle Workloads und alle zugehörigen Ressourcen (Infrastruktur, Apps und Daten) zu bewerten.

In der [Planmethodik des Cloud Adoption Framework](../../plan/index.md) wird die Verwendung der Ansätze [Inkrementelle Rationalisierung](../../digital-estate/rationalize.md#incremental-rationalization) und [Zehn Anwendungen](../../digital-estate/rationalize.md#release-planning) empfohlen, um die Migration zu bewerten und zu planen. Dieses Handbuch enthält auch eine ausführliche Beschreibung einer bewährten Methode [zum Bewerten digitaler Ressourcen mit Azure Migrate](../../plan/contoso-migration-assessment.md).

Die obigen Links deuten darauf hin, dass Annahmen akzeptabel sind und während der Planungsphase der Migration häufig empfohlen werden. Jetzt ist es jedoch an der Zeit, etwas zu tun. Diese Annahmen sollten vor der Migration zur Cloud für jede Workload hinterfragt werden.

### <a name="two-steps-of-incremental-rationalization"></a>Zwei Schritte der inkrementellen Rationalisierung

Zwei gleich wichtige Schritte sind erforderlich, um die [inkrementelle Rationalisierung](../../digital-estate/rationalize.md#incremental-rationalization) erfolgreich bereitzustellen. Beide Schritte erfordern Daten und Erkenntnisse zur Umgebung. Bei jedem Ansatz werden jedoch die Zeit und die Detailgranularität berücksichtigt, die bei einer erfolgreichen Migration erforderlich sind.

- [Releaseplanung – Zehn Anwendungen](../../digital-estate/rationalize.md#release-planning): Während der anfänglichen Rationalisierung und der Releaseplanung kommt nur eine der [fünf Phasen der Rationalisierung](../../digital-estate/5-rs-of-rationalization.md) zum Einsatz. Schätzen und planen Sie basierend auf der Rationalisierungsoption, die am besten mit den in der [Strategie- und Planungsvorlage](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx) definierten Beweggründen übereinstimmt.

- **Ausführliche Bewertung der einzelnen Workloads:** Die mit der Releaseplanung „Zehn Anwendungen“ verbundenen Annahmen sind annehmbar, um einen Plan zu erstellen. Diese Annahmen können jedoch signifikante Probleme verursachen, wenn sie vor der Migration nicht ausgewertet werden.

### <a name="challenge-assumptions-and-update-the-plan"></a>Hinterfragen von Annahmen und Aktualisieren des Plans

Überprüfen Sie die Bewertungsdaten in Azure Migrate oder dem gewählten Bewertungstool. Diese Daten bieten Erkenntnisse zu Kompatibilitätsproblemen, Wartungsanforderungen, Vorschläge zur Größenanpassung und andere Überlegungen.

Setzen Sie vor der Migration diese Daten zusammen mit den Gesprächen zur Ermittlung mit dem Produktbesitzer, den Entwicklungsteams, den Administratoren und anderen Beteiligten ein, um die Durchführbarkeit der Migration einer spezifischen Workload auszuwerten. Verwenden Sie diese Ermittlung, um grundlegende Annahmen zu dieser Workload zu hinterfragen. Wenn die Ergebnisse den Migrations- oder Einführungsplan ändern, aktualisieren Sie den Plan entsprechend.

Der erste Schritt beim Hinterfragen dieser Annahmen ist eine [Überprüfung aller fünf Phasen der Rationalisierung](../../digital-estate/rationalize.md).

- Funktioniert der angenommene Rationalisierungsansatz für diese Workload? Ist er der beste Ansatz?
- Wirkt sich eine der [physikalischen Grundlagen der Replikation](../migration-considerations/migrate/replicate.md#replication-risks---physics-of-replication) auf die Migration dieser Workload aus?
- Sind für diese Workload [Korrekturmaßnahmen](../migration-considerations/assess/evaluate.md) vor der Migration erforderlich?

Solche Fragen helfen Ihnen dabei, Annahmen zu hinterfragen und die beste Vorgehensweise für jede Workload zu ermitteln.

Eine erweiterte Liste mit Fragen und einen definierten Prozess für die Überprüfung von Annahmen finden Sie unter [Validierung von Bewertungsannahmen vor der Migration](../migration-considerations/assess/index.md).

## <a name="scenarios-and-stakeholders"></a>[Szenarien und Beteiligte](#tab/Scenarios)

### <a name="scenarios"></a>Szenarien

In diesem Leitfaden werden die folgenden Szenarien behandelt:

- **Ältere Hardware:** Sie führen die Migration durch, um eine Abhängigkeit von älterer Hardware zu entfernen, deren Support oder Lebensdauer bald endet.
- **Kapazitätserweiterung:** Sie möchten die Kapazität für Ressourcen (Infrastruktur, Apps und Daten) erhöhen, die in der aktuellen Infrastruktur nicht ausreichend bereitgestellt werden kann.
- **Modernisierung des Rechenzentrums:** Sie möchten Ihr Rechenzentrum erweitern oder mit Cloudtechnologie modernisieren, um sicherzustellen, dass Ihr Unternehmen modern und wettbewerbsfähig bleibt.
- **Anwendungs- oder Dienstmodernisierung:** Sie möchten Ihre Anwendungen aktualisieren, um cloudnative Funktionen nutzen zu können. Auch wenn eine Migration mit Rehostingstrategie Ihr ursprüngliches Ziel ist, stellt die Möglichkeit, Pläne für die Überprüfung von Anwendungen oder Diensten und für eine potenzielle Modernisierung zu erstellen, einen gängigen Vorgang bei jeder Migration dar.

### <a name="organizational-alignment-and-stakeholders"></a>Ausrichtung der Organisation und Projektbeteiligte

Die vollständige Liste der Projektbeteiligten variiert je nach Migrationsprojekt. Am ehesten ist davon auszugehen, dass Sie zu Beginn der Planung einer Migration nicht alle Projektbeteiligten kennen, da Projektbeteiligte oft erst in bestimmten Projektphasen identifiziert werden. Vor Beginn von Migrationsprojekten können Sie jedoch wichtige Führungskräfte der Finanz-, IT-Infrastruktur- und Anwendungsgruppen identifizieren, die an den gesamten Cloudmigrationsaktivitäten Ihres Unternehmens beteiligt sind.

Durch den Aufbau eines Cloudstrategieteams aus diesen wichtigen Projektbeteiligten auf höchster Ebene können Sie Ihr Unternehmen auf die Cloudeinführung vorbereiten und Ihre gesamten Cloudmigrationsaktivitäten steuern. Dieses Team ist zuständig für die Einschätzung von Cloudtechnologien und Migrationsprozessen, die Identifizierung der geschäftlichen Begründung für Migrationen und die Festlegung der besten allgemeinen Lösungen für Migrationsmaßnahmen. Das Team hilft auch bei der Identifizierung und Zusammenarbeit mit spezifischen Projektbeteiligten von Anwendungen und des Unternehmens, um eine erfolgreiche Migration zu gewährleisten.

Weitere Informationen zur Vorbereitung Ihrer Organisation auf die Cloudmigration finden Sie unter [Erstausrichtung der Organisation](../../plan/initial-org-alignment.md) des Frameworks für die Cloudeinführung.

## <a name="timelines"></a>[Zeitpläne](#tab/Timelines)

Kunden können das in dieser Anleitung beschriebene Migrationsszenario in der Regel in einem bis sechs Monaten umsetzen.

Bei der Bewertung des Zeitplans der Migration ist u. a.Folgendes zu berücksichtigen:

- **Zu migrierende Ressourcen (Infrastruktur, Apps und Daten):** Anzahl und Vielfalt der Ressourcen.
- **Bereitschaft der Mitarbeiter:** Sind Ihre Mitarbeiter in der Lage, die neue Umgebung zu verwalten, oder benötigen sie Schulungen?
- **Finanzierung:** Verfügen Sie über die entsprechende Genehmigung und das entsprechende Budget für die Migration?
- **Change Management:** Hat Ihr Unternehmen spezifische Anforderungen an die Implementierung und Genehmigung von Änderungen?
- **Branchenvorschriften:** Müssen Sie Segment- oder Branchenvorschriften einhalten?

## <a name="cost-management"></a>[Kostenmanagement](#tab/ManageCost)

Die Bewertung Ihrer Umgebung ist eine Möglichkeit, um einen Schritt zur Kostenanalyse einzuschließen. Anhand der bei den Bewertungsprozessen erfassten Daten sollten Sie in der Lage sein, die Kosten zu analysieren und vorherzusagen. Diese Kostenvorhersage sollte sowohl die verbrauchsbasierten Dienstkosten als auch alle einmaligen Kosten (z. B. erhöhter Dateneingang) berücksichtigen.

Während der Migration wirken sich bestimmte Faktoren auf Entscheidungen und Ausführungsaktivitäten aus:

- **Größe der digitalen Ressourcen:** Die Kenntnis der Größe Ihrer digitalen Ressourcen hat direkten Einfluss auf Entscheidungen und die für die Durchführung der Migration erforderlichen Ressourcen.
- **Kostenrechnungsmodelle:** Wechsel von einem strukturierten Investitionskostenmodell zu einem fließenden Betriebskostenmodell.

::: zone target="docs"

Entsprechende Informationen finden Sie in den folgenden Ressourcen:

- [Schätzen der Cloudkosten](../migration-considerations/assess/estimate.md)

::: zone-end
