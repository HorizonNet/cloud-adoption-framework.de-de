---
title: Grundlegendes zu Cloudgovernancefunktionen
description: Grundlegendes zu den Funktionen eines Cloudgovernanceteams, einschließlich der Quelle, des Umfangs und der Ergebnisse.
author: JanetCThomas
ms.author: janet
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.topic: conceptual
ms.date: 05/15/2020
ms.openlocfilehash: dfa8275bb96fc075e099b19c9c4b9b81d1714131
ms.sourcegitcommit: 9a84c2dfa4c3859fd7d5b1e06bbb8549ff6967fa
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/21/2020
ms.locfileid: "83755594"
---
<!-- docsTest:ignore IS -->

# <a name="cloud-governance-functions"></a>Cloudgovernancefunktionen

Mit einem Cloudgovernanceteam wird sichergestellt, dass Risiken und die Risikotoleranz richtig ausgewertet und verwaltet werden. Dieses Team sorgt dafür, dass Risiken, die für das Unternehmen nicht tolerierbar sind, richtig identifiziert werden. Die Mitarbeiter dieses Teams steuern Risiken mithilfe von Unternehmensrichtlinien.

Je nach den gewünschten Geschäftsergebnissen umfassen die Fähigkeiten, die zur Bereitstellung umfassender Cloudgovernancefunktionen erforderlich sind, folgende:

- IT-Governance
- Unternehmensarchitektur
- Sicherheit
- IT-Abläufe
- IT-Infrastruktur
- Netzwerk
- Identity
- Virtualisierung
- Business Continuity & Disaster Recovery
- Anwendungsbesitzer im IT-Bereich
- Besitzer im Finanzbereich

Diese Baselinefunktionen helfen Ihnen bei der Identifizierung von Risiken in Bezug auf aktuelle und zukünftige Releases. Diese Bemühungen helfen Ihnen beim Evaluieren von Risiken, dem Verstehen der potenziellen Auswirkungen sowie beim Treffen von Entscheidungen zur Risikotoleranz. Hierbei können Sie Pläne schnell aktualisieren, um die sich ändernden Anforderungen des [Cloudmigrationsteams](./cloud-migration.md) widerzuspiegeln.

## <a name="preparation"></a>Vorbereitung

