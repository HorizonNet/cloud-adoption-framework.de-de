---
title: Zuordnen von Zuständigkeiten zu Teams
description: Es wird beschrieben, wie Sie Teams übergreifend Zuständigkeiten zuordnen, indem Sie eine so genannte RACI-Matrix entwickeln und damit bestimmen, welche Teams verantwortlich sind (responsible), rechenschaftspflichtig sind (accountable), konsultiert werden (consulted) und zu informieren sind (informed).
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: af2ecfdfb10aa56993d893ef9bcc7152f4f3d702
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2020
ms.locfileid: "80428293"
---
<!-- cSpell:ignore ccoe -->

# <a name="align-responsibilities-across-teams"></a>Zuordnen von Zuständigkeiten zu Teams

Erfahren Sie, wie Sie Zuständigkeiten zu Teams zuordnen, indem Sie eine so genannte *RACI*-Matrix entwickeln, mit der bestimmt wird, welche Teams verantwortlich sind (responsible), rechenschaftspflichtig sind (accountable), konsultiert werden (consulted) und zu informieren sind (informed). Dieser Artikel bietet eine RACI-Beispielmatrix für die unter [Einrichten von Teamstrukturen](./organization-structures.md) beschriebenen Organisationsstrukturen:

- [Nur Cloudeinführungsteam](#cloud-adoption-team-only)
- [MVP – Bewährte Methode](#best-practice-minimum-viable-product-mvp)
- [Zentrale IT-Abteilung](#central-it)
- [Strategische Ausrichtung](#strategic-alignment)
- [Operative Ausrichtung](#operational-alignment)
- [Cloudkompetenzzentrum (CCoE)](#cloud-center-of-excellence-ccoe)

Laden Sie die [RACI-Tabellenvorlage](https://archcenter.blob.core.windows.net/cdn/fusion/management/raci-template.xlsx) herunter, und ändern Sie sie, um Entscheidungen bezüglich der Organisationstruktur im Lauf der Zeit nachzuverfolgen.

In den Beispielen in diesem Artikel werden diese RACI-Konstrukte angegeben:

- Ein Team, das für eine Funktion *rechenschaftspflichtig* (accountable) ist, also die Kosten- oder Gesamtverantwortung trägt.
- Die Teams, die für die Ergebnisse *verantwortlich* (responsible) sind, also die Durchführungsverantwortung tragen.
- Die Teams, die bei der Planung *konsultiert* (consulted) werden sollten.
- Die Teams, die nach Abschluss der Tätigkeit *informiert* (informed) werden sollten.

Die letzte Zeile jeder Tabelle (mit Ausnahme der ersten) enthält einen Link zu weiteren Informationen zur am besten ausgerichteten Cloudfunktion.

## <a name="cloud-adoption-team-only"></a>Nur Cloudeinführungsteam

|  |Lösungsbereitstellung  |Geschäftliche Ausrichtung  |Change Management  |Lösungsvorgänge  |Governance |Plattformreife  |Plattformbetrieb  |Plattformautomatisierung  |
|---------|---------|---------|---------|---------|---------|---------|---------|---------|
|Cloudeinführungsteam |Verantwortlich|Verantwortlich|Verantwortlich|Verantwortlich|Verantwortlich|Verantwortlich|Verantwortlich|Verantwortlich|

## <a name="best-practice-minimum-viable-product-mvp"></a>Bewährte Methode: Minimum Viable Product (MVP)

|  |Lösungsbereitstellung  |Geschäftliche Ausrichtung  |Change Management  |Lösungsvorgänge  |Governance |Plattformreife  |Plattformbetrieb  |Plattformautomatisierung  |
|---------|---------|---------|---------|---------|---------|---------|---------|---------|
|Cloudeinführungsteam|Verantwortlich|Verantwortlich|Verantwortlich|Verantwortlich|Zu Rate gezogen|Zu Rate gezogen|Zu Rate gezogen|Informiert|
|Cloudgovernanceteam|Zu Rate gezogen|Informiert|Informiert|Informiert|Verantwortlich|Verantwortlich|Verantwortlich|Verantwortlich|
||||||||||
|Ausgerichtete Cloudfunktionen|[Cloudeinführung](./cloud-adoption.md)|[Cloudstrategie](./cloud-strategy.md)|[Cloudstrategie](./cloud-strategy.md)|[Cloudbetrieb](./cloud-operations.md)|[CCoE](./cloud-center-of-excellence.md)-[Cloudgovernance](./cloud-governance.md)|[CCoE](./cloud-center-of-excellence.md)-[Cloudplattform](./cloud-platform.md)|[CCoE](./cloud-center-of-excellence.md)-[Cloudplattform](./cloud-platform.md)|[CCoE](./cloud-center-of-excellence.md)-[Cloudautomatisierung](./cloud-automation.md)|

## <a name="central-it"></a>Zentrale IT-Abteilung

| |Lösungsbereitstellung  |Geschäftliche Ausrichtung  |Change Management  |Lösungsvorgänge  |Governance |Plattformreife  |Plattformbetrieb  |Plattformautomatisierung  |
|---------|---------|---------|---------|---------|---------|---------|---------|---------|
|Cloudeinführungsteam  |Verantwortlich|Verantwortlich|Zuständig    |Zuständig|Informiert   |Informiert   |Informiert   |Informiert   |
|Cloudgovernanceteam|Zu Rate gezogen  |Informiert   |Informiert   |Informiert   |Verantwortlich|Zu Rate gezogen  |Zuständig|Informiert   |
|Zentrale IT-Abteilung           |Zu Rate gezogen  |Informiert   |Verantwortlich   |Verantwortlich   |Zuständig  |Verantwortlich|Verantwortlich|Verantwortlich|
||||||||||
|Ausgerichtete Cloudfunktionen|[Cloudeinführung](./cloud-adoption.md)|[Cloudstrategie](./cloud-strategy.md)|[Cloudstrategie](./cloud-strategy.md)|[Cloudbetrieb](./cloud-operations.md)|[Cloud Governance](./cloud-governance.md)|[Zentrale IT-Abteilung](./central-it.md)|[Zentrale IT-Abteilung](./central-it.md)|[Zentrale IT-Abteilung](./central-it.md)|

## <a name="strategic-alignment"></a>Strategische Ausrichtung

|  |Lösungsbereitstellung  |Geschäftliche Ausrichtung  |Change Management  |Lösungsvorgänge  |Governance |Plattformreife  |Plattformbetrieb  |Plattformautomatisierung  |
|---------|---------|---------|---------|---------|---------|---------|---------|---------|
|Cloudstrategieteam  |Zu Rate gezogen  |Verantwortlich|Verantwortlich|Zu Rate gezogen  |Zu Rate gezogen  |Informiert   |Informiert   |Informiert   |
|Cloudeinführungsteam  |Verantwortlich|Zu Rate gezogen  |Zuständig|Verantwortlich|Informiert   |Informiert   |Informiert   |Informiert   |
|CCoE-Modell-RACI      |Zu Rate gezogen  |Informiert   |Informiert   |Informiert   |Verantwortlich|Verantwortlich|Verantwortlich|Verantwortlich|
||||||||||
|Ausgerichtete Cloudfunktionen|[Cloudeinführung](./cloud-adoption.md)|[Cloudstrategie](./cloud-strategy.md)|[Cloudstrategie](./cloud-strategy.md)|[Cloudbetrieb](./cloud-operations.md)|[CCoE](./cloud-center-of-excellence.md)-[Cloudgovernance](./cloud-governance.md)|[CCoE](./cloud-center-of-excellence.md)-[Cloudplattform](./cloud-platform.md)|[CCoE](./cloud-center-of-excellence.md)-[Cloudplattform](./cloud-platform.md)|[CCoE](./cloud-center-of-excellence.md)-[Cloudautomatisierung](./cloud-automation.md)|

## <a name="operational-alignment"></a>Operative Ausrichtung

|  |Lösungsbereitstellung  |Geschäftliche Ausrichtung  |Change Management  |Lösungsvorgänge  |Governance |Plattformreife  |Plattformbetrieb  |Plattformautomatisierung  |
|---------|---------|---------|---------|---------|---------|---------|---------|---------|
|Cloudstrategieteam  |Zu Rate gezogen  |Verantwortlich|Verantwortlich|Zu Rate gezogen  |Zu Rate gezogen  |Informiert   |Informiert   |Informiert   |
|Cloudeinführungsteam  |Verantwortlich|Zu Rate gezogen  |Zuständig|Zu Rate gezogen  |Informiert   |Informiert   |Informiert   |Informiert   |
|Cloudbetriebsteam|Zu Rate gezogen  |Zu Rate gezogen  |Zuständig|Verantwortlich|Zu Rate gezogen  |Informiert   |Verantwortlich|Zu Rate gezogen  |
|CCoE-Modell-RACI      |Zu Rate gezogen  |Informiert   |Informiert   |Informiert   |Verantwortlich|Verantwortlich|Zuständig|Verantwortlich|
||||||||||
|Ausgerichtete Cloudfunktionen|[Cloudeinführung](./cloud-adoption.md)|[Cloudstrategie](./cloud-strategy.md)|[Cloudstrategie](./cloud-strategy.md)|[Cloudbetrieb](./cloud-operations.md)|[CCoE](./cloud-center-of-excellence.md)-[Cloudgovernance](./cloud-governance.md)|[CCoE](./cloud-center-of-excellence.md)-[Cloudplattform](./cloud-platform.md)|[CCoE](./cloud-center-of-excellence.md)-[Cloudplattform](./cloud-platform.md)|[CCoE](./cloud-center-of-excellence.md)-[Cloudautomatisierung](./cloud-automation.md)|

## <a name="cloud-center-of-excellence-ccoe"></a>Cloudkompetenzzentrum (CCoE)

|  |Lösungsbereitstellung  |Geschäftliche Ausrichtung  |Change Management  |Lösungsvorgänge  |Governance |Plattformreife  |Plattformbetrieb  |Plattformautomatisierung  |
|---------|---------|---------|---------|---------|---------|---------|---------|---------|
|Cloudstrategieteam  |Zu Rate gezogen  |Verantwortlich|Verantwortlich|Zu Rate gezogen  |Zu Rate gezogen  |Informiert   |Informiert   |Informiert   |
|Cloudeinführungsteam  |Verantwortlich|Zu Rate gezogen  |Zuständig|Zu Rate gezogen  |Informiert   |Informiert   |Informiert   |Informiert   |
|Cloudbetriebsteam|Zu Rate gezogen  |Zu Rate gezogen  |Zuständig|Verantwortlich|Zu Rate gezogen  |Informiert   |Verantwortlich|Zu Rate gezogen  |
|Cloudgovernanceteam|Zu Rate gezogen  |Informiert   |Informiert   |Zu Rate gezogen  |Verantwortlich|Zu Rate gezogen  |Zuständig|Informiert   |
|Cloudplattformteam  |Zu Rate gezogen  |Informiert   |Informiert   |Zu Rate gezogen  |Zu Rate gezogen  |Verantwortlich|Zuständig|Zuständig|
|Cloudautomatisierungsteam|Zu Rate gezogen  |Informiert   |Informiert   |Informiert   |Zu Rate gezogen  |Zuständig|Zuständig|Verantwortlich|
||||||||||
|Ausgerichtete Cloudfunktionen|[Cloudeinführung](./cloud-adoption.md)|[Cloudstrategie](./cloud-strategy.md)|[Cloudstrategie](./cloud-strategy.md)|[Cloudbetrieb](./cloud-operations.md)|[CCoE](./cloud-center-of-excellence.md)-[Cloudgovernance](./cloud-governance.md)|[CCoE](./cloud-center-of-excellence.md)-[Cloudplattform](./cloud-platform.md)|[CCoE](./cloud-center-of-excellence.md)-[Cloudplattform](./cloud-platform.md)|[CCoE](./cloud-center-of-excellence.md)-[Cloudautomatisierung](./cloud-automation.md)|

## <a name="next-steps"></a>Nächste Schritte

Laden Sie die [RACI-Tabellenvorlage](https://archcenter.blob.core.windows.net/cdn/fusion/management/raci-template.xlsx) herunter, und ändern Sie sie, um Entscheidungen bezüglich der Organisationstruktur im Lauf der Zeit nachzuverfolgen. Kopieren und ändern Sie das am nächsten kommende Beispiel aus den RACI-Matrizen in diesem Artikel.

> [!div class="nextstepaction"]
> [Herunterladen der RACI-Tabellenvorlage](https://archcenter.blob.core.windows.net/cdn/fusion/management/raci-template.xlsx)
