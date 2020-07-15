---
title: Leitfaden für Mitwirkende an Beiträgen
description: Leitfaden für Mitwirkende an Beiträgen.
author: alexbuckgit
ms.author: abuck
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: cc9676ec0e35cbb75b1884524d8c23b87c174460
ms.sourcegitcommit: 84d7bfd11329eb4c151c4c32be5bab6c91f376ed
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/10/2020
ms.locfileid: "86235108"
---
# <a name="contribution-guide"></a>Leitfaden für Mitwirkende an Beiträgen

## <a name="enterprise-scale-committee"></a>Komitee für Inhalte auf Unternehmensniveau

Das Komitee für Inhalte auf Unternehmensniveau und seine Mitglieder sind die Hauptverantwortlichen für das Unternehmensrepository, seine Sprache, seine Entwürfe und die Contoso-Implementierung.

Aktuelle Mitglieder des Komitees:

<!-- docsTest:disable -->
<!-- cSpell:disable -->

- Uday Pandya
- Callum Coffin
- Kristian Nese
- Victor Arzate
- Johan Dahlbom
- Lyon Till
- Niels Buit

<!-- docsTest:enable --->
<!-- cSpell:enable -->

## <a name="committee-member-responsibilities"></a>Zuständigkeiten der Komiteemitglieder

Die Mitglieder des Komitees sind für das Überprüfen und Bestätigen von RFCs (Request For Comment) verantwortlich, in denen neue Features oder Entwurfsänderungen vorgeschlagen werden.

Bei den anfänglichen Mitgliedern des Komitees handelt es sich um Mitarbeiter von Microsoft. Es wird jedoch davon ausgegangen, dass die Community weiter wächst und im Lauf der Zeit neue Communitymitglieder Teil des Komitees werden. Die Mitgliedschaft ist von der Art der Mitwirkung und den Fachkenntnissen einer Person abhängig. Personen, die wertvolle Beiträge zum Projekt leisten, erhalten eine entsprechende Anerkennung.

Mitglieder des Komitees können jederzeit engagierte Communitymitglieder für das Komitee nominieren. Diese Nominierungen sollten in Form von RFCs eingereicht werden, aus denen hervorgeht, weshalb die Person qualifiziert ist und welchen Beitrag sie leisten kann. Nachdem die Nominierung innerhalb des Komitees besprochen wurde, muss das neue Mitglied einstimmig in das Komitee gewählt werden.

## <a name="contribution-scope-for-enterprise-scale-architecture-guidelines"></a>Umfang der Mitwirkung an Leitfäden für unternehmensweite Architekturen

Wenn eine Plattform weiterentwickelt und neue Dienste und Funktionen in Produktionsumgebungen mit Kunden validiert werden, müssen die Entwurfsrichtlinien im Kontext der gesamten Architektur aktualisiert werden. Zum Aktualisieren der Dokumentation werden Platzhaltervorlagen verwendet, um Pull Requests (PRs) zu übermitteln.

## <a name="contribution-scope-for-contoso-reference-implementation"></a>Umfang der Mitwirkung an der Contoso-Referenzimplementierung

Wenn neue Dienste, Ressourcen, Ressourceneigenschaften und API-Versionen eingeführt werden, müssen das Implementierungshandbuch und die Referenzimplementierung entsprechend aktualisiert werden. Codebeiträge betreffen in erster Linie Microsoft Azure Policy-Definitionen und Zuweisungen für die Contoso-Implementierung.

<!-- cSpell:ignore azops apiversion northeurope -->

## <a name="how-to-submit-a-pr-to-the-upstream-repo"></a>Übermitteln von PRs in das Upstreamrepository

1. Führen Sie den folgenden Befehl aus, um basierend auf „upstream/master“ einen neuen Branch zu erstellen:

    ```shell
    git checkout -b feature upstream/master
    ```

2. Checken Sie die Dateien aus Ihrem Arbeitsbranch aus, die Sie in einen PR aufnehmen möchten:

    ```shell
    #substitute file name as appropriate. below example
    git checkout feature: .\.github\workflows\azops-push.yml
    ```

3. Übermitteln Sie Ihren Git-Branch per Push in Ihr Ursprungselement:

    ```shell
    git push origin -u
    ```

