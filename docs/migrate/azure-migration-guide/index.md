---
title: Einführung in den Leitfaden zur Azure-Migration
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Anhand einer Schritt-für-Schritt-Anleitung wird beschrieben, wie Sie die Dienste Ihres Unternehmens effizient zu Azure migrieren.
author: matticusau
ms.author: mlavery
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 9f27c7fca9a9a5bd2f5c38f78b8db2092b24d014
ms.sourcegitcommit: 3655aa7f3e80249e0b2b562cd40dd750afc82043
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2019
ms.locfileid: "74251485"
---
::: zone target="docs"

# <a name="azure-migration-guide-before-you-start"></a>Leitfaden zur Azure-Migration: Vorbereitung

::: zone-end

::: zone target="chromeless"

# <a name="before-you-start"></a>Vorbereitung

::: zone-end

Bevor Sie Ressourcen zu Azure migrieren, müssen Sie die Migrationsmethode und die Features auswählen, die Sie zur Steuerung und Sicherung Ihrer Umgebung verwenden. Dieser Leitfaden führt Sie durch diesen Entscheidungsprozess.

::: zone target="docs"

> [!TIP]
> Dieser Leitfaden steht im Azure-Portal als interaktive Umgebung zur Verfügung. Navigieren Sie im Azure-Portal zum [Azure Quickstart Center](https://portal.azure.com/?feature.quickstart=true#blade/Microsoft_Azure_Resources/QuickstartCenterBlade), wählen Sie **Migrieren Ihrer Umgebung zu Azure** aus, und befolgen Sie dann die Schritt-für-Schritt-Anleitung.

::: zone-end

# <a name="overviewtaboverview"></a>[Übersicht](#tab/Overview)

Dieser Leitfaden führt Sie durch die Grundlagen der Migration von Anwendungen und Ressourcen aus Ihrer lokalen Umgebung zu Azure. Es ist für Migrationsszenarien mit minimaler Komplexität konzipiert. Ermitteln Sie die Eignung dieses Leitfadens für Ihre Migration über die Registerkarte **Verwendung dieses Leitfadens**.

Bei der Migration zu Azure können Sie Ihre Anwendungen ohne Änderungen mit IaaS-basierten VM-Lösungen migrieren (als Migration vom Typ _Zuweisen eines neuen Hosts_ oder _Lift & Shift_ bezeichnet), oder Sie verfügen über die Flexibilität, verwaltete Dienste und andere cloudnative Features zur Modernisierung Ihrer Anwendungen zu nutzen. Weitere Informationen zu diesen Optionen finden Sie auf der Registerkarte mit den **Migrationsoptionen**. Bei der Entwicklung Ihrer Migrationsstrategie sollten Sie Folgendes berücksichtigen:

- Funktionieren meine migrierenden Anwendungen in der Cloud?
- Welche ist die beste Strategie (in Bezug auf Technologie, Tools und Migrationen) für meine Anwendung? Weitere Informationen finden Sie im [Entscheidungsleitfaden zur Wahl der Migrationstools](../../decision-guides/migrate-decision-guide/index.md) für das Microsoft Cloud Adoption Framework.
- Wie minimiere ich Ausfallzeiten während der Migration?
- Wie können Kosten gesteuert werden?
- Wie kann ich Ressourcenkosten nachverfolgen und ordnungsgemäß abrechnen?
- Wie stelle ich sicher, dass wir Konformität und Vorschriften einhalten?
- Wie erfülle ich die rechtlichen Vorgaben hinsichtlich der Datenhoheit in bestimmten Ländern?

Dieser Leitfaden hilft bei der Beantwortung dieser Fragen. Er schlägt die Aufgaben und Features vor, die Sie bei der Vorbereitung auf die Bereitstellung von Ressourcen in Azure berücksichtigen sollten, einschließlich:

> [!div class="checklist"]
>
> - **Konfigurieren der Voraussetzungen** Führen Sie die Planung und Vorbereitung auf die Migration durch.
> - **Bewerten Ihrer technischen Eignung** Überprüfen Sie die technische Bereitschaft und Eignung für die Migration.
> - **Verwalten von Kosten und Abrechnung:** Betrachten Sie die Kosten Ihrer Ressourcen.
> - **Migrieren Ihrer Dienste** Führen Sie die eigentliche Migration aus.
> - **Organisieren Ihrer Ressourcen** Sperren Sie wichtige Ressourcen für Ihr System und markieren Sie Ressourcen, um sie nachzuverfolgen.
> - **Optimieren und Transformieren** Nutzen Sie die Gelegenheit nach der Migration, um Ihre Ressourcen zu überprüfen.
> - **Sichern und Verwalten** Stellen Sie sicher, dass Ihre Umgebung sicher ist und ordnungsgemäß überwacht wird.
> - **Unterstützung** Erhalten Sie für die Aktivitäten während oder nach der Migration Hilfe oder Unterstützung.

::: zone target="docs"

Weitere Informationen zum Organisieren und Strukturieren Ihrer Abonnements, zur Verwaltung Ihrer bereitgestellten Ressourcen und zur Einhaltung Ihrer Unternehmensrichtlinien finden Sie unter [Governance in Azure](https://docs.microsoft.com/azure/security/governance-in-azure).

::: zone-end

# <a name="when-to-use-this-guidetabwhentousethisguide"></a>[Verwendung dieses Leitfadens](#tab/WhenToUseThisGuide)

Während die in diesem Leitfaden behandelten Tools eine Vielzahl von Migrationsszenarien unterstützen, konzentriert sich dieser Leitfaden auf Maßnahmen mit begrenztem Umfang und _minimaler Komplexität_. Zur Ermittlung, ob dieser Migrationsleitfaden für Ihr Projekt geeignet ist, prüfen Sie, ob die folgenden Bedingungen für Sie gelten:

- Sie migrieren eine homogene Umgebung.
- Es müssen nur wenige Geschäftseinheiten ausgerichtet werden, um die Migration abzuschließen.
- Sie planen keine Automatisierung der gesamten Migration.
- Sie migrieren eine geringe Anzahl von Servern.
- Die Abhängigkeitszuordnung der zu migrierenden Komponenten ist einfach zu definieren.
- Ihre Branche verfügt über minimale gesetzliche Anforderungen, die für diese Migration relevant sind.

Wenn eine dieser Bedingungen _nicht_ auf Ihre Situation zutrifft, sollten Sie stattdessen den [Leitfaden zum erweiterten Umfang](../expanded-scope/index.md) berücksichtigen. Außerdem empfehlen wir Ihnen, Unterstützung von einem unserer Microsoft-Teams oder -Partner anzufordern, um Migrationen durchzuführen, die den Leitfaden zum erweiterten Umfang erfordern. Kunden, die mit Microsoft oder zertifizierten Partnern zusammenarbeiten, sind in diesen Szenarien erfolgreicher. Weitere Informationen zur Anforderung von Unterstützung finden Sie in diesem Leitfaden.

<!-- markdownlint-enable MD033 -->

::: zone target="docs"

Weitere Informationen finden Sie unter

- [Leitfaden zum erweiterten Umfang](../expanded-scope/index.md)

::: zone-end

# <a name="migration-optionstabmigrationoptions"></a>[Migrationsoptionen](#tab/MigrationOptions)

Sie können eine Cloudmigration auf verschiedene Arten durchführen. Einige sind für verschiedene Szenarien besser geeignet als andere. Berücksichtigen Sie bei der Bestimmung der Migration für Ihre Umgebung die folgenden Optionen, wenn Sie sich für eine Migrationsstrategie entscheiden:

- **Zuweisen eines neuen Hosts:** Auch „Lift & Shift“ genannt. Beim Zuweisen eines neuen Hosts (Rehosten) wird der aktuellen Zustand zu Azure migriert. Die Architektur bleibt dabei größtenteils unverändert.
- **Refactoring:** PaaS-Optionen (Platform-as-a-Service) können zur Senkung der Betriebskosten zahlreicher Anwendungen beitragen. Unter Umständen empfiehlt es sich, eine Anwendung geringfügig umzugestalten, um sie an ein PaaS-Modell anzupassen. Dies bezieht sich auch auf den Anwendungsentwicklungsprozess der Codeumgestaltung, damit eine Anwendung neue Geschäftsmöglichkeiten erschließen kann.
- **Überarbeiten:** Einige ältere Anwendungen sind aufgrund von architekturbezogenen Entscheidungen, die bei der Entwicklung der Anwendung getroffen wurden, nicht mit Cloudanbietern kompatibel. In diesem Fall muss die Anwendung im Rahmen der Migration ggf. überarbeitet werden.
- **Neu erstellen:** In einigen Szenarien können die für die Migration einer Anwendung erforderlichen Änderungen zu groß sein, um weitere Investitionen zu rechtfertigen, und die Lösung muss neu erstellt werden.
- **Ersetzen:** Lösungen werden in der Regel mit der besten Technologie und den besten Verfahren implementiert, die zum Zeitpunkt der Implementierung zur Verfügung stehen. Manchmal können moderne SaaS-Anwendungen (Software-as-a-Service) sämtliche von der gehosteten Anwendung bereitgestellten Funktionen erfüllen. In diesem Fall kann eine Workload zukünftig ersetzt werden, wodurch sie bei Überlegungen im Rahmen der Migration nicht weiter berücksichtigt werden muss.

::: zone target="chromeless"

Diese Methoden schließen sich nicht gegenseitig aus. Während Ihre anfängliche Migration z. B. ein **Zuweisen eines neuen Hosts**-Modell verwenden könnte, wählen Sie möglicherweise ein **Refactoring**- oder **Überarbeiten**-Modell für die Implementierung im Rahmen der Optimierungsphase nach der Migration aus. Dies wird im Abschnitt **Optimieren und Transformieren** dieses Leitfadens nochmals aufgegriffen.

::: zone-end

::: zone target="docs"

Diese Methoden schließen sich nicht gegenseitig aus. Während Ihre anfängliche Migration z. B. ein **Zuweisen eines neuen Hosts**-Modell verwenden könnte, wählen Sie möglicherweise ein **Refactoring**- oder **Überarbeiten**-Modell für die Implementierung im Rahmen der Optimierungsphase nach der Migration aus. Dies wird im Abschnitt [Optimieren und Transformieren](./optimize-and-transform.md) dieses Leitfadens nochmals aufgegriffen.

::: zone-end

![Infografik zu den Migrationsoptionen](../../_images/migrate/migration-options.png)
