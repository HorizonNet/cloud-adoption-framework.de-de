---
title: Konfigurieren von Azure-Verwaltungsdiensten für ein Abonnement
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Konfigurieren von Azure-Verwaltungsdiensten für ein Abonnement
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 56a989e975625c9d8f0f3db80dab9043dca3a479
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031292"
---
# <a name="configure-azure-management-services-at-scale"></a>Bedarfsabhängiges Konfigurieren von Azure-Verwaltungsdiensten

Das Onboarding der Azure-Verwaltungsdienste für Ihre Server umfasst zwei Aufgaben: die Bereitstellung von Dienst-Agents für Ihre Server und die Aktivierung der Verwaltungslösungen. In diesem Artikel werden die folgenden Prozesse beschrieben, die es Ihnen ermöglichen, diese Aufgaben durchzuführen:

- [Bereitstellen von erforderlichen Agents auf Azure-VMs mit Azure Policy](#deploy-extensions-to-azure-vms-using-azure-policy)
- [Bereitstellen von erforderlichen Agents auf lokalen Servern](#install-required-agents-on-on-premises-servers)
- [Aktivieren und Konfigurieren von Lösungen](#enable-and-configure-solutions)

> [!NOTE]
> Erstellen Sie den erforderlichen [Log Analytics-Arbeitsbereich und das Azure Automation-Konto](./prerequisites.md#create-a-workspace-and-automation-account), bevor Sie das Onboarding von virtuellen Computern für Azure-Verwaltungsdienste durchführen.

## <a name="deploy-extensions-to-azure-vms-using-azure-policy"></a>Bereitstellen von Erweiterungen für Azure-VMs mit Azure Policy

Für alle Verwaltungslösungen, die unter [Azure-Verwaltungstools und -dienste](./tools-services.md) beschrieben sind, muss der Log Analytics-Agent auf virtuellen Azure-Computern (VMs) und lokalen Servern installiert sein. Sie können das Onboarding für Ihre Azure-VMs mit Azure Policy bedarfsabhängig durchführen. Weisen Sie eine Richtlinie zu, um sicherzustellen, dass der Agent auf Ihren gesamten Azure-VMs installiert ist und eine Verbindung mit dem richtigen Log Analytics-Arbeitsbereich besteht.

Azure Policy verfügt über eine integrierte [Richtlinieninitiative](https://docs.microsoft.com/azure/governance/policy/index.md#initiative-definition), die sowohl den Log Analytics-Agent als auch den [Microsoft Dependency-Agent](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-onboard#the-microsoft-dependency-agent) umfasst, der für Azure Monitor für VMs benötigt wird.

<!-- TODO: Add these when available.
- [Preview]: Enable Azure Monitor for virtual machine scale sets.
- [Preview]: Enable Azure Monitor for VMs.
 -->

> [!NOTE]
> Weitere Informationen zu den unterschiedlichen Agents für die Azure-Überwachung finden Sie unter [Übersicht über die Azure-Überwachungs-Agents](https://docs.microsoft.com/azure/azure-monitor/platform/agents-overview).

### <a name="assign-policies"></a>Zuweisen von Richtlinien

Weisen Sie die im obigen Abschnitt aufgeführten Richtlinien wie folgt zu:

1. Navigieren Sie im Azure-Portal zu **Azure Policy** > **Zuweisungen** > **Initiative zuweisen**.

    ![Screenshot: Benutzeroberfläche für Richtlinien im Portal](./media/onboarding-at-scale1.png)

2. Wählen Sie auf der Seite **Richtlinie zuweisen** den **Bereich** aus, indem Sie auf die Auslassungspunkte (…) klicken und dann entweder eine Verwaltungsgruppe oder ein Abonnement auswählen. Wählen Sie optional eine Ressourcengruppe aus. Mit einem Bereich wird bestimmt, welchen Ressourcen bzw. welcher Ressourcengruppe die Richtlinie zugewiesen wird. Wählen Sie anschließend unten auf der Seite **Bereich** die Option **Auswählen**.

3. Wählen Sie die Auslassungspunkte (…) neben der Option **Richtliniendefinition** aus, um die Liste mit den verfügbaren Definitionen zu öffnen. Sie können die Initiativendefinition filtern, indem Sie im Feld **Suche** den Suchbegriff **Azure Monitor** eingeben:

    ![Screenshot: Benutzeroberfläche für Richtlinien im Portal](./media/onboarding-at-scale2.png)

4. Der **Zuweisungsname** wird automatisch mit dem ausgewählten Richtliniennamen gefüllt, kann aber geändert werden. Sie können auch eine optionale Beschreibung hinzufügen, um weitere Informationen zu dieser Richtlinienzuweisung anzugeben. Das Feld **Zugewiesen von** wird abhängig vom angemeldeten Benutzer automatisch ausgefüllt. Dieses Feld ist optional. Sie können benutzerdefinierte Werte eingeben.

5. Wählen Sie für diese Richtlinie die Option **Log Analytics-Arbeitsbereich** für die Zuordnung des Log Analytics-Agents.

    ![Screenshot: Benutzeroberfläche für Richtlinien im Portal](./media/onboarding-at-scale3.png)

6. Überprüfen Sie den **Speicherort der verwalteten Identität**. Wenn diese Richtlinie den Typ [DeployIfNotExists](https://docs.microsoft.com/azure/governance/policy/concepts/effects#deployifnotexists) aufweist, ist für die Bereitstellung der Richtlinie eine verwaltete Identität erforderlich. Im Portal wird das Konto gemäß der Auswahl des Kontrollkästchens erstellt.

7. Wählen Sie **Zuweisen** aus.

Nach Abschluss des Assistenten wird die Richtlinienzuweisung in der Umgebung bereitgestellt. Es kann bis zu 30 Minuten dauern, bis die Richtlinie wirksam wird. Sie können sie testen, indem Sie nach 30 Minuten neue VMs erstellen und dann überprüfen, ob der Microsoft Monitoring Agent (MMA) auf dem virtuellen Computer standardmäßig aktiviert ist.

## <a name="install-required-agents-on-on-premises-servers"></a>Installieren der erforderlichen Agents auf lokalen Servern

> [!NOTE]
> Erstellen Sie den erforderlichen [Log Analytics-Arbeitsbereich und das Azure Automation-Konto](./prerequisites.md#create-a-workspace-and-automation-account), bevor Sie das Onboarding von Servern für Azure-Verwaltungsdienste durchführen.

Für lokale Server müssen Sie den [Log Analytics-Agent und den Microsoft Dependency-Agent](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-enable-hybrid-cloud) manuell herunterladen und installieren und diese Agents anschließend so konfigurieren, dass eine Verbindung mit dem richtigen Arbeitsbereich hergestellt wird. Geben Sie dazu die Arbeitsbereichs-ID und die Informationen zum Schlüssel an. Sie können diese Angaben ermitteln, indem Sie im Azure-Portal zu Ihrem Log Analytics-Arbeitsbereich navigieren und **Einstellungen** > **Erweiterte Einstellungen** auswählen.

![Screenshot: Erweiterte Einstellungen für Log Analytics-Arbeitsbereich im Azure-Portal](./media/onboarding-on-premises.png)

## <a name="enable-and-configure-solutions"></a>Aktivieren und Konfigurieren von Lösungen

Zur Aktivierung von Lösungen müssen Sie den Log Analytics-Arbeitsbereich konfigurieren. Für Azure-VMs und lokale Server, für die das Onboarding durchgeführt wurde, werden die Lösungen aus den Log Analytics-Arbeitsbereichen abgerufen, mit denen sie verbunden sind.

Die folgenden Lösungen werden in diesem Abschnitt behandelt:

- [Updateverwaltung](#update-management)
- [Änderungsnachverfolgung und Bestand](#change-tracking-and-inventory-solutions)
- [Azure-Aktivitätsprotokoll](#azure-activity-log)
- [Azure Log Analytics-Agent-Integritätsdiagnose](#azure-log-analytics-agent-health)
- [Antischadsoftwarebewertung](#antimalware-assessment)
- [Azure Monitor für VMs](#azure-monitor-for-vms)
- [Azure Security Center](#azure-security-center)

### <a name="update-management"></a>Updateverwaltung

Für die Lösungen für Updateverwaltung, Änderungsnachverfolgung und Bestand sind sowohl ein Log Analytics-Arbeitsbereich als auch ein Automation-Konto erforderlich. Um sicherzustellen, dass diese Ressourcen richtig konfiguriert sind, empfehlen wir Ihnen, das Onboarding über das Automation-Konto durchzuführen. Weitere Informationen finden Sie unter [Integrieren von Lösungen für die Updateverwaltung, Änderungsnachverfolgung und den Bestand](https://docs.microsoft.com/azure/automation/automation-onboard-solutions-from-automation-account).

Wir empfehlen Ihnen, die Lösung für die Updateverwaltung für alle Server zu aktivieren. Die Updateverwaltung ist für Azure-VMs und lokale Server kostenlos. Wenn Sie die Updateverwaltung über Ihr Automation-Konto aktivieren, wird im Arbeitsbereich eine [Bereichskonfiguration](https://docs.microsoft.com/azure/automation/automation-onboard-solutions-from-automation-account#scope-configuration) erstellt. Sie müssen den Bereich manuell aktualisieren, um Computer einzubinden, die dem Updatedienst unterliegen.

Um alle vorhandenen Server und zukünftigen Server abzudecken, müssen Sie die Bereichskonfiguration entfernen. Zeigen Sie hierzu im Azure-Portal Ihr Automation-Konto an, und wählen Sie **Updateverwaltung** > **Computer verwalten** > **Auf allen verfügbaren und zukünftigen Computern aktivieren**. Durch die Aktivierung dieser Einstellung kann die Updateverwaltung für alle Azure-VMs verwendet werden, für die eine Verbindung mit dem Arbeitsbereich besteht.

![Screenshot: Updateverwaltung im Azure-Portal](./media/onboarding-configuration1.png)

### <a name="change-tracking-and-inventory-solutions"></a>Lösungen für Änderungsnachverfolgung und Bestand

Für das Onboarding der Lösungen für die Änderungsnachverfolgung und den Bestand befolgen Sie dieselben Schritte wie für die Updateverwaltung. Weitere Informationen zum Onboarding dieser Lösungen über Ihr Automation-Konto finden Sie unter [Integrieren von Lösungen für die Updateverwaltung, Änderungsnachverfolgung und den Bestand](https://docs.microsoft.com/azure/automation/automation-onboard-solutions-from-automation-account).

Die Lösung für die Änderungsnachverfolgung ist für Azure-VMs kostenlos und kostet für lokale Server monatlich 6 USD pro Knoten. Mit diesen Kosten sind die Bereiche Änderungsnachverfolgung, Bestand und Desired State Configuration abgedeckt. Falls Sie nur bestimmte lokale Server registrieren möchten, können Sie diese Server einbinden. Wir empfehlen Ihnen, das Onboarding für Ihre gesamten Produktionsserver durchzuführen.

#### <a name="opt-in-via-the-azure-portal"></a>Einbinden über das Azure-Portal

1. Wechseln Sie zu dem Automation-Konto, für das die Lösungen für die Änderungsnachverfolgung und den Bestand aktiviert sind.
2. Wählen Sie **Änderungsnachverfolgung**.
3. Wählen Sie im Bereich oben rechts die Option **Computer verwalten**.
4. Wählen Sie **Auf ausgewählten Computern aktivieren** und dann den gewünschten Computer aus, indem Sie neben dem Computernamen auf **Hinzufügen** klicken.
5. Wählen Sie **Aktivieren** aus, um die Lösung für diese Computer zu aktivieren.

![Screenshot: Änderungsnachverfolgung im Azure-Portal](./media/onboarding-configuration2.png)

#### <a name="opt-in-by-using-saved-searches"></a>Einbinden mit gespeicherten Suchen

Alternativ können Sie die Bereichskonfiguration so durchführen, dass lokale Server eingebunden werden. Für die Bereichskonfiguration werden gespeicherte Suchvorgänge verwendet.

Führen Sie die folgenden Schritte aus, um die gespeicherte Suche zu erstellen oder zu ändern:

1. Wechseln Sie zum Log Analytics-Arbeitsbereich, der mit dem Automation-Konto verknüpft ist, das Sie in den vorherigen Schritten konfiguriert haben.

2. Wählen Sie unter **Allgemein** die Option **Gespeicherte Suchvorgänge** aus.

3. Geben Sie im Feld **Filter** das Wort **Änderungsnachverfolgung** ein, um die Liste mit den gespeicherten Suchen zu filtern. Wählen Sie in den Ergebnissen **MicrosoftDefaultComputerGroup** aus.

4. Geben Sie den Namen des Computers oder die VMUUID ein, um die Computer einzubinden, für die die Änderungsnachverfolgung genutzt werden soll.

    ```kusto
    Heartbeat
    | where AzureEnvironment=~"Azure" or Computer in~ ("list of the on-premises server names", "server1")
    | distinct Computer
    ```

    > [!NOTE]
    > Der Servername muss genau mit dem Wert übereinstimmen, der im Ausdruck angegeben ist, und sollte kein Domänennamensuffix enthalten.

5. Wählen Sie **Speichern** aus.

6. Standardmäßig ist die Bereichskonfiguration mit der gespeicherten Suche **MicrosoftDefaultComputerGroup** verknüpft und wird automatisch aktualisiert.

### <a name="azure-activity-log"></a>Azure-Aktivitätsprotokoll

Das [Azure-Aktivitätsprotokoll](https://docs.microsoft.com/azure/azure-monitor/platform/activity-logs-overview) ist ebenfalls Teil von Azure Monitor. Hiermit können Sie Erkenntnisse zu Ereignissen auf Abonnementebene gewinnen, die in Azure eintreten.

So fügen Sie diese Lösung hinzu

1. Öffnen Sie im Azure-Portal die Option **Alle Dienste**, und wählen Sie **Verwaltung + Governance** > **Lösungen**.
2. Wählen Sie in der Ansicht **Lösungen** die Option **Hinzufügen** aus.
3. Suchen Sie nach **Aktivitätsprotokollanalyse**, und wählen Sie diese Option aus.
4. Klicken Sie auf **Erstellen**.

Sie müssen den **Arbeitsbereichsnamen** des Arbeitsbereichs eingeben, den Sie im vorherigen Abschnitt beim Aktivieren der Lösung erstellt haben.

### <a name="azure-log-analytics-agent-health"></a>Azure Log Analytics-Agent-Integritätsdiagnose

Die Lösung „Azure Log Analytics-Agent-Integritätsdiagnose“ liefert Ihnen Erkenntnisse zur Integrität, Leistung und Verfügbarkeit Ihrer Windows- und Linux-Server.

So fügen Sie diese Lösung hinzu

1. Öffnen Sie im Azure-Portal die Option **Alle Dienste**, und wählen Sie **Verwaltung + Governance** > **Lösungen**.
2. Wählen Sie in der Ansicht **Lösungen** die Option **Hinzufügen** aus.
3. Suchen Sie nach **Azure Log Analytics-Agent-Integritätsdiagnose** , und wählen Sie diese Option aus.
4. Klicken Sie auf **Erstellen**.

Sie müssen den **Arbeitsbereichsnamen** des Arbeitsbereichs eingeben, den Sie im vorherigen Abschnitt beim Aktivieren der Lösung erstellt haben.

Nachdem die Erstellung abgeschlossen ist, zeigt die Instanz der Arbeitsbereichsressource **AgentHealthAssessment** an, wenn Sie **Ansicht** > **Lösungen** auswählen.

### <a name="antimalware-assessment"></a>Antischadsoftwarebewertung

Mit der Lösung für die Antischadsoftwarebewertung können Sie Server identifizieren, die mit Schadsoftware infiziert sind oder für die ein erhöhtes Risiko einer Infektion besteht.

So fügen Sie diese Lösung hinzu

1. Öffnen Sie im Azure-Portal die Option **Alle Dienste**, und wählen Sie **Verwaltung + Governance** > **Lösungen**.
2. Wählen Sie in der Ansicht **Lösungen** die Option **Hinzufügen** aus.
3. Suchen Sie nach **Antischadsoftwarebewertung**, und wählen Sie diese Option aus.
4. Klicken Sie auf **Erstellen**.

Sie müssen den **Arbeitsbereichsnamen** des Arbeitsbereichs eingeben, den Sie im vorherigen Abschnitt beim Aktivieren der Lösung erstellt haben.

Nachdem die Erstellung abgeschlossen ist, zeigt die Instanz der Arbeitsbereichsressource **AntiMalware** an, wenn Sie **Ansicht** > **Lösungen** auswählen.

### <a name="azure-monitor-for-vms"></a>Azure Monitor für VMs

Sie können [Azure Monitor für VMs](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-overview) auf der Ansichtsseite für die VM-Instanz so aktivieren, wie dies im vorherigen Artikel [Aktivieren von Verwaltungsdiensten auf einem einzelnen virtuellen Computer zur Auswertung](./onboard-single-vm.md) beschrieben ist. Sie sollten Lösungen nicht direkt auf der Seite **Lösungen** aktivieren, wie Sie dies für die anderen Lösungen in diesem Artikel getan haben. Bei Bereitstellungen größeren Umfangs ist es unter Umständen einfacher, die [Automatisierung](./onboarding-automation.md) zu verwenden, um im Arbeitsbereich die richtigen Lösungen zu aktivieren.

### <a name="azure-security-center"></a>Azure Security Center

In dieser Anleitung empfehlen wir Ihnen, für alle Server standardmäßig das Onboarding für den *Free-Tarif* von Azure Security Center durchzuführen. Bei dieser Option erhalten Sie eine Basisebene mit Sicherheitsbewertungen und verwertbaren Sicherheitsempfehlungen für Ihre Umgebung. Die Aktualisierung auf den *Standard-Tarif* von Security Center ist mit weiteren Vorteilen verbunden, die auf der [Seite mit den Preisen für Security Center](https://docs.microsoft.com/azure/security-center/security-center-pricing) ausführlich beschrieben sind.

Gehen Sie wie folgt vor, um den Free-Tarif für Azure Security Center zu aktivieren:

1. Wechseln Sie im Portal zur Seite **Security Center**.
2. Wählen Sie unter **RICHTLINIE UND KONFORMITÄT** die Option **Sicherheitsrichtlinie**.
3. Suchen Sie im rechten Bereich nach der von Ihnen erstellten Log Analytics-Arbeitsbereichsressource.
4. Wählen Sie für diesen Arbeitsbereich die Option **Einstellungen bearbeiten >** aus.
5. Wählen Sie **Tarif**aus.
6. Wählen Sie die Option **Free**.
7. Wählen Sie **Speichern** aus.

## <a name="next-steps"></a>Nächste Schritte

Informieren Sie sich darüber, wie Sie die Automatisierung zum Durchführen des Onboardings von Servern und zum Erstellen von Warnungen verwenden.

> [!div class="nextstepaction"]
> [Automatisieren des Onboardings und der Warnungskonfiguration](./onboarding-automation.md)