- Informieren Sie sich über die [Cloudgovernance-Methodik](../govern/index.md).
- Führen Sie die [Governance-Benchmarkbewertung](../govern/benchmark.md) durch.
- [Sicherheit, Verantwortung und Vertrauenswürdigkeit in Azure](https://docs.microsoft.com/learn/modules/intro-to-security-in-azure): Lernen Sie die grundlegenden Konzepte kennen, um Ihre Infrastruktur und Daten in der Cloud zu schützen. Verstehen Sie, wo Ihre Zuständigkeiten liegen und was Azure für Sie übernimmt.
- Erfahren Sie, wie Sie gruppenübergreifend arbeiten können, um [Kosten zu verwalten](../organize/cost-conscious-organization.md).

## <a name="minimum-scope"></a>Mindestumfang

- Verstehen der mit dem Plan verbundenen [Geschäftsrisiken](../govern/policy-compliance/risk-tolerance.md).
- Darstellen der [Risikotoleranz des Unternehmens](../govern/policy-compliance/risk-tolerance.md).
- Hilfe bei der Erstellung eines [Governance-MVP](../govern/guides/index.md).

Beteiligen Sie die folgenden Teilnehmer an Cloudgovernanceaktivitäten:

- Führungskräfte aus dem mittleren Management und direkt Mitwirkende in Schlüsselrollen sollten das Unternehmen repräsentieren und an der Evaluierung von Risikotoleranzen mitarbeiten.
- Die Cloudgovernancefunktionen werden durch eine Erweiterung des [Cloudstrategieteams](./cloud-strategy.md) bereitgestellt. Ebenso wie vom CIO und den betriebswirtschaftlichen Führungskräften erwartet wird, dass sie sich an Funktionen für die Cloudstrategie beteiligen, wird von ihren direkt unterstellten Mitarbeitern erwartet, dass sie sich an Aktivitäten für die Cloudgovernance beteiligen.
- Mitarbeiter aus dem betriebswirtschaftlichen Bereich, die der Geschäftseinheit angehören, die eng mit der Bereichsleistung zusammenarbeitet, sollten in die Lage versetzt werden, Entscheidungen in Bezug auf unternehmensbezogene und technische Risiken zu treffen.
- Für die Informationstechnologie (IT) und die Informationssicherheit (IS) zuständige Mitarbeiter, die sich mit den technischen Aspekten der Cloudtransformation auskennen, können wechselnde Funktionen ausfüllen, anstatt nur für die Cloudgovernancefunktionen.

## <a name="deliverable"></a>Ergebnisse

Die Mission der Cloudgovernance besteht im Erzielen einer Balance zwischen konkurrierenden Zielen in Bezug auf die Transformation und die Risikominderung. Darüber hinaus wird per Cloudgovernance sichergestellt, dass das [Cloudmigrationsteam](./cloud-migration.md) die Daten- und Ressourcenklassifizierung sowie die Architekturrichtlinien beachtet, denen die Einführung unterliegt. Governanceteams oder Einzelpersonen arbeiten auch mit dem [Cloudkompetenzzentrum](../organize/cloud-center-of-excellence.md) zusammen, um automatisierte Ansätze auf die Steuerung von Cloudumgebungen anzuwenden.

**Fortlaufende monatliche Aufgaben:**

- Verstehen von [Geschäftsrisiken](../govern/policy-compliance/risk-tolerance.md), die sich aus jedem Release ergeben.
- Darstellen der [Risikotoleranz des Unternehmens](../govern/policy-compliance/risk-tolerance.md).
- Leisten von Hilfestellung bei der inkrementellen Verbesserung von [Anforderungen an Richtlinien und Konformität](../govern/policy-compliance/index.md).

**Rhythmus von Besprechungen:**

Die Zeit, die hierfür von den einzelnen Teammitgliedern des Cloudgovernanceteams aufgewendet wird, macht einen großen Prozentsatz ihres täglichen Zeitplans aus. Beiträge sind nicht nur auf Besprechungen und Feedbackzyklen beschränkt.

## <a name="out-of-scope"></a>Nicht betreffende Organisationen

Je umfangreicher die Einführung wird, desto schwieriger ist es möglicherweise für das Cloudgovernanceteam, mit dem Innovationsfluss Schritt zu halten. Dies gilt insbesondere, wenn Ihre Umgebung hohe Anforderungen an Compliance, Betrieb und Sicherheit stellt. Wenn dies der Fall ist, können Sie einige Verantwortlichkeiten in ein vorhandenes IT-Team verlagern, um den Umfang für das Governanceteam zu reduzieren.

## <a name="next-steps"></a>Nächste Schritte

Einige große Organisationen verfügen über dedizierte Teams speziell für die IT-Governance. Diese Teams sind auf das Risikomanagement für das gesamte IT-Portfolio spezialisiert. Wenn diese Teams vorhanden sind, können die folgenden Entwicklungsmodelle beschleunigt werden. Für das für IT-Governance zuständige Team ist es aber ratsam, sich über das Cloudgovernancemodell zu informieren, um zu verstehen, wie sich die Governance in der Cloud etwas verschiebt. Wesentliche Artikel behandeln das Erweitern der Unternehmensrichtlinie auf die Cloud sowie „Die fünf Disziplinen der Cloudgovernance“.
Keine Governance: Es kommt häufig vor, dass Organisationen die Umstellung auf die Cloud ohne klare Planung für die Governance durchführen. Nach kurzer Zeit führen dann Bedenken in Bezug auf Sicherheit, Kosten, Skalierung und Abläufe zu Diskussionen über ein Governancemodell sowie über Personal für die Prozesse, die für dieses Modell erforderlich sind. Ein wichtiger erster Schritt besteht immer darin, mit dieser Diskussion zu beginnen, bevor es zu diesen Bedenken kommt. Auf diese Weise kann das Antimuster „Keine Governance“ vermieden werden. Der Abschnitt zum Definieren der Unternehmensrichtlinie enthält Informationen zu dieser Diskussion.

**Blockade der Governance:** Wenn Bedenken in Bezug auf Sicherheit, Kosten, Skalierung und Abläufe nicht beachtet werden, kann es passieren, dass Projekte und Geschäftsziele blockiert werden. Ohne richtige Governance entstehen Zweifel, Unsicherheiten und sogar Ängste bei Projektbeteiligten und Technikern. Verhindern Sie dies, indem Sie rechtzeitig Maßnahmen ergreifen. Die beiden Governanceleitfäden im Framework für die Cloudeinführung (Cloud Adoption Framework) dienen Ihnen als Hilfe beim Festlegen von ersten einschränkenden Richtlinien, um Angst, Unsicherheit und Zweifel zu reduzieren und die Governance im Laufe der Zeit weiterzuentwickeln. Sie können zwischen dem Leitfaden für komplexe Unternehmen und dem Standardunternehmensleitfaden wählen.

**Freiwillige Governance:** Es gibt in jedem Unternehmen mutige Menschen. Diese wenigen tapferen Personen, die einspringen und dem Team helfen, lernen aus ihren Fehlern. Häufig ist dies der Beginn von Governance. Dies gilt vor allem für kleinere Unternehmen. Diese Personen wenden freiwillig Zeit auf, um Probleme zu beheben und Cloudeinführungsteams zur Verwendung von gut verwalteten bewährten Methoden zu bewegen.

Die Anstrengungen dieser Personen sind deutlich besser als die Szenarien „Keine Governance“ oder „Blockade der Governance“. Diese Arbeit ist zwar sehr lobenswert, aber dieser Ansatz sollte nicht mit Governance verwechselt werden. Für richtige Governance ist mehr erforderlich als nur die sporadische Unterstützung zur Erzielung von Einheitlichkeit (dem Ziel jedes guten Governanceansatzes). Die Informationen unter „Die fünf Disziplinen der Cloudgovernance“ können hierbei als Hilfe dienen.

**Cloudverwalter:** Diese Bezeichnung (Englisch: Cloud Custodian) ist für viele Cloudarchitekten, die auf die frühen Phasen der Governance spezialisiert sind, zu einer Auszeichnung geworden. Zu Beginn der Governancemethoden scheinen die Ergebnisse den Resultaten der Personen, die freiwillig an die Governance herangehen, zu ähneln. Es gibt aber einen grundlegenden Unterschied. Ein Cloudverwalter hat einen Plan im Kopf. In dieser Phase der Entwicklung muss das Team Zeit dafür aufwenden, die Unordnung zu beseitigen, die von den Cloudarchitekten nach dem vorherigen Schritt hinterlassen wurde. Der Cloudverwalter richtet seine Arbeit aber nach der gut strukturierten Unternehmensrichtlinie aus. Außerdem nutzt er Governancetools, die beispielsweise im Governance-MVP beschrieben sind.

Ein weiterer grundlegender Unterschied zwischen einem Cloudverwalter und einem freiwilligen Governance-Akteur besteht in der Unterstützung durch die Führungsebene. Der Freiwillige leistet zusätzliche Stunden über die normalen Erwartungen hinaus, weil er lernen und aktiv sein möchte. Der Cloudverwalter erhält Unterstützung von der Führungsebene, was die Reduzierung der täglichen Aufgaben betrifft. So wird sichergestellt, dass regelmäßig Zeit zur Verfügung steht, die für die Verbesserung der Cloudgovernance genutzt werden kann.

**Cloudwächter:** Wenn sich die Governancemethoden verfestigen und von den Teams für die Cloudeinführung akzeptiert werden, kommt es zu einer geringfügigen Änderung der Rolle von Cloudarchitekten, die auf Governanceänderungen spezialisiert sind. Dies gilt auch für die Rolle des Teams für die Cloudgovernance. Meist fallen die besser entwickelten Methoden anderen Experten auf, die dann dazu beitragen können, den durch Governanceimplementierungen erzielten Schutz zu stärken.

Der Unterschied ist zwar subtil, aber beim Erstellen einer governancebezogenen IT-Kultur von entscheidender Bedeutung. Ein Cloudverwaltungsberechtigter räumt das Chaos auf, das von innovativen Cloudarchitekten hinterlassen wird, und zwischen den beiden Rollen gibt es natürliche Reibung und gegensätzliche Ziele. Ein Cloudwächter hält die Cloud sicher, damit andere Cloudarchitekten mit weniger Chaos schneller vorankommen.
Cloudwächter beginnen mit der Nutzung von anspruchsvolleren Governanceansätzen, um die Plattformbereitstellung zu beschleunigen und Teams beim eigenständigen Erfüllen ihrer Anforderungen an die Umgebung zu unterstützen, damit sie schneller vorankommen. Beispiele für diese anspruchsvolleren Funktionen sind in den inkrementellen Verbesserungen des Governance-MVP enthalten, z. B. in der Verbesserung der Sicherheitsbaseline.

**Cloudbeschleuniger:** Cloudwächter und Cloudverwalter nutzen auf natürliche Weise Skripts und Governancetools, mit denen die Bereitstellung von Umgebungen, Plattformen oder auch Komponenten verschiedener Anwendungen beschleunigt wird. Die Aufbereitung und Freigabe dieser Skripts zusätzlich zu den zentralen Governanceaufgaben verschafft diesen Architekten viel Respekt im gesamten IT-Bereich.

Diese Governancefachleute, die ihre aufbereiteten Skripts offen zur Verfügung stellen, sorgen dafür, dass Technologieprojekte schneller bereitgestellt werden können und die Governance in die Architektur der Workloads eingebettet wird. Durch diesen Einfluss auf die Workload und die Unterstützung guter Entwurfsmuster werden Cloudbeschleuniger auf eine höhere Ebene der Governancespezialisten gehoben.

**Globale Governance:** Wenn Organisationen von der Erfüllung global verteilter IT-Anforderungen abhängig sind, kann es in verschiedenen geografischen Regionen zu erheblichen Abweichungen in Bezug auf den Betrieb und die Governance kommen. Die Anforderungen von Geschäftseinheiten und sogar Anforderungen an die lokale Datenhoheit können dazu führen, dass die bewährten Governancemethoden mit den erforderlichen Abläufen kollidieren. In diesen Szenarien ermöglicht ein mehrstufiges Governancemodell eine geringstmögliche Konsistenz und Governance vor Ort. Der Artikel zum Thema „Mehrere Governance-Ebenen“ enthält weitere Informationen dazu, wie Sie diese Entwicklungsstufe erreichen.

Jedes Unternehmen ist einzigartig, und dies gilt auch für die jeweiligen Governanceanforderungen. Wählen Sie die Entwicklungsstufe, die zu Ihrer Organisation passt, und verwenden Sie das Framework für die Cloudeinführung (Cloud Adoption Framework) als Anleitung für die Methoden, Prozesse und Tools, um diese Stufe zu erreichen.

Während der Weiterentwicklung der Cloudgovernance werden Teams in die Lage versetzt, die Einführung der Cloud schneller zu betreiben. Wenn weiter kontinuierlich an der Cloudeinführung gearbeitet wird, werden in der Regel auch die anderen IT-Abläufe weiterentwickelt. Stellen Sie entweder ein Cloudbetriebsteam auf, oder sprechen Sie sich mit Ihrem Cloudbetriebsteam ab, um sicherzustellen, dass Governance Teil der Entwicklungsmaßnahmen für den Operations-Bereich ist.

Erfahren Sie mehr über das Starten eines [Cloudgovernanceteams](../get-started/team/cloud-governance.md) oder eines [Cloudbetriebsteams](../get-started/team/cloud-operations.md).

Nachdem Sie eine anfängliche [Cloudgovernancegrundlage](../govern/initial-foundation.md) geschaffen haben, verwenden Sie diese bewährten Methoden in [Verbesserungen der Governancegrundlage](../govern/foundation-improvements.md), um Ihren Einführungsplan umzusetzen und Risiken zu verhindern.
