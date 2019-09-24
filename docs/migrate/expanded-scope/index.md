---
title: Checkliste für die Cloudmigration mit erweitertem Umfang
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Checkliste für die Cloudmigration mit erweitertem Umfang
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/19/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 4daf4b01a2fde83de1040f224b8096475a24fe60
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/24/2019
ms.locfileid: "71224358"
---
# <a name="expanded-scope-for-cloud-migration"></a>Erweiterter Umfang für die Cloudmigration

Der [Leitfaden zur Azure-Migration](../azure-migration-guide/index.md) im Cloud Adoption Framework ist der empfohlene Ausgangspunkt für Leser, die an einer Migration mit erneutem Hosten zu Azure interessiert sind, die auch als „Lift & Shift“-Migration bezeichnet wird. Dieser Leitfaden führt Sie durch eine Reihe von Voraussetzungen, Tools und Ansätzen für die Migration virtueller Computer in die Cloud.

Dieser Leitfaden ist zwar eine effektive Baseline, um Sie mit dieser Art von Migration vertraut zu machen, er geht aber von verschiedenen Annahmen aus. Diese Annahmen richten den Leitfaden mit einem großen Prozentsatz der Leser des Cloud Adoption Frameworks aus, indem sie einen vereinfachten Ansatz für Migrationen bieten. Dieser Abschnitt des Cloud Adoption Frameworks befasst sich mit einigen erweiterten Migrationsszenarien, die als Orientierungshilfe dienen, wenn diese Annahmen nicht zutreffen.

## <a name="cloud-migration-expanded-scope-checklist"></a>Checkliste für die Cloudmigration mit erweitertem Umfang

Die folgende Checkliste beschreibt die allgemeinen Komplexitätsbereiche, die eine Erweiterung des Umfangs der Migration über den [Leitfaden zur Azure-Migration](../azure-migration-guide/index.md) hinaus erfordern könnten.

- **Geschäftsorientierte Bereichsänderungen:**
  - [Ausgewogenheit des Portfolios](./balance-the-portfolio.md)
  - [Unterstützung globaler Märkte](../../decision-guides/regions/index.md)
  - Kostenbewusstsein während einer Migration *(ab Q3 2019 verfügbar)*
- **Kulturbedingte Bereichsänderungen:**
  - Change Management und Genehmigungsprozesse *(ab Q3 2019 verfügbar)*
  - Bereitschaft der Geschäftsleitung *(ab Q3 2019 verfügbar)*
  - [Qualifikationsbereitschaft](./suggested-skills.md)
  - Ausrichten des Supports (Partner, Dienste und Support) *(ab Q3 2019 verfügbar)*
- **Durch technische Strategie bedingte Bereichsänderungen:**
  - Bestehende Einschränkungen im Rechenzentrum *(ab Q3 2019 verfügbar)*
  - Skalierbare Migration – Hohes Volumen oder Geschwindigkeit von Migrationen *(ab Q3 2019 verfügbar)*
  - [Mehrere Rechenzentren](./multiple-datacenters.md)
  - [Datenanforderungen überschreiten Netzwerkkapazität](./network-capacity-exceeded.md)
  - Change Management und Lösungsdokumentation *(ab Q3 2019 verfügbar)*
  - [Strategie für Governance bzw. Compliance](./governance-or-compliance.md)
- **Workload-spezifische Umfangsänderungen:**
  - Entwerfen von Workloads für Resilienz *(ab Q3 2019 verfügbar)*
  - Ausrichten der Migration an Anwendungsmustern *(ab Q3 2019 verfügbar)*

Wenn eine dieser Komplexitäten mit Ihrem Szenario übereinstimmt, dann wird dieser Abschnitt des Cloud Adoption Frameworks wahrscheinlich die Art von Anleitung bieten, die erforderlich ist, um den Umfang der Migrationsprozesse ordnungsgemäß abzustimmen.

Jedes dieser Szenarien wird in den verschiedenen Artikeln in diesem Abschnitt des Cloud Adoption Frameworks behandelt.

## <a name="scope-options-explained"></a>Erläuterung der Umfangsoptionen

Damit Sie die einzelnen Szenarien zur Erweiterung des Umfangs besser verstehen, werden in der folgenden Liste die in der obigen Checkliste verwendeten Titel kurz zusammengefasst.

### <a name="business-driven-scope-changes"></a>Geschäftsorientierte Bereichsänderungen

- **Ausgleichen des Portfolios zur Cloudeinführung:** Das Cloudstrategieteam ist daran interessiert, verstärkt in die Migration (erneutes Hosting bestehender Workloads und Anwendungen mit minimalen Änderungen) oder in Innovationen (Refactoring oder erneutes Erstellen dieser Workloads und Anwendungen unter Verwendung moderner Cloudtechnologie) zu investieren. Häufig ist ein Gleichgewicht zwischen den beiden Prioritäten der Schlüssel zum Erfolg. In diesem Leitfaden ist das Thema zum Ausgleichen des Portfolios zur Cloudeinführung ein allgemeines Thema, das in jedem der Migrationsprozesse behandelt wird.
- **Unterstützung globaler Märkte:** Das Unternehmen ist in mehreren geografischen Regionen mit unterschiedlichen Anforderungen an die Datenhoheit tätig. Um diesen Anforderungen gerecht zu werden, sollten zusätzliche Überlegungen bei der erforderlichen Überprüfung und Verteilung der Ressourcen während der Migration berücksichtigt werden.

