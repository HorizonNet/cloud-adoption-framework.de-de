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
ms.openlocfilehash: 697d1e8c57e2e4b7354b8730bbcf5e7653657000
ms.sourcegitcommit: 949b87bad28d32df84df190160089f01826f3a31
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/13/2020
ms.locfileid: "88193196"
---
<!-- cSpell:ignore CAF -->

# <a name="cloud-adoption-framework-enterprise-scale-landing-zone-architecture"></a>Cloud Adoption Framework – Architektur für Zielzonen auf Unternehmensebene

Der Entwurf auf Unternehmensebene ist ein Architekturansatz und eine Referenzimplementierung, die die effektive Erstellung und Operationalisierung von Zielzonen in Azure im großen Stil ermöglicht. Er ist auf die Azure-Roadmap und das Cloud Adoption Framework für Azure abgestimmt.

## <a name="architecture-overview"></a>Übersicht über die Architektur

Die Architektur für Cloud Adoption Framework-Zielzonen auf Unternehmensniveau stellt den strategischen Entwurfspfad und den technischen Zielstatus für die Azure-Umgebung einer Organisation dar. Sie wird weiterhin parallel zur Azure-Plattform weiterentwickelt und durch die verschiedenen Entwurfsentscheidungen definiert, die Organisationen zum Ausarbeiten ihrer Azure-Journey treffen müssen.

Nicht alle Unternehmen verwenden Azure gleich, sodass die Architektur für Cloud Adoption Framework-Zielzonen auf Unternehmensniveau von Kunde zu Kunde unterschiedlich ist. Basierend auf den technischen Überlegungen und Entwurfsempfehlungen in diesem Leitfaden müssen Sie je nach Szenario Ihrer Organisation daher unterschiedliche Faktoren gegeneinander abwägen. Gewisse Abweichungen werden erwartet. Wenn Sie jedoch die wichtigsten Empfehlungen befolgen, ebnet die resultierende Zielarchitektur für Ihre Organisation den Weg für eine nachhaltigere Skalierung.

## <a name="landing-zone-expanded-definition"></a>Zielzone: Erweiterte Definition

Unter [Überlegungen zu Zielzonen](../../ready/considerations/index.md) finden Sie eine detaillierte Definition des Begriffs _Zielzone_. Für Unternehmen, die eine Cloud Adoption Framework-Zielzone auf Unternehmensniveau implementieren möchten, ist jedoch eine noch genauere Definition erforderlich.

- **Bereich:** Bei Cloud Adoption Framework-Zielzonen auf Unternehmensniveau wird der Umfang von Zielzonen erheblich erweitert, um die Migration von Anwendungen und Greenfieldentwicklung auf Unternehmensniveau in Azure zu unterstützen. Durch diese Erweiterung lassen sich Entwürfe über das gesamte IT-Portfolio des Kunden hinweg skalieren und gehen damit weit über einen kurzfristigen Cloudeinführungsplan hinaus.

- **Refactoring:** Zur Unterstützung eines umfassenden IT-Portfolios auf Unternehmensebene können eine große Anzahl von Abonnements erforderlich sein. Im Cloud Adoption Framework wird zunächst ein häufiges Refactoring befürwortet. Vor der Bereitstellung der zehnten Produktionsworkload in der Cloud sollte jedoch eine Stabilisierung erfolgt sein. Wenn Sie mit einem Unternehmensportfolio arbeiten, lassen sich im Handumdrehen zehn Anwendungen bereitstellen. Ein Refactoring wird dadurch jedoch unpraktisch. Stattdessen sollte ein zentrales IT-Team oder Cloudkompetenzzentrum bei der ersten Veröffentlichung eine vollständigere Zielzone bereitstellen.

- **Ziel:** Um eine zu große Anzahl von Abonnements zu vermeiden, sollten Sie einheitliche Zielzonen verwenden, die auf einer Abonnementstrategie für Anwendungsarchetypen basieren. Erweitern Sie die Definition von erforderlichen Komponenten, um die Governance- und Complianceanforderungen eines cloudfähigen Unternehmens besser zu erfüllen. Eine Übersicht finden Sie in Abbildung 1.

- **Primärer Zweck:** Mit eingeschränkten Refaktoringmöglichkeiten und einer sorgfältig definierten Abonnementstrategie lassen sich die Zielzonen des Kunden schneller weiterentwickeln und ausbauen. Mit den Cloud Adoption Framework-Zielzonen auf Unternehmensniveau wird der primäre Zweck der Zielzone erweitert und der Fokus auf Aspekte wie Governance, Compliance, Sicherheit und Betriebsmanagement gelegt. Jeder dieser Bereiche wird bei der ersten Veröffentlichung der Zielzone und der unterstützenden gemeinsamen Dienste berücksichtigt.

Vor dem Bau neuer Häuser wird zum Beispiel zunächst die Verfügbarkeit von Wasser-, Gas- und Stromleitungen sichergestellt. Im vorliegenden Kontext werden die Netzwerk-, Identitäts- und Zugriffsverwaltung sowie die Richtlinien, Verwaltung und Überwachung als gemeinsame Versorgungsdienste betrachtet, die für eine optimierte Anwendungsmigration verfügbar sein müssen, bevor der Vorgang gestartet wird.

![Diagramm mit Struktur einer Zielzone](./media/lz-design.png)

_Abbildung 1: Zielzonenaufbau._

## <a name="expanded-list-of-requisite-components"></a>Erweiterte Liste der erforderlichen Komponenten

