---
title: Was ist die Cloudressourcenkontrolle?
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Erläuterung zur Cloudressourcenkontrolle in Azure
author: alexbuckgit
ms.author: abuck
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.openlocfilehash: a72213a1ad72ce2df14add3e36b276b58b75485e
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70836888"
---
<!-- markdownlint-disable MD026 -->

# <a name="what-is-cloud-resource-governance"></a>Was ist die Cloudressourcenkontrolle?

Unter [Wie funktioniert Azure?](../../getting-started/what-is-azure.md) haben Sie gelernt, dass es sich bei Azure um eine Sammlung von Servern und Netzwerkhardwarekomponenten handelt, auf denen im Auftrag von Benutzern virtualisierte Hardware und Software ausgeführt wird. Dank Azure kann die Anwendungsentwicklungs- und IT-Abteilung Ihrer Organisation flexibel arbeiten, weil Ressourcen auf einfache Weise erstellt, gelesen, aktualisiert und gelöscht werden können.

Während der uneingeschränkte Zugriff auf Ressourcen Entwickler flexibler macht, kann er jedoch auch zu unerwarteten Kosten führen. Beispielsweise kann für ein Entwicklungsteam die Bereitstellung einer Reihe von Ressourcen zu Testzwecken genehmigt werden, wobei dann nach Abschluss des Testens aber vergessen wird, diese zu löschen. Für diese Ressourcen fallen weiterhin Kosten an, selbst wenn sie nicht mehr genehmigt oder erforderlich sind.

Die Lösung ist die Kontrolle (bzw. Governance) des Ressourcenzugriffs. **Governance** bezieht sich auf die fortlaufende Verwaltung, Überwachung und Überprüfung der Nutzung von Azure-Ressourcen, um die Ziele und Anforderungen Ihrer Organisation zu erfüllen.

<!-- markdownlint-disable MD034 -->

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE2ii94]

<!-- markdownlint-enable MD034 -->

Diese Anforderungen sind für jedes Unternehmen spezifisch, weshalb ein Allzweckansatz für Governance nicht hilfreich ist. Es liegt stattdessen im Ermessen jeder Organisation, wie sie ihr Governancemodell mithilfe der beiden primären Governancetools von Azure gestaltet: **rollenbasierte Zugriffssteuerung** (Role-Based Access Control, RBAC) und **Ressourcenrichtlinie**.

Die rollenbasierte Zugriffssteuerung definiert Rollen, und Rollen definieren die Vorgänge, die diejenigen Benutzer ausführen dürfen, die der jeweiligen Rolle zugewiesen sind. Die Rolle **Besitzer** beispielsweise lässt alle Vorgänge (Erstellen, Lesen, Aktualisieren und Löschen) für eine Ressource zu, während die Rolle **Leser** nur die Lesevorgänge zulässt. Rollen können umfassend definiert und auf viele Ressourcentypen angewendet werden. Sie können auch enger gefasst und auf nur einige wenige Ressourcentypen angewendet werden.

Über Ressourcenrichtlinien werden Regeln für die Ressourcenerstellung definiert. Per Ressourcenrichtlinie kann beispielsweise die SKU eines virtuellen Computers auf eine bestimmte vorab genehmigte Größe begrenzt werden. Eine weitere Ressourcenrichtlinie kann das Hinzufügen eines Tags für eine zugewiesene Kostenstelle erzwingen, wenn die Anforderung zum Erstellen der Ressource gesendet wird.

Bei der Konfiguration dieser Tools ist es wichtig, Governance und Agilität in der Organisation in Einklang zu bringen. Je restriktiver Ihre Governancerichtlinie ist, desto weniger agil sind Ihre Entwickler und IT-Fachkräfte. Eine restriktivere Governancerichtlinie erfordert ggf. mehr manuelle Schritte, z.B. das Erzwingen der Dateneingabe in ein Formular durch einen Entwickler oder das Senden einer E-Mail an ein Mitglied des Governanceteams mit der Bitte, eine Ressource manuell zu erstellen. Das Governanceteam verfügt nicht über unendliche Kapazitäten und kann zu einem Engpass werden. Dies führt dazu, dass Entwicklungsteams unproduktiv auf die Erstellung ihrer Ressourcen warten oder nicht benötigte Ressourcen Kosten verursachen, bevor sie gelöscht werden.

## <a name="next-steps"></a>Nächste Schritte

Nachdem Sie sich nun mit dem Konzept der Kontrolle von Cloudressourcen vertraut gemacht haben, können Sie sich über das Verwalten des Ressourcenzugriffs in Azure informieren.

> [!div class="nextstepaction"]
> [Informationen zum Ressourcenzugriff in Azure](./azure-resource-access.md)
