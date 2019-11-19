---
title: Skalieren mit mehreren Azure-Abonnements
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Erfahren Sie, wie Sie Ihre Umgebungen mit mehreren Azure-Abonnements skalieren.
author: alexbuckgit
ms.author: abuck
ms.date: 05/20/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 4910309817d348874ec7eed75640bd0407f1ffcf
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/04/2019
ms.locfileid: "73564010"
---
# <a name="scale-with-multiple-azure-subscriptions"></a>Skalieren mit mehreren Azure-Abonnements

Organisationen benötigen aufgrund von Ressourcenlimits und anderen Governanceüberlegungen häufig mehr als ein Azure-Abonnement. Eine Strategie zur Skalierung Ihrer Abonnements ist wichtig.

## <a name="production-and-nonproduction-workloads"></a>Produktions- und Nichtproduktionsworkloads

Wenn Sie Ihre erste Produktionsworkload in Azure bereitstellen, sollten Sie mit zwei Abonnements beginnen: einem Abonnement für Ihre Produktionsumgebung und einem Abonnement für Ihre Nichtproduktionsumgebung (für Entwicklung und Tests).

![Ein grundlegendes Abonnementmodell, das Schlüssel neben Feldern mit der Bezeichnung „Produktion“ und „Nichtproduktion“ anzeigt](../../_images/ready/basic-subscription-model.png)

Dieser Ansatz empfiehlt sich aus verschiedenen Gründen:

- Azure verfügt über spezifische Abonnementangebote für Dev/Test-Workloads. Diese Angebote bieten vergünstigte Preise für Azure-Dienste und -Lizenzen.
- Ihre Produktions-und Nichtproduktionsumgebungen verfügen wahrscheinlich über unterschiedliche Azure-Richtliniensätze. Mit separaten Abonnements lassen sich die verschiedenen Richtliniensätze ganz einfach auf Abonnementebene anwenden.
- Möglicherweise möchten Sie bestimmte Azure-Ressourcentypen zu Testzwecken in einem Dev/Test-Abonnement nutzen. Mit einem separaten Abonnement können Sie diese Ressourcentypen verwenden, ohne Sie in der Produktionsumgebung zur Verfügung zu stellen.
- Dev/Test-Abonnements können als isolierte Sandboxumgebungen verwendet werden. Mit solchen Sandboxes können Administratoren und Entwickler schnell vollständige Sätze von Azure-Ressourcen erstellen und bereinigen. Diese Isolation ist auch nützlich für den Schutz und die Sicherheit von Daten.
- Für Produktions- und Dev/Test-Abonnements gelten wahrscheinlich unterschiedlich akzeptable Kostenschwellenwerte.

## <a name="other-reasons-for-multiple-subscriptions"></a>Weitere Gründe für mehrere Abonnements

Auch in anderen Situationen können zusätzliche Abonnements erforderlich sein. Beachten Sie Folgendes, wenn Sie Ihre Cloudumgebung erweitern.

