---
title: Schaffen von Hybrid Cloud-Konsistenz
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um zu erfahren, wie Sie den Ansatz zum Schaffen von Hybrid Cloud-Konsistenz definieren.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/27/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 68b360af15f6a2537fb077202373c846365266d2
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/27/2020
ms.locfileid: "80353657"
---
<!-- cSpell:ignore ISVs Bitnami Yourhosting Revera Avanade Pulsant PricewaterhouseCoopers Pointnext -->

# <a name="create-hybrid-cloud-consistency"></a>Schaffen von Hybrid Cloud-Konsistenz

Dieser Artikel führt Sie durch allgemeine Ansätze zum Erzeugen von Hybrid Cloud-Konsistenz.

Hybridbereitstellungsmodelle können während der Migration das Risiko minimieren und zu einem problemlosen Übergang der Infrastruktur beitragen. Cloudplattformen bieten das höchste verfügbare Maß an Flexibilität bei Geschäftsprozessen. Viele Organisationen zögern damit, den Schritt in die Cloud zu wagen. Stattdessen bevorzugen sie, die vollständige Kontrolle über ihre vertraulichsten Daten zu behalten. Leider ermöglichen lokale Server nicht das gleiche Maß an Innovationen wie die Cloud. Eine Hybrid Cloud-Lösung bietet die Geschwindigkeit von Innovationen in der Cloud und die Kontrolle einer lokalen Verwaltung.

## <a name="integrate-hybrid-cloud-consistency"></a>Integrieren von Hybrid Cloud-Konsistenz

Durch die Verwendung einer Hybrid Cloud-Lösung können Unternehmen Rechenressourcen skalieren. Außerdem ist damit weniger Kapitalaufwand erforderlich, um kurzfristige Spitzen im Bedarf zu kompensieren. Veränderte Geschäftsbedingungen können die Freigabe lokaler Ressourcen für vertraulichere Daten oder Anwendungen erforderlich machen. Es ist einfacher, schneller und günstiger, die Bereitstellung von Cloudressourcen aufzuheben. Sie bezahlen nur für die Ressourcen, die Ihre Organisation vorübergehend nutzt, und müssen keine zusätzlichen Ressourcen erwerben und verwalten. Dieser Ansatz reduziert die Menge der Geräte, die über einen längeren Zeitraum ungenutzt bleiben könnten. Hybrid Cloud-Computing bietet alle Vorzüge des Cloud Computings – Flexibilität, Skalierbarkeit und Kosteneffizienz – bei gleichzeitig niedrigstem Risiko für Datenenthüllungen.

![Erstellen von Hybrid Cloud-Konsistenz für Identitäten, Verwaltung, Sicherheit, Daten, Entwicklung und DevOps](../../_images/hybrid-consistency.png)
*Abbildung 1: Erstellen von Hybrid Cloud-Konsistenz für Identitäten, Verwaltung, Sicherheit, Daten, Entwicklung und DevOps.*

Eine echte Hybrid Cloud-Lösung muss vier Komponenten bereitstellen, von denen jede entscheidende Vorteile bietet:

- **Einheitliche Identitäten für lokale und cloudbasierte Anwendungen:** Diese Komponente verbessert die Produktivität der Benutzer, da diese das einmalige Anmelden (SSO) für alle ihre Anwendungen nutzen können. Zusätzlich wird Konsistenz gewährleistet, da Anwendungen und Benutzer die Grenzen von Netzwerk oder Cloud überschreiten können.
- **Integrierte Verwaltung und Sicherheit in der Hybrid Cloud:** Diese Komponente verschafft Ihnen einen zentralen Ort zum Überwachen, Verwalten und Schützen der Umgebung bei mehr Transparenz und Kontrolle.
- **Eine einheitliche Datenplattform für das Rechenzentrum und die Cloud:** Diese Komponente schafft Datenportabilität und sorgt für einen nahtlosen Zugriff auf lokale und cloudbasierte Datendienste und damit für umfassendere Einblicke in alle Datenquellen.
- **Konsistenz bei Entwicklung und DevOps in Cloud- und lokalen Rechenzentren:** Diese Komponente gestattet es Ihnen, Anwendungen nach Bedarf zwischen den beiden Umgebungen zu verschieben. Die Produktivität der Entwickler verbessert sich, da beide Orte nun dieselbe Entwicklungsumgebung haben.

Hier finden Sie einige Beispiele für diese Komponenten aus Sicht von Azure:

