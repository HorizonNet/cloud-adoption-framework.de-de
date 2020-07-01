---
title: Architektur für CAF-Zielzonen auf Unternehmensebene
description: Architektur für CAF-Zielzonen auf Unternehmensebene.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: csu
ms.openlocfilehash: fad625eb7b2cd1ebcfefe3a5ac27be6682ad00d2
ms.sourcegitcommit: 7c16b2857b00520bec3c4f6e9844ceac33970846
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/01/2020
ms.locfileid: "85766850"
---
<!-- cSpell:ignore CAF -->

# <a name="cloud-adoption-framework-enterprise-scale-landing-zone-architecture"></a>Cloud Adoption Framework – Architektur für Zielzonen auf Unternehmensebene

Mit dieser Architektur der Unternehmensebene werden eine Vorgehensweise und eine Referenzimplementierung für eine effektive Erstellung und Operationalisierung von Zielzonen in Azure beschrieben, die auf die Azure-Roadmap und das Microsoft Cloud Adoption Framework für Azure abgestimmt sind.

## <a name="an-overview-of-enterprise-scale-landing-zone-architecture"></a>Übersicht über die Architektur für Zielzonen auf Unternehmensebene

Die Architektur für CAF-Zielzonen auf Unternehmensebene stellt den strategischen Entwurfspfad und den technischen Zielstatus für die Azure-Umgebung des Kunden dar. Sie wird weiterhin gemeinsam mit der Azure-Plattform weiterentwickelt und letztendlich durch die verschiedenen Entwurfsentscheidungen definiert, die Organisationen zum Festlegen ihrer Azure-Journey treffen müssen.

Da Unternehmen Azure auf unterschiedliche Weise nutzen, variieren CAF-Architekturen für Zielzonen auf Unternehmensebene abhängig von der jeweiligen Implementierung eines Kunden. Aufgrund der technischen Überlegungen und Entwurfsempfehlungen innerhalb dieser Anleitung müssen Sie je nach Kundenszenario daher unterschiedliche Faktoren gegeneinander abwägen. Gewisse Abweichungen sind zu erwarten. Wenn jedoch die wichtigsten Empfehlungen befolgt werden, ebnet die resultierende Zielarchitektur den Weg für eine nachhaltigere Skalierung.

## <a name="landing-zone-expanded-definition"></a>Zielzone: Erweiterte Definition

Unter [Überlegungen zu Zielzonen](../../ready/considerations/index.md) finden Sie eine detaillierte Definition des Begriffs _Zielzone_. Für Unternehmen, die eine CAF-Zielzone auf Unternehmensebene implementieren möchten, ist jedoch eine noch genauere Definition erforderlich.

- **Bereich:** Um die Migration von Anwendungen und Greenfield-Projekte auf Unternehmensebene in Azure zu unterstützen, wird der Umfang einer Zielzone innerhalb der CAF-Zielzone auf Unternehmensebene erheblich erweitert. Durch diese Erweiterung lassen sich Entwürfe über das gesamte IT-Portfolio des Kunden hinweg skalieren und gehen damit weit über einen kurzfristigen Cloudeinführungsplan hinaus.

- **Refactoring:** Zur Unterstützung eines umfassenden IT-Portfolios auf Unternehmensebene können eine große Anzahl von Abonnements erforderlich sein. Im Cloud Adoption Framework wird zunächst ein häufiges Refactoring befürwortet. Bevor die zehnte Produktionsworkload bereitgestellt wird, sollte jedoch eine stabile Implementierung vorhanden sein. Wenn Sie mit einem Unternehmensportfolio arbeiten, lassen sich im Handumdrehen zehn Anwendungen bereitstellen. Ein Refactoring wird dadurch jedoch unpraktisch. Stattdessen sollte ein zentrales IT-Team oder Cloudkompetenzzentrum bei der ersten Veröffentlichung eine umfassendere Zielzone bereitstellen.

- **Ziel:** Um eine zu große Anzahl von Abonnements zu vermeiden, sollten Sie einheitliche Zielzonen verwenden, die auf einer Abonnementstrategie für Anwendungsarchetypen basieren. Erweitern Sie die Definition von erforderlichen Komponenten, um die Governance- und Complianceanforderungen eines cloudfähigen Unternehmens besser zu erfüllen. Siehe Abbildung unten.

- **Primärer Zweck:** Mit eingeschränkten Refaktoringmöglichkeiten und einer sorgfältig definierten Abonnementstrategie lassen sich die Zielzonen des Kunden schneller weiterentwickeln und ausbauen. Mit den CAF-Zielzonen auf Unternehmensebene wird der primäre Zweck der Zielzone erweitert, damit auch Aspekten wie Governance, Compliance, Sicherheit und Betriebsverwaltung Rechnung getragen werden kann. Jeder dieser Aspekte wird bei der ersten Veröffentlichung der Zielzonen und der unterstützenden gemeinsamen Dienste berücksichtigt.

Diese Vorgehensweise lässt sich mit einer Situation vergleichen, in der zunächst die Verfügbarkeit von Gas-, Wasser- und Stromleitungen sichergestellt wird, bevor neue Häuser gebaut werden. Im vorliegenden Kontext werden die Netzwerk-, Identitäts- und Zugriffsverwaltung sowie die Richtlinien, Verwaltung und Überwachung als gemeinsame Versorgungsdienste betrachtet, die für eine optimierte Anwendungsmigration verfügbar sein müssen, bevor der Vorgang gestartet wird.

![Zielzone](./media/lz-design.png)
_Abbildung 1: Zielzonenaufbau._