- Abonnements weisen unterschiedliche Grenzwerte für unterschiedliche Ressourcentypen auf. Beispielsweise ist die Anzahl von virtuellen Netzwerken in einem Abonnement begrenzt. Wenn ein Abonnement einen solchen Grenzwert erreicht, müssen Sie ein weiteres Abonnement erstellen und ihm neue Ressourcen zuordnen.

  Weitere Informationen finden Sie unter [Grenzwerte für Azure-Abonnements, -Dienste und -Kontingente sowie allgemeine Beschränkungen](https://docs.microsoft.com/azure/azure-subscription-service-limits).

- Jedes Abonnement kann eigene Richtlinien für bereitstellbare Ressourcentypen und unterstützte Regionen implementieren.

- Für Abonnements in Regionen mit öffentlicher Cloud und Sovereign Cloud- oder Government Cloud-Regionen gelten unterschiedliche Einschränkungen. Diese werden häufig von unterschiedlichen Datenklassifizierungsebenen zwischen Umgebungen gesteuert.

- Wenn Sie verschiedene Gruppen von Benutzern aus Sicherheits- oder Compliancegründen vollständig isolieren, sind möglicherweise separate Abonnements erforderlich. Nationale Behördenorganisationen müssen z. B. möglicherweise den Zugriff eines Abonnements auf Staatsangehörige beschränken.

- Verschiedene Abonnements können unterschiedliche Arten von Angeboten haben, die jeweils über eigene Nutzungsbedingungen und Vorteile verfügen.

- Möglicherweise bestehen Probleme hinsichtlich der Vertrauensstellung zwischen den Besitzern eines Abonnements und dem Besitzer der Ressourcen, die bereitgestellt werden sollen. Durch Verwendung eines anderen Abonnements mit anderem Besitzer können diese Probleme minimiert werden. Allerdings müssen Sie auch Netzwerk- und Datenschutzprobleme berücksichtigen, die in dieser Bereitstellung auftreten können.

- Aufgrund strenger finanzieller oder geopolitischer Kontrollen sind möglicherweise separate finanzielle Regelungen für bestimmte Abonnements erforderlich. Hierbei sind verschiedene Aspekte zu berücksichtigen: Datenhoheit, Unternehmen mit mehreren Tochtergesellschaften oder separater Buchhaltung und Abrechnung für Geschäftseinheiten in verschiedenen Ländern und mit verschiedenen Währungen.

- Azure-Ressourcen, die mit dem klassischen Bereitstellungsmodell erstellt wurden, sollten in Ihrem eigenen Abonnement isoliert werden. Die Sicherheit für klassische Ressourcen unterscheidet sich von der Sicherheit für Ressourcen, die über Resource Manager bereitgestellt werden. Azure-Richtlinien können auf klassische Ressourcen nicht angewendet werden.

- Dienstadministratoren, die klassische Ressourcen verwenden, verfügen über dieselben Berechtigungen wie die RBAC-Besitzer (Role-Based Access Control, rollenbasierte Zugriffssteuerung) eines Abonnements. Es ist schwierig, den Zugriff dieser Dienstadministratoren in einem Abonnement, das klassische Ressourcen und Resource Manager-Ressourcen kombiniert, ausreichend einzuschränken.

Es können auch andere geschäftliche oder technische Gründe in Ihrer Organisation dafür sprechen, zusätzliche Abonnements zu erstellen. Möglicherweise fallen zusätzliche Kosten für Dateneingang und -ausgang zwischen Abonnements an.

Viele Ressourcentypen können von einem Abonnement in ein anderes verschoben werden. Sie können auch automatisierte Bereitstellungen verwenden, um Ressourcen zu einem anderen Abonnement zu migrieren. Weitere Informationen finden Sie unter [Verschieben von Azure-Ressourcen in eine andere Ressourcengruppe oder ein anderes Abonnement](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-move-resources).

## <a name="manage-multiple-subscriptions"></a>Verwalten mehrerer Abonnements

Wenn Sie nur über wenige Abonnements verfügen, ist deren unabhängige Verwaltung relativ einfach. Sobald die Anzahl Ihrer Abonnements aber steigt, sollten Sie erwägen, eine Verwaltungsgruppenhierarchie zu erstellen, um die Verwaltung Ihrer Abonnements und Ressourcen zu vereinfachen.

Verwaltungsgruppen ermöglichen eine effiziente Verwaltung von Zugriff, Richtlinien und Compliance für die Abonnements einer Organisation. Jede Verwaltungsgruppe ist ein Container für ein oder mehrere Abonnements.

Verwaltungsgruppen werden in einer einzigen Hierarchie angeordnet. Sie definieren diese Hierarchie in Ihrem Azure AD-Mandanten, um sie an der Struktur und den Anforderungen Ihrer Organisation auszurichten. Die oberste Ebene wird als *Stammverwaltungsgruppe* bezeichnet. Sie können bis zu sechs Ebenen von Verwaltungsgruppen in der Hierarchie definieren. Jedes Abonnement gehört nur zu einer einzigen Verwaltungsgruppe.

Azure bietet vier Verwaltungsebenen: Verwaltungsgruppen, Abonnements, Ressourcengruppen und Ressourcen. Alle Zugriffsrichtlinien oder anderen Richtlinien, die auf einer bestimmten Hierarchieebene angewendet werden, werden von den darunter liegenden Ebenen geerbt. Ein Ressourcen- oder Abonnementbesitzer kann eine geerbte Richtlinie nicht ändern. Diese Einschränkung trägt zur Verbesserung der Governance bei.

> [!NOTE]
> Beachten Sie, dass eine Tagvererbung zurzeit nicht möglich ist, aber in Kürze verfügbar sein wird.

Mit diesem Vererbungsmodell können Sie die Abonnements in Ihrer Hierarchie so anordnen, dass jedes Abonnement die Richtlinien und Sicherheitsvorgaben erfüllt.

![Vier Bereichsebenen zum Organisieren Ihrer Azure-Ressourcen](../../ready/azure-setup-guide/media/organize-resources/scope-levels.png)

Jede Zugriffs- oder Richtlinienzuweisung in der Stammverwaltungsgruppe gilt für alle Ressourcen im Verzeichnis. Überlegen Sie sorgfältig, welche Elemente Sie in diesem Bereich definieren. Fügen Sie nur die Zuordnungen hinzu, über die Sie verfügen müssen.

Wenn Sie Ihre Verwaltungsgruppenhierarchie erstmals definieren, erstellen Sie zunächst die Stammverwaltungsgruppe. Anschließend verschieben Sie alle vorhandenen Abonnements im Verzeichnis in die Stammverwaltungsgruppe. Neue Abonnements werden immer in der Stammverwaltungsgruppe erstellt. Sie können Sie später in eine andere Verwaltungsgruppe verschieben.

Wenn Sie ein Abonnement in eine vorhandene Verwaltungsgruppe verschieben, erbt es die Richtlinien und Rollenzuweisungen aus der darüber liegenden Verwaltungsgruppenhierarchie. Sobald Sie mehrere Abonnements für Ihre Azure-Workloads eingerichtet haben, sollten Sie weitere Abonnements erstellen, um die Azure-Dienste aufzunehmen, die mit den anderen Abonnements gemeinsam genutzt werden.

![Beispiel für eine Verwaltungsgruppenhierarchie](../../_images/ready/management-group-hierarchy.png)

Weitere Informationen finden Sie unter [Organisieren von Ressourcen mit Azure-Verwaltungsgruppen](https://docs.microsoft.com/azure/governance/management-groups).

## <a name="tips-for-creating-new-subscriptions"></a>Tipps zum Erstellen neuer Abonnements

- Bestimmen Sie, wer für das Erstellen neuer Abonnements zuständig sein soll.
- Entscheiden Sie, welche Ressourcen standardmäßig in einem Abonnement enthalten sein sollen.
- Entscheiden Sie, wie alle Standardabonnements aussehen sollen. Zu den Überlegungen zählen RBAC-Zugriff, Richtlinien, Tags und Infrastrukturressourcen.
- Wenn möglich, [verwenden Sie einen Dienstprinzipal](https://docs.microsoft.com/azure/azure-resource-manager/grant-access-to-create-subscription) zum Erstellen neuer Abonnements. Definieren Sie eine Sicherheitsgruppe, die neue Abonnements über einen automatisierten Workflow anfordern kann.
- Wenn Sie ES-Kunde (Enterprise Agreement) sind, bitten Sie den Azure-Support, die Erstellung von Nicht-EA-Abonnements für Ihre Organisation zu sperren.

## <a name="related-resources"></a>Zugehörige Ressourcen

- [Grundlegende Konzepte in Azure](../considerations/fundamental-concepts.md).
- [Organisieren Ihrer Ressourcen mit Azure-Verwaltungsgruppen](https://docs.microsoft.com/azure/governance/management-groups)
- [Erhöhen der Zugriffsrechte zum Verwalten aller Azure-Abonnements und Verwaltungsgruppen](https://docs.microsoft.com/azure/role-based-access-control/elevate-access-global-admin).
- [Verschieben von Azure-Ressourcen in eine andere Ressourcengruppe oder ein anderes Abonnement](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-move-resources).

## <a name="next-steps"></a>Nächste Schritte

Sehen Sie sich die [empfohlenen Namens- und Kennzeichnungskonventionen](./naming-and-tagging.md) an, die Sie beim Bereitstellen Ihrer Azure-Ressourcen befolgen sollten.

> [!div class="nextstepaction"]
> [Empfohlene Namens- und Kennzeichnungskonventionen](./naming-and-tagging.md)