4. Erstellen Sie einen PR von „upstream“ an Ihren `master`-Remotebranch.

## <a name="writing-azure-resource-manager-templates-for-contoso-implementation"></a>Verfassen von Azure Resource Manager-Vorlagen für die Contoso-Implementierung

Beim Schreiben von Resource Manager-Vorlagen und Parameterdateien gibt es kein Richtig oder Falsch. Die Resource Manager-Sprache kann auf unterschiedliche Weise verwendet werden, und jeder Mitwirkende hat einen eigenen Schreibstil. Nur selten ähneln sich die Vorlagen- und Parameterdateien, die von verschiedenen Entwicklern geschrieben werden. Es gibt keine eindeutigen Stilvorgaben, mit denen Code von Konfigurationen getrennt und in denen festgelegt wird, welche Elemente in Vorlagen bzw. in Parameterdateien enthalten sein müssen. Auch bei der Frage, ob Parameter oder Objekte als Parameter (ohne Schema) verwendet werden sollen, gibt es keine eindeutige Vorgabe, die allen Szenarien gerecht würde.

Um die Entwicklung und Komponententests zu vereinfachen, wenn mehrere Entwickler zu einem Projekt beitragen, haben wir uns beim Schreiben von Vorlagen für einen bestimmten Stil entschieden. Dabei wird die Vorlage vollständig von der zugehörigen Parameterdatei getrennt. Bei diesem minimalistischen, auf einer einzigen Vorlage basierenden Ansatz werden alle Ressourceneigenschaften als komplexes Objekt in einer Parameterdatei externalisiert. Außerdem lässt sich eine strikte Schemaüberprüfung in der Datei erzwingen, die auf einem Ressourcenschema basiert, das von der Plattform bereits veröffentlicht wird. Bei dieser Vorgehensweise wird die Vorlage vollständig von den Parametern getrennt. Bei der Parameterdatei handelt es sich im Wesentlichen um eine RESTful-Darstellung der Ressource beim Aufruf von `Get-AzResource` oder `az resource show`.

- Template.json

```json
"resources": [{
        "condition": "[bool(equals(variables('resourceType'),'Microsoft.Authorization/policyDefinitions'))]",
        "type": "Microsoft.Authorization/policyDefinitions",
        "name": "[variables('policyDefinitions').name]",
        "apiVersion": "[variables('apiversion')[variables('resourceType')]]",
        "location": "northeurope",
        "properties": "[variables('policyDefinitions').Properties]"
    }],
```

Um sicherzustellen, dass Fehlerbehebungen in der aktuellen API-Version berücksichtigt werden, ist eine [allgemeine Vorlage mit mehreren Ressourcen](https://github.com/uday31in/AzOps/blob/main/template/template.json) verfügbar.

- Template.parameters.json

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "input": {
            "value": {
                <copy-paste-value-of-powershell/cli-output-here>
            }
        }
    }
}
```

Rufen Sie Ressourcendefinitionen ab, indem Sie die `Get-AzResource`-Funktion aufrufen und `resourceId` an die vorhandene Ressource übergeben.

```powershell
# Replace the resourceId in the command below before executing it

