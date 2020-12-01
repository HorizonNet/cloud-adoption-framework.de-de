---
title: Steuern einer Azure-Instanz in Ihrem Rechenzentrum
description: Erfahren Sie, wie Sie eine Azure-Instanz steuern, die auf Azure Stack Hub in Ihrem Rechenzentrum ausgeführt wird.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/19/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.openlocfilehash: 117b21cde2fccbb1e823986d91528cca0dfa21f7
ms.sourcegitcommit: 57b757759b676a22f13311640b8856557df36581
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2020
ms.locfileid: "94994699"
---
# <a name="govern-an-azure-instance-in-your-datacenter"></a>Steuern einer Azure-Instanz in Ihrem Rechenzentrum

Das öffentliche und private Cloudplattformen übergreifende Steuern von Hybridlösungen steigert die Komplexität. Da es sich bei Ihrer Azure Stack Hub-Bereitstellung um Ihre eigene private Instanz von Azure handelt, die in Ihrem Rechenzentrum ausgeführt wird, wird diese Komplexität grundsätzlich reduziert.

Die Geschäftsprozesse, Disziplinen und viele der bewährten Methoden, die im Artikel [Governance für die Einführung der Microsoft Cloud für Azure (Microsoft Cloud Adoption Framework)](../../govern/index.md) erläutert werden, können weiterhin auf die hybride Governance mit Azure Stack Hub angewendet werden. Viele cloudnative Tools, die in der öffentlichen Cloudversion von Azure verwendet werden, können auch in Ihrer Azure Stack Hub-Bereitstellung verwendet werden.

## <a name="azure-stack-hub-governance-considerations"></a>Überlegungen zur Azure Stack Hub-Governance

Die folgende Reihe von Blogs zeigt, wie Ihre Organisation Cloudgovernancekonzepte für Azure Stack Hub implementieren kann:

- [Organisationsdienste](https://azure.microsoft.com/blog/azure-stack-iaas-part-seven/) wie Ressourcengruppen, rollenbasierte Zugriffssteuerung (Role-Based Access Control, RBAC), Änderungsüberwachung, Sperren und Tags.
- [Sicherheitsdienste](https://azure.microsoft.com/blog/azure-stack-iaas-part-four/) einschließlich Standardfirewalls, Einschränkungen, VM-Updates und Patchverwaltung sowie Malwarestatus.
- [DevOps-Optionen](https://azure.microsoft.com/blog/azure-stack-iaas-part-seven-2/) einschließlich Infrastructure-as-Code, ein Portal mit PowerShell und Befehlszeilenschnittstelle, Azure Application Insights und Integration in Azure DevOps und Jenkins.

## <a name="governance-toolchain-for-azure-stack-hub"></a>Governancetoolkette für Azure Stack Hub

Anleitungen zum Anwenden cloudnativer Governancetools auf Azure Stack Hub-Umgebungen finden Sie unter:

- [Verwenden von Azure Resource Manager-Vorlagen in Azure Stack Hub](/azure-stack/user/azure-stack-arm-templates?view=azs-2002)
- [PowerShell](/azure-stack/user/azure-stack-powershell-overview?view=azs-2002)
- [Azure Policy](/azure-stack/user/azure-stack-policy-module?view=azs-2002)
- [Rollenbasierte Zugriffssteuerung](/azure-stack/user/azure-stack-manage-permissions?view=azs-2002)

## <a name="next-steps"></a>Nächste Schritte

Anleitungen zu bestimmten Elementen der Cloudeinführungsjourney finden Sie in den folgenden Artikeln:

- [Verwalten von Azure Stack Hub](./manage.md)