In der folgenden Liste wird diese Abbildung einer Zielzone erweitert. Dort werden die wichtigsten technischen Konstrukte beschrieben, die im Kontext der Kundenanforderungen entworfen und entwickelt werden müssen, um konforme technische Zielzonenumgebungen zu erstellen und eine erfolgreiche Azure-Einführung zu ermöglichen.

- **Identitäts- und Zugriffsverwaltung**: Sowohl für die Server- als auch für die Benutzerauthentifizierung muss eine Azure Active Directory-Implementierung entworfen und integriert werden. Um eine Trennung der Aufgabenbereiche und Berechtigungen für den Betrieb und die Verwaltung der Plattform zu erzwingen, muss die ressourcenbasierte Zugriffssteuerung (Role-Based Access Control, RBAC) modelliert und bereitgestellt werden. Für einen sicheren Zugriff auf Ressourcen und die Unterstützung von Vorgängen wie Rotation und Wiederherstellung muss eine Schlüsselverwaltungslösung entworfen und bereitgestellt werden. Abschließend werden Anwendungsbesitzern Zugriffsrollen auf Steuerungs- und Datenebene zugewiesen, um Ressourcen eigenständig erstellen und verwalten zu können.

- **Richtlinienverwaltung**: Auf der Azure-Zielplattform müssen ganzheitliche, zielzonenspezifische Richtlinien bestimmt, beschrieben, erstellt und bereitgestellt werden, mit denen unternehmens- und branchenspezifische sowie regulatorische Kontrollen implementiert werden. Mithilfe von Richtlinien sollte die Konformität von Anwendungen und zugrunde liegender Ressourcen ohne Abstraktion oder Verwaltungsfunktion sichergestellt werden.

- **Verwaltung und Überwachung**: Es müssen ganzheitliche (horizontale) Funktionen für Ressourcenüberwachung und Warnungen auf Plattformebene entworfen, bereitgestellt und integriert werden. Operative Aufgaben wie das Patchen und Durchführen von Sicherungen müssen ebenfalls definiert und optimiert werden. Sicherheitsvorgänge sowie Funktionen für Überwachung und Protokollierung müssen entworfen und sowohl mit Azure-Ressourcen als auch mit vorhandenen lokalen Systemen integriert werden. Sämtliche Aktivitätsprotokolle für Abonnements, in denen ressourcenübergreifende Vorgänge auf der Steuerungsebene erfasst werden, sollten in Log Analytics gestreamt werden, damit sie in Übereinstimmung mit RBAC-Berechtigungen abgefragt und analysiert werden können.

- **Netzwerktopologie und -konnektivität**: Die End-to-End-Netzwerktopologie muss Azure-Regionen und lokale Umgebungen umfassen, um eine lückenlose Konnektivität zwischen Plattformbereitstellungen sicherzustellen. Erforderliche Dienste und Ressourcen (z. B. Firewalls und virtuelle Netzwerkgeräte) müssen so bestimmt, bereitgestellt und konfiguriert werden, dass sämtliche Sicherheitsanforderungen erfüllt sind.

- **Infrastruktur gemeinsamer Dienste**: Zentral gesteuerte, jedoch verteilt bereitgestellte Dienste wie Domänencontroller müssen so entworfen, konfiguriert und erstellt werden, dass Anwendungsteams erforderliche und gemeinsame Dienste und Ressourcen nutzen und integrieren können. Nicht alle traditionellen und gemeinsam genutzten lokalen Dienste sollten in der Cloud bereitgestellt werden. Dateifreigaben und Hardwaresicherheitsmodule sollten z. B. als Ressourcen auf Anwendungsebene betrachtet werden, die native Azure-Dienste nutzen.

- **DevOps**: Um eine sichere, wiederholbare und einheitliche Bereitstellung von Infrastructure-as-Code-Artefakten sicherzustellen, muss eine umfassende DevOps-Lösung mit zuverlässigen Verfahren für den Softwareentwicklungslebenszyklus entworfen, erstellt und bereitgestellt werden. Diese Artefakte müssen unter Verwendung von dedizierten Pipelines für Integration, Veröffentlichung und Bereitstellung, die eine umfassende, zuverlässige Quellcodeverwaltung und Nachverfolgbarkeit bieten, entwickelt, getestet und bereitgestellt werden.

Zusätzlich zu den hier aufgeführten Aspekten müssen bei Entwurf, Konfiguration, Bereitstellung und Integration der einzelnen Zielzonen die kritischen Anforderungen Ihrer Organisation im Zusammenhang mit folgenden Faktoren erfüllt werden:

- Geschäftskontinuität und Notfallwiederherstellung auf Plattform- und Anwendungsebene
- Dienstverwaltung, z. B. Reaktion auf Incidents und Support
- Einem Dienstkatalog (z. B. einer Konfigurationsverwaltungsdatenbank)

## <a name="high-level-architecture"></a>Allgemeine Architektur

[![Diagramm: Architektur für Cloud Adoption Framework-Zielzonen auf Unternehmensniveau](./media/ns-arch-inline.png)](./media/ns-arch-expanded.png#lightbox)

_Abbildung 2: Architektur für Cloud Adoption Framework-Zielzonen auf Unternehmensniveau_

Laden Sie die [PDF-Datei](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/ready/enterprise-scale-architecture.pdf) herunter, die dieses Architekturdiagramm enthält.

## <a name="next-steps"></a>Nächste Schritte

Passen Sie die Implementierung dieser Architektur unter Berücksichtigung der Entwurfsleitfäden für das Cloud Adoption Framework auf Unternehmensniveau an.

> [!div class="nextstepaction"]
> [Entwurfsrichtlinien](./design-guidelines.md)
