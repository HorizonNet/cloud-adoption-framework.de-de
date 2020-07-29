---
title: Steuern der Ausführung von Azure in Ihrem Rechenzentrum
description: Erfahren Sie, wie Sie die Ausführung von Azure auf Azure Stack Hub in Ihrem Rechenzentrum steuern.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/19/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.openlocfilehash: c9f8a2f161571ced20f3a9317469cee14cc35fb1
ms.sourcegitcommit: 9163a60a28ffce78ceb5dc8dc4fa1b83d7f56e6d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/17/2020
ms.locfileid: "86452580"
---
# <a name="govern-azure-running-in-your-datacenter"></a>Steuern der Ausführung von Azure in Ihrem Rechenzentrum

Das öffentliche und private Cloudplattformen übergreifende Steuern von Hybridlösungen steigert die Komplexität. Der Umstand, dass Azure Stack Hub Ihre eigene, in Ihrem Rechenzentrum ausgeführte private Instanz von Azure ist, reduziert diese Komplexität.

Die Geschäftsprozesse, Disziplinen und viele der bewährten Methoden, die im Artikel [Governance für die Einführung der Microsoft Cloud für Azure (Microsoft Cloud Adoption Framework)](../../govern/index.md) erläutert werden, können weiterhin auf die hybride Governance mit Azure Stack Hub angewendet werden. Viele cloudnative Tools, die in der öffentlichen Cloudversion von Azure verwendet werden, können auch in Azure Stack Hub verwendet werden.

## <a name="azure-stack-hub-governance-considerations"></a>Überlegungen zur Azure Stack Hub-Governance

Die folgende Reihe von Blogs zeigt, wie die Konzepte für die Cloudgovernance für Azure Stack Hub implementiert werden können:

- [Organisationsdienste](https://azure.microsoft.com/blog/azure-stack-iaas-part-seven/) wie Ressourcengruppen, rollenbasierte Zugriffssteuerung (Role-Based Access Control, RBAC), Änderungsüberwachung, Sperren und Tags.
- [Sicherheitsdienste](https://azure.microsoft.com/blog/azure-stack-iaas-part-four/) einschließlich Standardfirewalls, Einschränkungen, VM-Updates und Patchverwaltung sowie Malwarestatus.
- [DevOps-Optionen](https://azure.microsoft.com/blog/azure-stack-iaas-part-seven-2/) einschließlich Infrastructure-as-Code (IaC), ein Portal mit PowerShell und Befehlszeilenschnittstelle (Command-Line Interface, CLI), Azure Application Insights und Integration in Azure DevOps und Jenkins.

## <a name="governance-toolchain-for-azure-stack-hub"></a>Governancetoolkette für Azure Stack Hub

Anleitungen zum Anwenden cloudnativer Governancetools auf Azure Stack Hub-Umgebungen finden Sie unter den folgenden Links:

- [Verwenden von Azure Resource Manager-Vorlagen in Azure Stack Hub](https://docs.microsoft.com/azure-stack/user/azure-stack-arm-templates?view=azs-2002)
- [PowerShell](https://docs.microsoft.com/azure-stack/user/azure-stack-powershell-overview?view=azs-2002)
- [Azure Policy](https://docs.microsoft.com/azure-stack/user/azure-stack-policy-module?view=azs-2002)
- [Rollenbasierte Zugriffssteuerung (Role-Based Access Control, RBAC)](https://docs.microsoft.com/azure-stack/user/azure-stack-manage-permissions?view=azs-2002)

## <a name="next-step-integrate-this-strategy-into-your-cloud-adoption-journey"></a>Nächster Schritt: Integrieren dieser Strategie in Ihre Cloudeinführungsjourney

In den folgenden Artikeln finden Sie Informationen zu bestimmten Aufgaben während der Cloudeinführungsjourney.

- [Verwalten von Azure Stack Hub](./manage.md)
