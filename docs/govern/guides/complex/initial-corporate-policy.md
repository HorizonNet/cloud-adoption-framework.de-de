---
title: 'Governance in komplexen Unternehmen: Anfängliche Unternehmensrichtlinie'
description: Verwenden Sie das Framework für die Cloudeinführung (Cloud Adoption Framework) für Azure, um die anfängliche Governanceposition, Risiken in der Anfangsphase, anfängliche Richtlinienanweisungen und Prozesse zur frühzeitigen Erzwingung zu definieren.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 470c84385606f1f7c5c36ec8e72b348aa6d4d8a5
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2020
ms.locfileid: "80995414"
---
# <a name="governance-guide-for-complex-enterprises-initial-corporate-policy-behind-the-governance-strategy"></a>Governanceleitfaden für komplexe Unternehmen: Anfängliche Unternehmensrichtlinie hinter der Governancestrategie

Die folgende Unternehmensrichtlinie definiert die anfängliche Governanceposition, die den Ausgangspunkt für diesen Leitfaden bildet. In diesem Artikel werden Risiken in einem frühen Stadium, anfängliche Richtlinienanweisungen und frühe Prozesse zum Durchsetzen von Richtlinienanweisungen definiert.

> [!NOTE]
>Die Unternehmensrichtlinie ist kein technisches Dokument, gibt aber den Anstoß zu vielen technischen Entscheidungen. Das in der [Übersicht](./index.md) beschriebene Governance-MVP ist letztlich von dieser Richtlinie abgeleitet. Vor der Implementierung eines Governance-MVP sollte Ihre Organisation eine Unternehmensrichtlinie entwickeln, die auf Ihren eigenen Zielen und geschäftlichen Risiken basiert.

## <a name="cloud-governance-team"></a>Cloudgovernanceteam

Der CIO hatte kürzlich eine Besprechung mit dem IT Governance-Team, um die Geschichte der Richtlinien für personenbezogene Informationen und der unternehmenskritischen Richtlinien zu verstehen und die Auswirkungen zu untersuchen, die eine Änderung dieser Richtlinien mit sich bringen würde. Dabei wurde auch das Gesamtpotenzial der Cloud für IT und das Unternehmen erörtert.

Nach der Besprechung baten zwei Mitglieder des IT-Governance-Teams um Erlaubnis, die Anstrengungen zur Cloudplanung zu erforschen und zu unterstützen. In Anerkennung der Notwendigkeit von Governance und der Möglichkeit, Schatten-IT zu begrenzen, fand diese Idee die Unterstützung des Leiters der IT-Governance. Mit diesem Schritt wurde das Cloudgovernanceteam aus der Taufe gehoben. Im Lauf der nächsten Monate wird es die Bereinigung vieler Fehler – aus der Governance-Perspektive – übernehmen, die während der Erkundung in der Cloud gemacht wurden. Das wird ihm den Spitznamen der _Cloudverwahrer_ einbringen. In späteren Iterationen lässt sich an diesem Leitfaden ablesen, wie sich seine Rolle im Lauf der Zeit ändert.

[!INCLUDE [business-risk](../../../../includes/business-risks.md)]

## <a name="tolerance-indicators"></a>Toleranzindikatoren

Die aktuelle Risikotoleranz ist hoch, und das Interesse an der Investition in die Cloud-Governance ist gering. Daher fungieren die Toleranzindikatoren als Frühwarnsystem, um die Investition von Zeit und Energie auszulösen. Falls die nachfolgend aufgeführten Indikatoren festgestellt werden, ist es ratsam, die Governancestrategie weiterzuentwickeln.

- **Kostenmanagement:** Das Ausmaß der Bereitstellung übersteigt 1.000 Ressourcen in der Cloud, oder die monatlichen Ausgaben überschreiten 10.000 USD pro Monat.
- **Identitätsbaseline:** Einbeziehung von Anwendungen mit Legacy- oder Drittanbieteranforderungen für die mehrstufige Authentifizierung.
- **Sicherheitsbaseline:** Die Aufnahme der geschützten Daten in definierte Cloudeinführungspläne.
- **Ressourcenkonsistenz:** Die Aufnahme der unternehmenskritischen Anwendungen in definierte Cloudeinführungspläne.

[!INCLUDE [policy-statements](../../../../includes/policy-statements.md)]

## <a name="next-steps"></a>Nächste Schritte

Diese Unternehmensrichtlinie bereitet das Cloudgovernanceteam auf die Implementierung des Governance-MVP als Grundlage für die Einführung vor. Der nächste Schritt ist das Implementieren dieses MVP.

> [!div class="nextstepaction"]
> [Beschreibung der bewährten Methoden](./prescriptive-guidance.md)