Get-AzResource -ResourceId '/providers/Microsoft.Management/managementGroups/contoso/providers/Microsoft.Authorization/policyDefinitions/DINE-Diagnostics-ActivityLog' | ConvertTo-Json -depth 100
```

<!-- docsTest:ignore "Policy definition" -->

Wenn Sie Entscheidungen für einen Entwurf treffen, sollten Sie die folgenden Vor- und Nachteile berücksichtigen:

- Vorteile:

  - Es müssen nicht länger Resource Manager-Vorlagen geschrieben werden, die letzte Resource Manager-Vorlage wurde erstellt.
  - Für Ressourcen werden unabhängig davon, wie sie erstellt und aktualisiert werden (Azure-Portal, Azure CLI, PowerShell oder Drittanbietertools), während ihres Lebenszyklus regelmäßige Exporte durchgeführt.
  - Abweichungen zwischen einer in Git gespeicherten Konfiguration und der aktuellen Konfiguration lassen sich leichter erkennen. Im Wesentlichen werden zwei JSON-Dokumente verglichen.
  - Es ist möglich, implizite Abhängigkeiten zwischen einfachen Ressourcen auf Client- und Serverseite zu verwalten. Azure weist nur wenige Ringabhängigkeiten zwischen Ressourcen auf, und implizite Abhängigkeiten lassen sich basierend auf bereits veröffentlichten Ressourcenschemas erkennen. Beispiel: Eine VM hängt von virtuellen Switches auf Kernelebene ab, die Switches hängen jedoch nicht von der VM ab (z. B. Richtliniendefinition -> Richtlinienzuweisung -> Rollenzuweisung -> Wartung oder virtuelles Netzwerk -> ExpressRoute oder Key Vault -> Azure SQL).

- Nachteile:

  Beim Erstellen des komplexen Objekts einer Parameterdatei können wichtige Einblicke verloren gehen. Dies lässt sich vermeiden, indem die Basisdefinition der aktuellen Ressource abgerufen oder die Ressource zunächst über das Portal erstellt wird. Vorlagenbereitstellungen können nicht mithilfe von „Azure-partner-customer-usage-attribution“ nachverfolgt werden. Diese Option ist im Rahmen des Unternehmensrepositorys nicht verfügbar.

Die aktuellen Resource Manager-Vorlagen, die für Ressourcenbereitstellungen verwendet werden, weisen das erwartete Verhalten auf, und es wird nicht davon ausgegangen, dass diese Vorlagen umgeschrieben werden. Die Bereitstellung erfolgt weiterhin über die Pipeline, und auch Konfigurationsabweichungen werden über die Pipeline ermittelt. Da die Plattform keinen Export von Bereitstellungsvorlagen zulässt, können die Vorlagen nicht zusammengeführt werden. Aufgrund dieser Parameter müssen alle in PRs übermittelten Vorlagen dem Prinzip entsprechen, dass die exportierten und die bereitgestellten Inhalte übereinstimmen.

Lesen Sie den nächsten Abschnitt, bevor Sie einen PR übermitteln. Übermitteln Sie keine PRs mit Vorlagen und Parameterdateien, um Ressourcen wie Azure Key Vault oder Azure Monitor-Protokolle bereitzustellen, ohne diese vorher in einer Richtlinie zu umschließen.

## <a name="contributing-to-policy-definitions-policy-assignments-and-role-definitions-and-assignments-for-contoso-implementation"></a>Mitwirkung an Richtliniendefinitionen, Richtlinienzuweisungen und Rollendefinition sowie Zuweisungen für die Contoso-Implementierung

Wenn Ihr Parameter den im obigen Abschnitt beschriebenen Standards entspricht und für Ihre Ressource verwendet werden kann, legen Sie fest, ob die Ressource für eine Verwaltungsgruppe oder ein Abonnement (Konnektivitäts- oder Verwaltungsabonnement) bereitgestellt werden soll. Wenngleich die Pipeline Vorlagen für jeden der vier Bereiche bereitstellen kann, erfolgt im Rahmen einer Zielzonenvorlage keine Bereitstellung auf Ressourcengruppenebene. Es muss mindestens eine Bereitstellungsvorlage auf Abonnementebene angegeben werden, die in einer Richtliniendefinition umschlossen ist.

- Führen Sie Folgendes aus:
  - Wenn Sie über Ressourcen verfügen, die in einer Zielzone bereitgestellt werden sollen, umschließen Sie sie in `DeployIfNotExists`-Richtlinien. Die entsprechende Zuweisung sollte auf Verwaltungsgruppenebene erfolgen.
  - Die Richtlinie sollte im Idealfall über einen Existenzbereich mit dem Abonnementbereich als Ziel verfügen, wenn die Bereitstellungszahl der Ressourcen innerhalb einer Zielzone genau Eins beträgt (z. B. ein virtuelles Netzwerk innerhalb einer Zielzone oder ein virtueller Hub für eine neue Azure-Region).
  - Idealerweise werden alle Richtliniendefinitionen im Stamm erstellt, der in der End-to-End-Vorlage definiert ist.

- Übermitteln Sie keine PRs mit einer Vorlage und einer Parameterdatei, um Ressourcen bereitzustellen (z. B. einen Schlüsseltresor) oder um eine eigene Verwaltungsgruppenhierarchie außerhalb der in einer End-to-End-Zielzone definierten Hierarchie zu erstellen.

Beispiel:

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "input": {
      "value": {
        "Name": "Tailspin",
        "DisplayName": "Tailspin",
        "ParentId": "/providers/Microsoft.Management/managementGroups/3fc1081d-6105-4e19-b60c-1ec1252cf560",
        "Children": [
          {
            "Id": "/providers/Microsoft.Management/managementGroups/Tailspin-bu1",
            "Name": "Tailspin-bu1",
            "DisplayName": "Tailspin-bu1",
            "properties": {
              "policyAssignments" :[
              ],
              "roleAssignments": [
              ]
            }
          }
        ],
        "properties": {
          "policyDefinitions": [
                <copy-paste of Json representation of the resource>
          ],
          "policyAssignments" :[
          ],
          "roleDefinitions": [
          ],
          "roleAssignments": [
          ]
        }
      }
    }
  }
}
```