- Azure Active Directory (Azure AD) arbeitet mit dem lokalen Azure Directory zusammen, um allen Benutzern eine einheitliche Identität bereitzustellen. SSO für lokale und cloudbasierte Anwendungen macht es Benutzern einfach, sicher auf die Anwendungen und Ressourcen zuzugreifen, die sie benötigen. Administratoren können Sicherheits- und Governance-Kontrollen verwalten und besitzen ferner die Flexibilität, Berechtigungen anpassen zu können, ohne die Benutzererfahrung zu beeinträchtigen.
- Azure bietet integrierte Verwaltungs- und Sicherheitsdienste für die Cloud- und die lokale Infrastruktur. Diese Dienste umfassen einen integrierten Satz von Tools, die zum Überwachen, Konfigurieren und Schützen von Hybrid Clouds verwendet werden. Dieser umfassende Ansatz bei der Verwaltung hilft insbesondere bei realen Problemen, denen Organisationen gegenüber stehen, die eine Hybrid Cloud-Lösung in Betracht ziehen.
- Azure Hybrid Cloud stellt Tools bereit, die einen sicheren, nahtlosen und effizienten Zugriff auf sämtliche Daten gewährleisten. Azure-Datendienste sorgen in Kombination mit Microsoft SQL Server für eine konsistente Datenplattform. Ein konsistentes Hybrid Cloud-Modell ermöglicht Benutzern das Arbeiten mit sowohl Betriebs- als auch analytischen Daten. Dieselben Dienste werden lokal und in der Cloud für Data Warehousing, Datenanalyse und Datenvisualisierung bereitgestellt.
- Azure-Clouddienste und ein lokaler Azure Stack ermöglichen einheitliche Vorgehensweisen bei Entwicklung und DevOps. Konsistenz in der Cloud und lokal vor Ort bedeutet, dass Ihr DevOps-Team Anwendungen erstellen kann, die in beiden Umgebungen ausgeführt und problemlos am richtigen Standort bereitgestellt werden können. Sie können Vorlagen auch in der Hybridlösung wiederverwenden und so DevOps-Prozesse noch weiter vereinfachen.

## <a name="azure-stack-in-a-hybrid-cloud-environment"></a>Azure Stack in einer Hybrid Cloud-Umgebung

Azure Stack ist eine Hybrid Cloud-Lösung, mit der Organisationen mit Azure konsistente Dienste in ihren Rechenzentren ausführen können. Sie bietet vereinfachte Entwicklung, Verwaltung und Sicherheit durch eine einheitliche Benutzeroberfläche der Azure-Dienste für die öffentliche Cloud. Azure Stack ist eine Erweiterung von Azure. Sie können sie verwenden, um Azure-Dienste aus Ihren lokalen Umgebungen heraus auszuführen. Sie können dann entscheiden, ob und wann Sie den Schritt in die Azure-Cloud wagen.

Azure Stack erlaubt es Ihnen, IaaS und PaaS bereitzustellen und zu betreiben und dafür die gleichen Tools und Umgebungen zu nutzen wie in der öffentlichen Azure-Cloud. Für die Verwaltung von Azure Stack – über das Webportal oder mithilfe von PowerShell – steht IT-Administratoren und Endbenutzern mit Azure eine einheitliche Oberfläche zur Verfügung.

Azure und Azure Stack eröffnen gänzlich neue Hybridanwendungsfälle für Kundenanwendungen und interne Branchenanwendungen:

- **Edgelösungen und nicht vernetzte Lösungen**: Kunden können den Anforderungen im Hinblick auf Wartezeit und Konnektivität gerecht werden, indem sie Daten lokal in Azure Stack verarbeiten und dann zur weiteren Analyse in Azure aggregieren. In beiden Fällen können sie eine gemeinsame Anwendungslogik verwenden. Für dieses Edgeszenario interessieren sich viele Kunden aus unterschiedlichen Kontexten, z. B. Fertigungshallen, Kreuzfahrtschiffe und Bergbauminen.
- **Cloudanwendungen, die verschiedene Bestimmungen erfüllen**: Kunden können ihre Anwendungen in Azure entwickeln und dort bereitstellen. Dank vollständiger Flexibilität können sie dieselben Anwendungen mithilfe von Azure Stack in ihrer lokalen Umgebung bereitstellen, um gesetzliche oder richtlinienbasierte Anforderungen zu erfüllen. Hierzu sind keine Codeänderungen erforderlich. Anwendungsbeispiele hierfür sind globale Überwachung, Finanzberichte, Devisenhandel, Onlinespiele und Spesenabrechnungen. Manchmal möchten Kunden je nach geschäftlichen oder technischen Anforderungen verschiedene Instanzen derselben Anwendung in Azure oder Azure Stack bereitstellen. Während Azure die meisten Anforderungen erfüllt, ergänzt Azure Stack das Bereitstellungskonzept, falls erforderlich.
- **Lokales Cloudanwendungsmodell**: Kunden können Azure-Webdienste, Container, Microservices und serverlose Architekturen verwenden, um vorhandene Anwendungen zu aktualisieren und zu erweitern oder neue Anwendungen zu erstellen. Nutzen Sie konsistente DevOps-Prozesse in Azure (in der Cloud) sowie in Azure Stack (lokal). Die Modernisierung von Anwendungen wird immer interessanter – und dies schließt auch unternehmenskritische Anwendungen ein.

