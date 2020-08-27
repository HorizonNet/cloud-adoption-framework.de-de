---
title: Leitfaden zur Entscheidungsfindung für die Verschlüsselung
description: Implementieren Sie eine Verschlüsselungsrichtlinie (einen Kerndienst bei der Azure-Migration), die zusätzliche Sicherheitsebenen für Ihre cloudbasierten Workloads und Daten bereitstellt.
author: rotycenh
ms.author: abuck
ms.date: 02/11/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: a6e8a7c5b4929c590a4e33784b9ff1f297ec31d0
ms.sourcegitcommit: 07d56209d56ee199dd148dbac59671cbb57880c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88881851"
---
# <a name="encryption-decision-guide"></a>Leitfaden zur Entscheidungsfindung für die Verschlüsselung

Das Verschlüsseln von Daten schützt vor nicht autorisiertem Zugriff. Eine ordnungsgemäß implementierte Verschlüsselung bietet zusätzliche Ebenen der Sicherheit für Ihre cloudbasierten Workloads und dient als Schutz vor Angreifern und anderen nicht autorisierten Benutzern – innerhalb und außerhalb Ihrer Organisation und Ihrer Netzwerke.

Wechseln Sie zu: [Schlüsselverwaltung](#key-management) | [Datenverschlüsselung](#data-encryption) | [Weitere Informationen](#learn-more)

Bei einer cloudbasierten Verschlüsselungsstrategie stehen die Richtlinien- und Compliancevorgaben des Unternehmens im Mittelpunkt. Die Verschlüsselung von Ressourcen ist wünschenswert und in vielen Azure-Diensten (etwa in Azure Storage und in Azure SQL-Datenbank) standardmäßig aktiviert. Die Verschlüsselung stellt jedoch einen Zusatzaufwand dar, der zu einer höheren Wartezeit sowie zu einer allgemein höheren Ressourcennutzung führen kann.

Bei anspruchsvollen Workloads muss daher die richtige Balance zwischen Verschlüsselung und Leistung gefunden werden. Ein weiterer entscheidender Faktor ist die Art der Verschlüsselung von Daten und Datenverkehr. Verschlüsselungsmechanismen können sich in Sachen Kosten und Komplexität unterscheiden, und sowohl technische als auch richtlinienbedingte Anforderungen können Ihre Entscheidungen im Zusammenhang mit der Anwendung der Verschlüsselung sowie mit der Speicherung und Verwaltung kritischer Geheimnisse und Schlüssel beeinflussen.

Unternehmensrichtlinien und Konformität mit Drittanbietern sind die wichtigsten Aspekte bei der Planung einer Verschlüsselungsstrategie. Azure bietet mehrere Standardmechanismen zur Erfüllung allgemeiner Datenverschlüsselungsanforderungen für ruhende und übertragene Daten. Für Richtlinien und Complianceanforderungen, die eine strengere Kontrolle erfordern (etwa eine standardisierte Geheimnis- und Schlüsselverwaltung, eine Verschlüsselung während der Verwendung oder eine datenspezifische Verschlüsselung), ist dagegen eine komplexere Verschlüsselungsstrategie erforderlich.

## <a name="key-management"></a>Schlüsselverwaltung

Die Verschlüsselung von Daten in der Cloud hängt von der sicheren Speicherung, Verwaltung und betrieblichen Nutzung von Verschlüsselungsschlüsseln ab. Ein Schlüsselverwaltungssystem ist enorm wichtig, damit Ihre Organisation kryptografische Schlüssel, wichtige Kennwörter, Verbindungszeichenfolgen und andere vertrauliche IT-Informationen erstellen, speichern und verwalten kann.

Moderne Schlüsselverwaltungssysteme wie Azure Key Vault unterstützen die Speicherung und Verwaltung von softwaregeschützten Schlüsseln für die Entwicklung und den Testbetrieb sowie HSM-geschützte (Hardware Security Module) Schlüssel für den maximalen Schutz von Produktionsworkloads oder vertraulichen Daten.

Die folgende Tabelle zur Planung einer Cloudmigration hilft Ihnen bei der Entscheidung, wie Sie Verschlüsselungsschlüssel, Zertifikate und Geheimnisse, die zum Erstellen sicherer und verwaltbarer Cloudbereitstellungen kritisch sind, speichern und verwalten:

| Frage | Cloudnativ | Bring Your Own Key | Eigenen Schlüssel speichern |
|--- |--------------|--------|-------------|
| Fehlt in Ihrer Organisation eine zentralisierte Schlüssel- und Geheimnisverwaltung?                                                                    | Ja          | Nein     | Nein          |
| Muss die Erstellung von Schlüsseln und Geheimnissen für Geräte auf lokale Hardware beschränkt werden, wenn diese Schlüssel in der Cloud verwendet werden? | Nein           | Ja    | Nein          |
| Verfügt Ihre Organisation über Regeln oder Richtlinien, die eine externe Speicherung von Schlüsseln verhindern?                | Nein           | Nein     | Ja         |

### <a name="cloud-native"></a>Cloudnativ

Bei der cloudnativen Schlüsselverwaltung werden alle Schlüssel und Geheimnisse in einem cloudbasierten Tresor wie Azure Key Vault generiert, verwaltet und gespeichert. Dieser Ansatz vereinfacht viele IT-Aufgaben im Zusammenhang mit der Schlüsselverwaltung – etwa das Sichern, Speichern und Verlängern von Schlüsseln.

**Annahmen für cloudnative Systeme:** Die Verwendung eines cloudnativen Schlüsselverwaltungssystems umfasst die folgenden Annahmen:

- Sie vertrauen der Cloudlösung für die Schlüsselverwaltung beim Erstellen, Verwalten und Hosten der Geheimnisse und Schlüssel Ihres Unternehmens.
- Sie ermöglichen allen lokalen Anwendungen und Diensten, die auf den Zugriff auf Verschlüsselungsdienste oder Geheimnisse angewiesen sind, den Zugriff auf das Schlüsselverwaltungssystem in der Cloud.

### <a name="bring-your-own-key-byok"></a>Bring Your Own Key (BYOK)

Bei einem BYOK-Ansatz generieren Sie die Schlüssel auf dedizierter HSM-Hardware in Ihrer lokalen Umgebung und übertragen diese dann sicher an ein cloudbasiertes Verwaltungssystem wie Azure Key Vault zur Verwendung mit Ihren in der Cloud gehosteten Ressourcen.

**Voraussetzungen für Bring-Your-Own-Key:** Das lokale Generieren von Schlüsseln und deren Verwendung mit einem cloudbasierten Schlüsselverwaltungssystem umfasst die folgenden Annahmen:

- Sie vertrauen der zugrunde liegenden Sicherheits- und Zugriffssteuerungsinfrastruktur der Cloudplattform beim Hosting und der Verwendung Ihrer Schlüssel und Geheimnisse.
- Ihre in der Cloud gehosteten Anwendungen und Dienste können sicher und zuverlässig auf Schlüssel und Geheimnisse zugreifen und sie entsprechend verwenden.
- Sie sind durch gesetzliche Vorgaben oder Organisationsrichtlinien gezwungen, die Erstellung und Verwaltung der Geheimnisse und Schlüssel Ihrer Organisation lokal durchzuführen.

### <a name="on-premises-hold-your-own-key"></a>Lokal (Hold-Your-Own-Key)

In bestimmten Szenarien liegen möglicherweise gesetzliche Vorschriften, Richtlinien oder technische Gründe vor, die das Speichern von Schlüsseln in einem cloudbasierten Schlüsselverwaltungssystem verbieten. In diesem Fall müssen Sie die Schlüssel mithilfe lokaler Hardware generieren, mithilfe eines lokalen Schlüsselverwaltungssystems speichern und verwalten sowie ein Verfahren bereitstellen, mit dem cloudbasierte Ressourcen für die Verschlüsselung auf diese Schlüssel zugreifen können. Beachten Sie, dass das Speichern eines eigenen Schlüssels möglicherweise nicht mit allen Azure-basierten Diensten kompatibel ist.

**Annahmen für die lokale Schlüsselverwaltung:** Die Verwendung eines lokalen Schlüsselverwaltungssystems umfasst die folgenden Annahmen:

- Sie sind durch gesetzliche Vorgaben oder organisationsweite Richtlinien gezwungen, Erstellung, Verwaltung und Hosting der Geheimnisse und Schlüssel Ihrer Organisation lokal durchzuführen.
- Alle cloudbasierten Anwendungen und Dienste, die auf den Zugriff auf Verschlüsselungsdienste oder Geheimnisse angewiesen sind, können auf das lokale Schlüsselverwaltungssystem zugreifen.

## <a name="data-encryption"></a>Datenverschlüsselung

Berücksichtigen Sie bei der Planung Ihrer Verschlüsselungsrichtlinie die verschiedene Datenzustände mit unterschiedlichen Anforderungen an die Verschlüsselung:

| Datenzustand | Daten |
|-----|-----|
| Daten während der Übertragung | Interner Netzwerkdatenverkehr, Internetverbindungen, Verbindungen zwischen Rechenzentren oder virtuellen Netzwerken |
| Ruhende Daten    | Datenbanken, Dateien, virtuelle Laufwerke, PaaS-Speicher |
| Daten in Gebrauch     | Daten, die in den Arbeitsspeicher oder in CPU-Caches geladen wurden |

### <a name="data-in-transit"></a>Daten während der Übertragung

Dies sind Daten, die zwischen internen Ressourcen, zwischen Rechenzentren oder externen Netzwerken oder über das Internet verschoben werden.

Daten werden während der Übertragung normalerweise durch das Erzwingen der SSL/TLS-Protokolle für den Netzwerkdatenverkehr verschlüsselt. Verschlüsseln Sie immer den Datenverkehr zwischen Ihren in der Cloud gehosteten Ressourcen und externen Netzwerken oder dem öffentlichen Internet. In der Regel erzwingen PaaS-Ressourcen standardmäßig SSL-/TLS-Verschlüsselung. Die Cloudeinführungsteams und Workloadbesitzers sollten erwägen, die Verschlüsselung für Datenverkehr zwischen IaaS-Ressourcen zu erzwingen, die in Ihren virtuellen Netzwerken gehostet werden.

**Annahmen für die Verschlüsselung von Daten während der Übertragung:** Für die Implementierung einer geeigneten Verschlüsselungsrichtlinie für Daten während der Übertragung wird Folgendes angenommen:

- Alle öffentlich zugänglichen Endpunkte in Ihrer Cloudumgebung kommunizieren mit dem öffentlichen Internet über SSL/TLS-Protokolle.
- Wenn Cloudnetzwerke über das öffentliche Internet mit einem lokalen oder anderen externen Netzwerk verbunden werden, verwenden Sie verschlüsselte VPN-Protokolle.
- Werden Cloudnetzwerke über eine dedizierte WAN-Verbindung wie ExpressRoute mit lokalen oder anderen externen Netzwerken verbunden, verwenden Sie eine VPN- oder andere lokale Verschlüsselungsappliance, die mit einer entsprechenden virtuellen VPN- oder Verschlüsselungsappliance in Ihrem Cloudnetzwerk gekoppelt ist.
- Wenn Sie über vertrauliche Daten verfügen, die nicht in Datenverkehrsprotokolle oder andere Diagnoseberichte, die für IT-Mitarbeiter einsehbar sind, eingeschlossen werden sollten, verschlüsseln Sie sämtlichen Datenverkehr zwischen den Ressourcen in Ihrem virtuellen Netzwerk.

### <a name="data-at-rest"></a>Ruhende Daten

Ruhende Daten sind alle Daten, die nicht aktiv verschoben oder verarbeitet werden, einschließlich Dateien, Datenbanken, Laufwerken virtueller Computer, PaaS-Speicherkonten oder ähnlicher Ressourcen. Das Verschlüsseln gespeicherter Daten schützt virtuelle Geräte oder Dateien vor nicht autorisiertem Zugriff durch externes Eindringen in das Netzwerk, böswillige interne Benutzer oder versehentliche Veröffentlichung.

PaaS-Speicher und Datenbankressourcen erzwingen Verschlüsselung in der Regel standardmäßig. IaaS-Ressourcen können durch die Verschlüsselung von Daten auf der Ebene des virtuellen Datenträgers oder durch die Verschlüsselung des gesamten Speicherkontos für Ihre virtuellen Laufwerke geschützt werden. Alle diese Ressourcen können entweder von Microsoft oder vom Kunden verwaltete Schlüssel verwenden, die in Azure Key Vault gespeichert sind.

Die Verschlüsselung ruhender Daten umfasst auch erweiterte Methoden zur Datenbankverschlüsselung, z. B. auf Spalten- und Zeilenebene. Diese bieten deutlich mehr Kontrolle darüber, welche Daten genau geschützt werden.

Ihre allgemeinen Richtlinien und Complianceanforderungen, die Vertraulichkeit der gespeicherten Daten und die Leistungsanforderungen Ihrer Workloads legen fest, für welche Ressourcen eine Verschlüsselung erforderlich ist.

### <a name="assumptions-about-encrypting-data-at-rest"></a>Annahmen für die Verschlüsselung von ruhenden Daten

Für die Verschlüsselung von ruhenden Daten wird Folgendes angenommen:

- Sie speichern Daten, die nicht für die öffentliche Nutzung vorgesehen sind.
- Ihre Workloads vertragen die zusätzliche Latenz durch die Datenträgerverschlüsselung.

### <a name="data-in-use"></a>Daten in Gebrauch

Die Verschlüsselung von Daten in Gebrauch umfasst das Schützen von Daten in nicht beständigem Speicher, z.B. Arbeitsspeicher oder CPU-Caches. Dies setzt die Nutzung von Technologien wie der Verschlüsselung des gesamten Arbeitsspeichers und Enclave-Technologien, z.B. Secure Guard Extensions (SGX) von Intel, voraus. Außerdem umfasst dieser Bereich kryptografische Techniken, wie die homomorphe Verschlüsselung, die zum Erstellen von sicheren, vertrauenswürdigen Ausführungsumgebungen verwendet werden kann.

**Annahmen für die Verschlüsselung von Daten in Gebrauch:** Für die Verschlüsselung von Daten in Gebrauch wird Folgendes angenommen:

- Sie sollen den Besitz der Daten jederzeit von der zugrunde liegenden Cloudplattform trennen – selbst auf den Ebenen von Arbeitsspeicher und CPU.

## <a name="learn-more"></a>Weitere Informationen

Weitere Informationen zur Verschlüsselung und Schlüsselverwaltung in Azure finden Sie unter:

- **[Übersicht über die Azure-Verschlüsselung](/azure/security/fundamentals/encryption-overview):** Eine ausführliche Beschreibung zur Verwendung der Verschlüsselung in Azure zum Schutz sowohl ruhender Daten als auch von Daten bei der Übertragung.
- **[Azure Key Vault](/azure/key-vault/general/overview):** Key Vault ist das primäre Schlüsselverwaltungssystem zum Speichern und Verwalten von kryptografischen Schlüsseln, Geheimnissen und Zertifikaten in Azure.
- **[Bewährte Methoden für Datensicherheit und Datenverschlüsselung in Azure](/azure/security/fundamentals/data-encryption-best-practices):** Eine Diskussion über die bewährten Methoden von Azure zur Datensicherheit und Datenverschlüsselung.
- **[Azure Confidential Computing](https://azure.microsoft.com/solutions/confidential-compute):** Die Confidential Computing-Initiative von Azure stellt Tools und Technologien zum Erstellen von vertrauenswürdigen Ausführungsumgebungen und anderen Verschlüsselungsmechanismen zum Schützen von Daten in Gebrauch bereit.

## <a name="next-steps"></a>Nächste Schritte

„Verschlüsselung“ ist nur eine der Kernkomponenten der Infrastruktur, die architekturspezifische Entscheidungen während eines Cloudeinführungsprozesses erfordert. Navigieren Sie zur Übersicht über Leitfäden zur architekturbezogenen Entscheidungsfindung, um mehr über alternative Muster oder Modelle zu erfahren, die bei Entwurfsentscheidungen für andere Arten von Infrastrukturen verwendet werden.

> [!div class="nextstepaction"]
> [Übersicht über Leitfäden zur architekturbezogenen Entscheidungsfindung](../index.md)