## <a name="contributing-new-azure-policy-definitions-for-contoso-implementation"></a>Mitwirken an neuen Azure Policy-Definitionen für die Contoso-Implementierung

Verwenden Sie die folgenden Tools, und befolgen Sie die folgenden Empfehlungen, um an Richtliniendefinitionen mitzuwirken, die der unternehmensweiten Architektur entsprechen:

[Azure Policy-Erweiterung für Visual Studio](https://docs.microsoft.com/azure/governance/policy/how-to/extension-for-vscode)

Verwenden Sie diese Erweiterung, um nach Richtlinienaliasen zu suchen oder Ressourcen und Richtlinien zu überprüfen.

## <a name="explore-available-resource-properties-with-corresponding-policy-aliases"></a>Entdecken Sie verfügbare Ressourceneigenschaften mit entsprechenden Richtlinienaliasen

Für Azure PowerShell:

```powershell
# List all available providers
Get-AzPolicyAlias -ListAvailable

# Get aliases for a specific resource provider
(Get-AzPolicyAlias -NamespaceMatch 'Microsoft.Network').Aliases.Name
```

Für die Azure CLI:

```bash
# List all available providers

az provider list --query [*].namespace

# Get aliases for a specific resource provider

az provider show --namespace Microsoft.Network --expand "resourceTypes/aliases" --query "resourceTypes[].aliases[].name"
```

## <a name="contributing-new-azure-policy-assignments"></a>Mitwirken an neuen Azure Policy-Zuweisungen

Beim Zuweisen aller Richtlinien muss Folgendes berücksichtigt werden:

- Geben Sie eine präzise Absicht für die Zuweisung an. Gehört sie zu den beiden Abonnements (Konnektivität und Verwaltung) oder zu den Verwaltungsgruppen?
- Wie sind die Ressourcen innerhalb der Abonnements verteilt?
- Welche Regionen werden verwendet, und sind mehrere Regionen zulässig bzw. werden mehrere Regionen pro Abonnement verwendet?
- Welche Ressourcentypen sind zulässig, die sich gegebenenfalls darauf auswirken, wo die Richtlinie zugewiesen wird?
- Können mehrere Richtlinien, die für denselben oder einen ähnlichen Zweck definiert wurden, in einer Richtlinieninitiative zusammengefasst werden?
- Welcher Grund besteht für die aktuell gültige Richtlinie? Sollte eine Überwachungsrichtlinie in eine Erzwingungsrichtlinie geändert werden?
- Befolgen Sie bei `DeployIfNotExists`-Richtlinien das Prinzip der geringsten Rechte für die verwendete RBAC-Definition (rollenbasierte Zugriffssteuerung)?

<!-- cSpell:ignore don'ts -->

## <a name="code-of-conduct"></a>Verhaltensregeln

Wir arbeiten kontinuierlich daran, die Zusammenarbeit mit unserer engagierten Community zu stärken und auszubauen. Ihr Feedback ist uns sehr wichtig. Aktuell werden eine Reihe von Prinzipien und Leitlinien mit Empfehlungen zur Vorgehensweise ausgearbeitet.