Azure Stack wird in zwei Bereitstellungsoptionen angeboten:

- **Integrierte Azure Stack-Systeme**: Integrierte Azure Stack-Systeme werden von Microsoft und Hardwarepartnern angeboten. Dadurch entsteht eine ausgewogene Lösung mit cloudbasierten Innovationen und komfortabler Verwaltung. Bei Azure Stack handelt es sich um ein integriertes System aus Hardware und Software. Somit bietet die Plattform Flexibilität und Kontrolle bei gleichzeitiger Bereitstellung von cloudbasierten Innovationen. Integrierte Azure Stack-Systeme gibt es in Größen von 4 bis 12 Knoten. Sie werden gemeinsam vom Hardwarepartner und von Microsoft unterstützt. Mit integrierten Azure Stack-Systemen ermöglichen Sie neue Szenarien für Ihre Produktionsworkloads.
- **Azure Stack Development Kit**: Das Microsoft Azure Stack Development Kit ist eine Bereitstellung von Azure Stack mit einem Knoten. Sie können es verwenden, um Azure Stack zu evaluieren und kennen zu lernen. Sie können das Kit auch für Entwicklungsarbeiten mit APIs und Tools verwenden, die mit Azure konsistent sind. Das Azure Stack Development Kit ist nicht für die Verwendung als Produktionsumgebung konzipiert.

## <a name="azure-stack-one-cloud-ecosystem"></a>Azure Stack-Ökosystem mit einer Cloud

Sie können Azure Stack-Initiativen beschleunigen, indem Sie das vollständige Azure-Ökosystem nutzen:

<!-- cSpell:ignore ISVs Bitnami Yourhosting Revera Avanade Pulsant PricewaterhouseCoopers -->

- Azure stellt sicher, dass die meisten Anwendungen und Dienste, die für Azure zertifiziert sind, auch in Azure Stack funktionieren. Mehrere unabhängige Softwarehersteller (ISVs) erweitern ihre Lösungen auf Azure Stack. Zu diesen ISVs gehören Bitnami, Docker, Kemp Technologies, Pivotal Cloud Foundry, Red Hat Enterprise Linux und SUSE Linux.
- Sie können Azure Stack wahlweise als einen vollständig verwalteten Dienst bereitstellen und betreiben. Mehrere Partner werden in Kürze Angebote für verwaltete Dienste in Azure und Azure Stack anbieten. Zu diesen Partnern gehören Tieto, Yourhosting, Revera, Pulsant und NTT. Diese Partner liefern verwaltete Dienste für Azure durch das Cloud Solution Provider-Programm (CSP). Sie erweitern ihre Angebote um die Einbeziehung von Hybridlösungen.
- Als Beispiel für eine umfassende, vollständig verwaltete Hybrid Cloud Lösung bietet Avanade ein All-in-One-Angebot. Es umfasst Cloudtransformationsdienste, Software, Infrastruktur, Einrichtung und Konfiguration sowie kontinuierlich verwaltete Dienste. Auf diese Weise können Kunden Azure Stack genauso nutzen, sie es heute mit Azure tun.
- Anbieter können dazu beitragen, Modernisierungsinitiativen für Anwendungen zu beschleunigen, indem sie für die Kunden End-to-End-Lösungen mit Azure erstellen. Sie verfügen über umfassende Kenntnisse zu Azure sowie Fach- und Branchenwissen und kennen sich mit Prozessen aus, z. B. DevOps. Jede Azure Stack-Cloud ist für einen Anbieter die Möglichkeit, die Lösung zu entwerfen und die Systembereitstellung anzuleiten und zu beeinflussen. Darüber hinaus können sie die enthaltenen Funktionen anzupassen und Betriebsaktivitäten umzusetzen. Beispiele für Anbieter sind u. a. Avanade, DXC, Dell EMC Services, InFront Consulting Group, HPE Pointnext und PwC (früher PricewaterhouseCoopers).