### <a name="culture-driven-scope-changes"></a>Kulturbedingte Bereichsänderungen

- **Change Management und Genehmigungsprozesse:** Wenn die Kultur Ihres Unternehmens komplex, hochgradig matrixartig strukturiert oder isoliert ist, werden die Prozesse im Zusammenhang mit Change Management und Genehmigungen zu einer Herausforderung. Hinweise zur Bewältigung dieser Komplexität finden sich in der Bewertung, Migration und Optimierung von Prozessen.
- **Bereitschaft der Geschäftsleitung:** Das richtige Maß an Unterstützung und Führung der Geschäftsleitung ist entscheidend für den Erfolg einer Migration. Wenn das Führungsteam nicht bereit ist, sich zu engagieren, dann wird die Unterstützung wahrscheinlich nicht folgen. Diese Komplexität wird in den Voraussetzungs- und Bewertungsprozessen behandelt.
- **Qualifikationsbereitschaft:** Wenn die Mitglieder des Cloudeinführungsteams oder andere unterstützende Teams nicht bereit sind, kann sich die Komplexität während des gesamten Migrationsvorgangs schnell erhöhen. Diese Herausforderung wird während jedes Migrationsprozesses auf einer speziellen Seite zur Qualifikationsbereitschaft behandelt.
- **Ausrichten des Supports (Partner-, Dienst- und Supportoptionen):** Innerhalb der einzelnen beschriebenen Prozesse gibt es Möglichkeiten, wie ein Partner, Dienste des Cloudanbieters und der Support des Cloudanbieters bei der Ausführung helfen können. In jedem der Prozessabschnitte werden die Optionen auf einer Seite zur Supportausrichtung weiter erläutert.

### <a name="technical-strategy-driven-scope-changes"></a>Durch technische Strategie bedingte Bereichsänderungen

- **Bestehende Einschränkungen im Rechenzentrum:** Unternehmen entscheiden sich häufig für eine Migration in die Cloud, da die Kapazität, Geschwindigkeit und Stabilität eines bestehenden Rechenzentrums nicht mehr zufriedenstellend ist. Leider erhöhen dieselben Einschränkungen die Komplexität des Migrationsprozesses, was eine zusätzliche Planung während der Bewertungs- und Migrationsprozesse erfordert.
- **Skalierbare Migration:** Migrationen mit mehr als 2.000 Ressourcen werden wahrscheinlich auf Einschränkungen stoßen, die eine zusätzliche Planung und einen disziplinierten Ansatz bei der Ausführung erfordern. Die Prozesse zur Bewertung und Migration werden an die Komplexität der Skalierung angepasst.
- **Mehrere Rechenzentren:** Die Migration mehrerer Rechenzentren erhöht die Komplexität erheblich. Während der Prozesse zur Bewertung, Migration, Optimierung und Verwaltung werden zusätzliche Überlegungen erläutert.
- **Change Management und Lösungsdokumentation:** Große digitale Bestände, komplexe Lösungsarchitekturen, langjährige technische Schulden und Abhängigkeiten können eine Komplexität schaffen, die während der Prozesse zur Bewertung, Migration und Optimierung behandelt werden sollte.
- **Strategie für Governance bzw. Compliance:** Wenn Governance und Compliance für den Erfolg einer Migration entscheidend sind, ist eine zusätzliche Abstimmung zwischen IT-Governanceteams und dem Cloudeinführungsteam erforderlich.

### <a name="workload-specific-scope-changes"></a>Workload-spezifische Umfangsänderungen

- **Entwerfen von Workloads für Resilienz:** Allgemeine Cloudentwurfsprinzipien können helfen, unternehmenskritische Workloads auf eine verbesserte Resilienz vorzubereiten. In diesem Artikel werden die Auswirkungen auf einen Migrationsprozess erläutert, wenn die Resilienz eine Workloadanforderung darstellt. Sie teilt auch einige allgemeine Prinzipien, die in die allgemeine Umgebungskonfiguration einzubeziehen sind, um die Resilienz für die Umgebung zu verbessern.
- **Ausrichten der Migration an Anwendungsmustern:** Das Migrationsmuster einer Workload kann sich auf den gewählten Migrationspfad auswirken. In diesem Artikel werden einige Umfangsänderungen beschrieben, die in die Arbeitselementebene eines Migrationsbacklogs integriert würden, um unterschiedliche Ansätze für die Migration pro Workload widerzuspiegeln.

## <a name="next-steps"></a>Nächste Schritte

Durchsuchen Sie das Inhaltsverzeichnis auf der linken Seite, um bestimmte Anforderungen oder Änderungen des Umfangs zu berücksichtigen. Alternativ ist die erste Umfangserweiterung in der Liste, [Ausgewogenheit des Portfolios](./balance-the-portfolio.md), ein guter Ausgangspunkt für die Überprüfung dieser Szenarien.

> [!div class="nextstepaction"]
> [Ausgewogenheit des Portfolios](./balance-the-portfolio.md)
