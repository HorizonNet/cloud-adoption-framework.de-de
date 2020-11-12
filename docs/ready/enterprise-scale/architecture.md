---
title: Cloud Adoption Framework – Architektur für Zielzonen auf Unternehmensebene
description: Hier erfahren Sie mehr über die Zielzonenarchitektur auf Unternehmensniveau im Cloud Adoption Framework für Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: csu
ms.openlocfilehash: 276556467a2741cfb12d2c79049c33b31e5a421f
ms.sourcegitcommit: 2c949c44008161e50b91ffd3f01f6bf32da2d4d2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/10/2020
ms.locfileid: "94432702"
---
# <a name="cloud-adoption-framework-enterprise-scale-landing-zone-architecture"></a>Cloud Adoption Framework – Architektur für Zielzonen auf Unternehmensebene

Der Entwurf auf Unternehmensebene ist ein Architekturansatz und eine Referenzimplementierung, die die effektive Erstellung und Operationalisierung von Zielzonen in Azure im großen Stil ermöglicht. Er ist auf die Azure-Roadmap und das Cloud Adoption Framework für Azure abgestimmt.

## <a name="architecture-overview"></a>Übersicht über die Architektur

Die Architektur für Cloud Adoption Framework-Zielzonen auf Unternehmensniveau stellt den strategischen Entwurfspfad und den technischen Zielstatus für die Azure-Umgebung einer Organisation dar. Sie wird weiterhin parallel zur Azure-Plattform weiterentwickelt und durch die verschiedenen Entwurfsentscheidungen definiert, die Organisationen zum Ausarbeiten ihrer Azure-Journey treffen müssen.

Nicht alle Unternehmen verwenden Azure gleich, sodass die Architektur für Cloud Adoption Framework-Zielzonen auf Unternehmensniveau von Kunde zu Kunde unterschiedlich ist. Basierend auf den technischen Überlegungen und Entwurfsempfehlungen in diesem Leitfaden müssen Sie je nach Szenario Ihrer Organisation daher unterschiedliche Faktoren gegeneinander abwägen. Gewisse Abweichungen werden erwartet. Wenn Sie jedoch die wichtigsten Empfehlungen befolgen, ebnet die resultierende Zielarchitektur für Ihre Organisation den Weg für eine nachhaltigere Skalierung.

## <a name="landing-zone-in-enterprise-scale"></a>Zielzone auf Unternehmensebene

Azure-Zielzonen sind das Ergebnis einer Azure-Umgebung mit mehreren Abonnements, in der Skalierbarkeit, Sicherheit, Governance, Netzwerke und Identität berücksichtigt werden. Azure-Zielzonen ermöglichen die Anwendungsmigration und Greenfield-Entwicklung auf Unternehmensniveau in Azure. Diese Zonen berücksichtigen alle Plattformressourcen, die zur Unterstützung des Anwendungsportfolios des Kunden erforderlich sind, und unterscheiden nicht zwischen Infrastructure-as-a-Service oder Platform-as-a-Service.

Vor dem Bau neuer Häuser wird zum Beispiel zunächst die Verfügbarkeit von Wasser-, Gas- und Stromleitungen sichergestellt. Im vorliegenden Kontext werden die Netzwerk-, Identitäts- und Zugriffsverwaltung sowie die Richtlinien, Verwaltung und Überwachung als gemeinsame Versorgungsdienste betrachtet, die für eine optimierte Anwendungsmigration verfügbar sein müssen, bevor der Vorgang gestartet wird.

![Diagramm mit Struktur einer Zielzone](./media/lz-design.png)

_Abbildung 1: Zielzonenaufbau._

## <a name="high-level-architecture"></a>Grundlegende Architektur

Eine Architektur in der Größenordnung eines Unternehmens wird durch eine Reihe von Entwurfsüberlegungen und -empfehlungen aus acht [kritischen Entwurfsbereichen](./design-guidelines.md) definiert, wobei zwei Netzwerktopologien empfohlen werden: eine Architektur auf Unternehmensniveau, die auf einer Azure Virtual WAN-Netzwerktopologie basiert (in Abbildung 2 abgebildet), oder basierend auf einer herkömmlichen Azure-Netzwerktopologie, die auf der Hub-and-Spoke-Architektur basiert (zu sehen in Abbildung 3).   