## <a name="expanded-list-of-requisite-components"></a>Erweiterte Liste der erforderlichen Komponenten

In der folgenden Liste sind weitere technische Konstrukte beschrieben, die im Kontext der Kundenanforderungen berücksichtigt und entwickelt werden müssen, um konforme technische Zielzonenumgebungen zu erstellen und eine erfolgreiche Azure-Einführung zu ermöglichen.

- **Identitäts- und Zugriffsverwaltung**: Sowohl für die Server- als auch für die Benutzerauthentifizierung muss eine Azure Active Directory-Implementierung entworfen und integriert werden. Um eine Trennung der Aufgabenbereiche und Berechtigungen für den Betrieb und die Verwaltung der Plattform zu erzwingen, muss die ressourcenbasierte Zugriffssteuerung (Role-Based Access Control, RBAC) modelliert und bereitgestellt werden. Für einen sicheren Zugriff auf Ressourcen und die Unterstützung von Vorgängen wie Rotation und Wiederherstellung muss eine Schlüsselverwaltungslösung entworfen und bereitgestellt werden. Abschließend werden Anwendungsbesitzern Zugriffsrollen auf Steuerungs- und Datenebene zugewiesen, um Ressourcen eigenständig erstellen und verwalten zu können.

- **Richtlinienverwaltung**: Auf der Azure-Zielplattform müssen ganzheitliche, zielzonenspezifische Richtlinien bestimmt, beschrieben, erstellt und bereitgestellt werden, mit denen unternehmens- und branchenspezifische sowie regulatorische Kontrollen implementiert werden. Mithilfe von Richtlinien sollte die Konformität von Anwendungen und zugrunde liegender Ressourcen ohne Abstraktion/Verwaltungsfunktion sichergestellt werden.

- **Verwaltung und Überwachung**: Es müssen ganzheitliche (horizontale) Funktionen für Ressourcenüberwachung und Warnungen auf Plattformebene entworfen, bereitgestellt und integriert werden. Operative Aufgaben wie das Patchen und Durchführen von Sicherungen müssen ebenfalls definiert und optimiert werden. Sicherheitsvorgänge sowie Funktionen für Überwachung und Protokollierung müssen entworfen und sowohl in Azure-Ressourcen als auch in vorhandenen lokalen Systemen integriert werden. Sämtliche Aktivitätsprotokolle für Abonnements, in denen Vorgänge auf Steuerungsebene erfasst werden, sollten in Log Analytics gestreamt werden, damit diese (in Übereinstimmung mit RBAC-Berechtigungen) abgefragt und analysiert werden können.

- **Netzwerktopologie und -konnektivität**: Die End-to-End-Netzwerktopologie muss Azure-Regionen und lokale Kundenumgebungen umfassen, um eine lückenlose Konnektivität zwischen Plattformbereitstellungen sicherzustellen. Erforderliche Dienste und Ressourcen (z. B. Firewalls und virtuelle Netzwerkgeräte) müssen so bestimmt, bereitgestellt und konfiguriert werden, dass sämtliche Sicherheitsanforderungen erfüllt sind.

- **Infrastruktur gemeinsamer Dienste**: Zentral gesteuerte, jedoch verteilt bereitgestellte Dienste wie Domänencontroller müssen so entworfen, konfiguriert und erstellt werden, dass Anwendungsteams erforderliche und gemeinsame Dienste und Ressourcen nutzen und integrieren können. Dabei ist es wichtig zu berücksichtigen, dass nicht alle traditionellen und gemeinsamen lokalen Dienste in der Cloud bereitgestellt werden sollten. Dateifreigaben und Hardwaresicherheitsmodule sollten z. B. als Ressourcen auf Anwendungsebene betrachtet werden, die native Azure-Dienste nutzen.

- **DevOps**: Um eine sichere, wiederholbare und einheitliche Bereitstellung von Infrastructure-as-Code-Artefakten sicherzustellen, muss eine umfassende DevOps-Lösung mit zuverlässigen Verfahren für den Softwareentwicklungslebenszyklus entworfen, erstellt und bereitgestellt werden. Diese Artefakte müssen unter Verwendung von dedizierten Pipelines für Integration, Veröffentlichung und Bereitstellung entwickelt, getestet und bereitgestellt werden, die eine umfassende, zuverlässige Quellcodeverwaltung und Nachverfolgbarkeit bieten.

Zusätzlich zu den oben aufgeführten Aspekten müssen bei Entwurf, Konfiguration, Bereitstellung und Integration der einzelnen Zielzonen die kritischen Kundenanforderungen im Zusammenhang mit folgenden Faktoren erfüllt werden:

- Geschäftskontinuität und Notfallwiederherstellung auf Plattform- und Anwendungsebene
- Dienstverwaltung wie Reaktion auf Vorfälle und Support
- Ein Dienstkatalog (z. B. eine Konfigurationsverwaltungsdatenbank)

## <a name="high-level-architecture"></a>Allgemeine Architektur

![Architektur für CAF-Zielzonen auf Unternehmensebene](./media/ns-arch.png)
_Abbildung 2: Architektur für CAF-Zielzonen auf Unternehmensebene._

_Laden Sie eine [Visio-Datei](https://github.com/microsoft/CloudAdoptionFramework/blob/master/ready/enterprise-scale-architecture.vsdx) herunter, die dieses Architekturdiagramm enthält._

## <a name="next-steps"></a>Nächste Schritte

Passen Sie die Implementierung dieser Architektur unter Berücksichtigung der [CAF-Entwurfsrichtlinien](./design-guidelines.md) an.

> [!div class="nextstepaction"]
> [Entwurfsrichtlinien](./design-guidelines.md)
