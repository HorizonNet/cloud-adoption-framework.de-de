---
title: Einführung in die Einhaltung gesetzlicher Bestimmungen
description: Hier finden Sie Informationen zu Konformitätsbestimmungen in verschiedenen Branchen und geografischen Regionen, die sich auf die Cloudgovernance auswirken können.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 0860dfc137b8aaa9ad39beeebb3856786eee1318
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83218304"
---
# <a name="introduction-to-regulatory-compliance"></a>Einführung in die Einhaltung gesetzlicher Bestimmungen

Dies ist ein einführender Artikel zur Einhaltung gesetzlicher Bestimmungen, der nicht für die Implementierung einer Compliancestrategie vorgesehen ist. Ausführlichere Informationen zu [Azure-Complianceangeboten](https://aka.ms/allcompliance) sind im [Microsoft Trust Center](https://www.microsoft.com/trust-center) verfügbar. Alle heruntergeladenen Dokumente sind zudem für bestimmte Azure-Kunden über das [Microsoft Service Trust-Portal](https://servicetrust.microsoft.com) verfügbar.

Die Einhaltung von Vorschriften bezieht sich auf die Disziplin und den Prozess, mit dem sichergestellt wird, dass ein Unternehmen die Gesetze befolgt, die von den Regierungsstellen in ihrer Region durchgesetzt werden, oder die Regeln, die durch freiwillig übernommene Industriestandards erforderlich sind. Im Rahmen der Einhaltung gesetzlicher Bestimmungen in der IT überwachen Personen oder Prozesse Unternehmenssysteme, um Verletzungen der durch geltende Gesetze, Bestimmungen und Standards festgelegten Richtlinien und Verfahren zu erkennen und zu verhindern. Dies betrifft wiederum einen großen Bereich von Überwachungs- und Erzwingungsprozessen. Je nach Branche und Region können sich diese Prozesse langwierig und komplex gestalten.

Compliance ist für multinationale Organisationen eine große Herausforderung, insbesondere in streng regulierten Branchen wie Gesundheitswesen und Finanzdienstleistungen. Es gelten viele Standards und Bestimmungen, die sich in bestimmten Fällen häufig ändern können. Dadurch ist es schwierig für Unternehmen, mit ständig weiterentwickelten internationalen Gesetzen zur elektronischen Datenverarbeitung Schritt zu halten.

Wie bei Sicherheitskontrollen sollten Organisationen sich über die Unterteilung der Zuständigkeiten bezüglich der Einhaltung gesetzlicher Bestimmungen in der Cloud im Klaren sein. Cloudanbieter bemühen sich sicherzustellen, dass ihre Plattformen und Dienste die gesetzlichen Bestimmungen einhalten. Unternehmen müssen aber auch bestätigen, dass ihre Anwendungen, die Infrastruktur, von der diese Anwendungen abhängen, und die von Drittanbietern bereitgestellten Dienste ebenfalls als konform zertifiziert sind.

Im Folgenden finden Sie Beschreibungen von behördlichen Vorschriften in verschiedenen Branchen und Regionen:

<!-- docsTest:ignore PHI "Health Information Portability and Accountability Act" -->

## <a name="hipaa"></a>HIPAA

Eine Anwendung im US-Gesundheitswesen, die geschützte gesundheitliche Informationen (Protected Health Information, PHI) verarbeitet, unterliegt sowohl den Regeln zur Privatsphäre als auch denen zur Sicherheit im Health Information Portability and Accountability Act (HIPAA). Als Minimum ist für HIPAA wahrscheinlich erforderlich, dass ein Unternehmen im Gesundheitswesen schriftliche Zusicherungen vom Cloudanbieter erhalten muss, dass alle empfangenen oder erstellten Patientendaten sicher verwahrt werden.

<!-- cSpell:ignore Visa Mastercard -->
<!-- docsTest:ignore "American Express" Discover JCB QSA ISA ROC SAQ DPO GRC -->

## <a name="pci"></a>PCI

Der Payment Card Industry Data Security Standard (PCI-DSS) ist ein proprietärer Informationssicherheitsstandard für Organisationen, die mit Markenkreditkarten großer Kartenschemas wie Visa, Mastercard, American Express, Discover und JCB umgehen. Der PCI-Standard wird von den Kartenmarken beauftragt und vom Payment Card Industry Security Standards Council verwaltet. Der Standard wurde erstellt, um die Kontrolle über die Daten von Karteninhabern zu verbessern und Kreditkartenbetrug zu verringern. Eine Überprüfung der Konformität wird jährlich durchgeführt – für Organisationen, die große Transaktionsvolumen verarbeiten, durch einen externen qualifizierten Sicherheitsbewerter oder einen firmenspezifischen internen Sicherheitsbewerter, der einen Konformitätsbericht erstellt, oder für Unternehmen durch einen Selbstbewertungsfragebogen.

## <a name="personal-data"></a>Personenbezogene Daten

Personenbezogene Informationen sind Informationen, anhand derer ein Kunde, Mitarbeiter, Partner oder eine sonstige natürliche oder juristische Person identifiziert werden kann. Viele neue Gesetze, insbesondere zu Datenschutz und personenbezogenen Daten, erfordern, dass die Unternehmen gesetzliche Bestimmungen eigenständig einhalten und Berichte zur Einhaltung und zu eventuell aufgetretenen Verletzungen erstellen.

## <a name="gdpr"></a>GDPR

Eine der wichtigsten Entwicklungen in diesem Bereich ist die Datenschutz-Grundverordnung (DSGVO) der Europäischen Kommission, die speziell entwickelt wurde, um den Schutz von Daten für Einzelpersonen innerhalb der Europäischen Union zu verbessern. Die DSGVO erfordert, dass Daten über Einzelpersonen, (wie Namen, Privatadressen, Fotos, E-Mail-Adressen, Bankdaten, Beiträge in sozialen Netzwerken, medizinische Informationen oder IP-Adressen eines Computers) auf Servern innerhalb der EU verwaltet und nicht an einen Ort außerhalb der EU übertragen werden. Sie erfordert auch, dass Unternehmen Personen über Datenschutzverletzungen benachrichtigen, und fordert, dass Unternehmen einen Datenschutzbeauftragten (DSB) haben müssen. Andere Länder haben ähnliche Arten von Vorschriften oder entwickeln diese derzeit.

## <a name="compliant-foundation-in-azure"></a>Konformitätsbasis in Azure

Um Kunden bei der Erfüllung ihrer eigenen Konformitätsverpflichtungen in regulierten Branchen und auf Märkten weltweit zu unterstützen, verfügt Azure über das größte Complianceportfolio der Branche – in der Breite (Gesamtanzahl von Angeboten), aber auch der Tiefe (Anzahl von kundenorientierten Diensten im Rahmen des Bewertungsbereichs). Die Azure-Complianceangebote sind in vier Segmente gruppiert:

- Global
- US Government
- Branche
- Länderspezifisch

Azure-Complianceangebote basieren auf unterschiedlichen Arten von Zusicherungen, z.B. formalen Zertifizierungen, Nachweisen, Validierungen, Autorisierungen und Bewertungen, die von unabhängigen externen Prüfungsgesellschaften erstellt wurden, sowie Vertragsänderungen, Selbstbewertungen und Kundenleitfäden, die von Microsoft erstellt wurden. Jede Angebotsbeschreibung in diesem Dokument enthält eine aktuelle Umfangserklärung, die angibt, welche Azure-Kundendienste für die Bewertung in Frage kommen, sowie Links zu herunterladbaren Ressourcen, um Kunden bei ihren eigenen Konformitätsverpflichtungen zu unterstützen.

Das Microsoft Trust Center bietet ausführlichere Informationen zu [Azure-Complianceangeboten](https://www.microsoft.com/trust-center/compliance/compliance-overview). Alle heruntergeladenen Dokumente sind zudem für bestimmte Azure-Kunden über das [Microsoft Service Trust-Portal](https://servicetrust.microsoft.com) in den folgenden Abschnitten verfügbar:

- **Überwachungsberichte:** Enthält Abschnitte zu FedRAMP, GRC-Bewertung, ISO, PCI-DSS und SOC-Berichten.
- **Datenschutzressourcen:** Enthält Konformitätsrichtlinien, häufig gestellte Fragen und Whitepaper sowie Abschnitte zu Penetrationstests und Sicherheitsbewertungen.

## <a name="next-steps"></a>Nächste Schritte

Informieren Sie sich über die Bereitschaft der Cloudsicherheit.

> [!div class="nextstepaction"]
> [Bereitschaft der Cloudsicherheit](./cloud-security-readiness.md)
