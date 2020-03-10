---
title: 'Governance für Standardunternehmen: Anfängliche Unternehmensrichtlinie'
description: Verwenden Sie das Framework für die Cloudeinführung (Cloud Adoption Framework) für Azure, um die anfängliche Governanceposition, Risiken in der Anfangsphase, anfängliche Richtlinienanweisungen und Prozesse zur frühzeitigen Erzwingung zu definieren.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 64f04fe32445f79f36fe3846f16e3296e9424130
ms.sourcegitcommit: 10637acba8c857a6f5aa8c4a80c0649903f60402
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/28/2020
ms.locfileid: "78170935"
---
# <a name="standard-enterprise-governance-guide-initial-corporate-policy-behind-the-governance-strategy"></a>Governanceleitfaden für Standardunternehmen: Anfängliche Unternehmensrichtlinie hinter der Governancestrategie

Die folgende Unternehmensrichtlinie definiert eine anfängliche Governanceposition, die der Ausgangspunkt für diesen Leitfaden ist. In diesem Artikel werden Risiken in einem frühen Stadium, anfängliche Richtlinienanweisungen und frühe Prozesse zum Durchsetzen von Richtlinienanweisungen definiert.

> [!NOTE]
>Die Unternehmensrichtlinie ist kein technisches Dokument, gibt aber den Anstoß zu vielen technischen Entscheidungen. Das in der [Übersicht](./index.md) beschriebene Governance-MVP ist letztlich von dieser Richtlinie abgeleitet. Vor der Implementierung eines Governance-MVP sollte Ihre Organisation eine Unternehmensrichtlinie entwickeln, die auf Ihren eigenen Zielen und geschäftlichen Risiken basiert.

## <a name="cloud-governance-team"></a>Cloudgovernanceteam

In dieser Schilderung besteht das Cloudgovernanceteam aus zwei Systemadministratoren, die die Notwendigkeit einer Governance erkannt haben. In den nächsten Monaten übernehmen sie den Auftrag, die Governance der Cloudpräsenz des Unternehmens zu bereinigen, also als _Cloudverwalter_ zu agieren. In zukünftigen Iterationen wird sich diese Position wahrscheinlich ändern.

[!INCLUDE [business-risk](../../../../includes/business-risks.md)]

## <a name="tolerance-indicators"></a>Toleranzindikatoren

Die aktuelle Risikotoleranz ist hoch, und das Interesse an der Investition in die Cloudgovernance ist niedrig. Daher fungieren die Toleranzindikatoren als Frühwarnsystem, um weitere Investitionen von Zeit und Energie auszulösen. Wenn die nachfolgend aufgeführten Indikatoren festgestellt werden, sollten Sie die Governancestrategie iterativ verbessern.

- **Kostenmanagement:** Der Umfang der Bereitstellung übersteigt die vorgegebenen Grenzwerte für Ressourcenanzahl oder monatliche Kosten.
- **Sicherheitsbaseline:** Die Aufnahme der geschützten Daten in definierte Cloudeinführungspläne.
- **Ressourcenkonsistenz:** Die Aufnahme der unternehmenskritischen Anwendungen in definierte Cloudeinführungspläne.

[!INCLUDE [policy-statements](../../../../includes/policy-statements.md)]

## <a name="next-steps"></a>Nächste Schritte

Diese Unternehmensrichtlinie bereitet das Cloudgovernanceteam auf die Implementierung des Governance-MVP vor, das die Grundlage für die Einführung bildet. Der nächste Schritt ist das Implementieren dieses MVP.

> [!div class="nextstepaction"]
> [Beschreibung der bewährten Methoden](./prescriptive-guidance.md)