[![Diagramm, das eine Architektur für Cloud Adoption Framework-Zielzonen auf Unternehmensniveau, basierend auf einer Azure Virtual WAN-Netzwerktopologie, zeigt.](./media/ns-arch-inline.png)](./media/ns-arch-expanded.png#lightbox)

_Abbildung 2: Eine Architektur für Cloud Adoption Framework-Zielzonen auf Unternehmensniveau, basierend auf einer Azure Virtual WAN-Netzwerktopologie. Beachten Sie, dass das Konnektivitätsabonnement einen VWAN-Hub verwendet._

[![Diagramm: Architektur für Cloud Adoption Framework-Zielzonen auf Unternehmensniveau](./media/ns-arch-cust-inline.png)](./media/ns-arch-cust-expanded.png#lightbox)

_Abbildung 3: Eine Architektur für Cloud Adoption Framework-Zielzonen auf Unternehmensniveau, basierend auf einer herkömmlichen Azure-Netzwerktopologie. Beachten Sie, dass das Konnektivitätsabonnement eine Hub-VNet verwendet._

Laden Sie die PDF-Dateien herunter, die die Diagramme der Architektur auf Unternehmensniveau enthalten, basierend auf der [Virtual WAN](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/ready/enterprise-scale-architecture.pdf)-Netzwerktopologie oder einer herkömmlichen Azure-Netzwerktopologie, basierend auf der [Hub-and-Spoke](https://github.com/microsoft/CloudAdoptionFramework/raw/master/ready/enterprise-scale-architecture-cust.pdf)-Architektur.

In den Abbildungen 2 und 3 finden Sie Verweise auf die kritischen Entwurfsbereiche auf Unternehmensniveau, die mit den Buchstaben A bis I gekennzeichnet sind:

![Der Buchstabe A](./media/a.png) [Enterprise Agreement-Registrierung (EA) und Azure Active Directory-Mandanten](./enterprise-enrollment-and-azure-ad-tenants.md). Eine Enterprise Agreement-Registrierung (EA) stellt die Geschäftsbeziehung zwischen Microsoft und der Art und Weise dar, wie Ihre Organisation Azure verwendet. Sie bildet die Grundlage für die Abrechnung für alle Ihre Abonnements und wirkt sich auf die Verwaltung Ihrer digitalen Ressourcen aus. Ihre EA-Registrierung wird über ein Azure-Unternehmensportal verwaltet. Eine Registrierung bildet häufig die Hierarchie einer Organisation ab, zu der die Abteilungen, Konten und Abonnements gehören. Ein Azure AD-Mandant bietet Identitäts- und Zugriffsverwaltung, die ein wichtiger Bestandteil Ihres Sicherheitsstatus ist. Ein Azure AD-Mandant stellt sicher, dass authentifizierte und autorisierte Benutzer nur auf die Ressourcen zugreifen können, für die sie über Zugriffsberechtigungen verfügen.

![Der Buchstabe B](./media/b.png) [Identitäts- und Zugriffsverwaltung](./identity-and-access-management.md). Sowohl für die Server- als auch für die Benutzerauthentifizierung muss eine Azure Active Directory-Implementierung entworfen und integriert werden. Um eine Trennung der Aufgabenbereiche und Berechtigungen für den Betrieb und die Verwaltung der Plattform zu erzwingen, muss die ressourcenbasierte Zugriffssteuerung (Role-Based Access Control, RBAC) modelliert und bereitgestellt werden. Für einen sicheren Zugriff auf Ressourcen und die Unterstützung von Vorgängen wie Rotation und Wiederherstellung muss eine Schlüsselverwaltungslösung entworfen und bereitgestellt werden. Abschließend werden Anwendungsbesitzern Zugriffsrollen auf Steuerungs- und Datenebene zugewiesen, um Ressourcen eigenständig erstellen und verwalten zu können.

![Der Buchstabe C](./media/c.png) [Verwaltungsgruppen- und Abonnementorganisation](./management-group-and-subscription-organization.md). Verwaltungsgruppenstrukturen innerhalb eines Azure AD-Mandanten (Azure Active Directory) unterstützen Organisationszuordnung und sind sorgfältig zu durchdenken, wenn eine Organisation die Azure-Einführung in großem Umfang plant. Abonnements sind eine Einheit für die Verwaltung, Abrechnung und Skalierung in Azure. Sie spielen eine wichtige Rolle bei der Entwicklung für Azure im großen Stil. Dieser kritische Entwurfsbereich unterstützt Sie beim Erfassen von Abonnementanforderungen und Entwerfen von Zielabonnements anhand wichtiger Faktoren. Zu diesen Faktoren gehören die Art von Umgebung, das Besitzer- und Governancemodell, die Organisationsstruktur sowie Anwendungsportfolios.

![Der Buchstabe C](./media/d.png) [Verwaltung und Überwachung](./management-and-monitoring.md). Eine ganzheitliche (horizontale) Ressourcenüberwachung und entsprechende Warnungen müssen auf Plattformebene entworfen, bereitgestellt und integriert werden. Operative Aufgaben wie das Patchen und Durchführen von Sicherungen müssen ebenfalls definiert und optimiert werden. Sicherheitsvorgänge sowie Funktionen für Überwachung und Protokollierung müssen entworfen und sowohl mit Azure-Ressourcen als auch mit vorhandenen lokalen Systemen integriert werden. Sämtliche Aktivitätsprotokolle für Abonnements, in denen ressourcenübergreifende Vorgänge auf der Steuerungsebene erfasst werden, sollten in Log Analytics gestreamt werden, damit sie in Übereinstimmung mit RBAC-Berechtigungen abgefragt und analysiert werden können.

![Der Buchstabe E](./media/e.png) [Netzwerktopologie und Konnektivität](./network-topology-and-connectivity.md). Die End-to-End-Netzwerktopologie muss Azure-Regionen und lokale Umgebungen umfassen, um eine lückenlose Konnektivität zwischen Plattformbereitstellungen sicherzustellen. Erforderliche Dienste und Ressourcen (z. B. Firewalls und virtuelle Netzwerkgeräte) müssen so bestimmt, bereitgestellt und konfiguriert werden, dass sämtliche Sicherheitsanforderungen erfüllt sind.

![Der Buchstabe F](./media/f.png), ![Der Buchstabe G](./media/g.png), ![Der Buchstabe H](./media/h.png) [Business Continuity & Disaster Recovery (Geschäftskontinuität und Notfallwiederherstellung)](./business-continuity-and-disaster-recovery.md) und [Sicherheit, Governance und Compliance](./security-governance-and-compliance.md). Auf der Azure-Zielplattform müssen ganzheitliche, zielzonenspezifische Richtlinien bestimmt, beschrieben, erstellt und bereitgestellt werden, mit denen unternehmens- und branchenspezifische sowie regulatorische Kontrollen implementiert werden. Mithilfe von Richtlinien sollte die Konformität von Anwendungen und zugrunde liegender Ressourcen ohne Abstraktion oder Verwaltungsfunktion sichergestellt werden.

![Der Buchstabe I](./media/i.png) [Plattformautomatisierung und DevOps](platform-automation-and-devops.md). Um eine sichere, wiederholbare und einheitliche Bereitstellung von Infrastructure-as-Code-Artefakten sicherzustellen, muss eine umfassende DevOps-Lösung mit zuverlässigen Verfahren für den Softwareentwicklungslebenszyklus entworfen, erstellt und bereitgestellt werden. Diese Artefakte müssen unter Verwendung von dedizierten Pipelines für Integration, Veröffentlichung und Bereitstellung, die eine umfassende, zuverlässige Quellcodeverwaltung und Nachverfolgbarkeit bieten, entwickelt, getestet und bereitgestellt werden.

## <a name="next-steps"></a>Nächste Schritte

Passen Sie die Implementierung dieser Architektur unter Berücksichtigung der Entwurfsleitfäden für das Cloud Adoption Framework auf Unternehmensniveau an.

> [!div class="nextstepaction"]
> [Entwurfsrichtlinien](./design-guidelines.md)
