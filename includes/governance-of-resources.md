<!-- TEMPLATE FILE - DO NOT ADD METADATA -->
<!-- markdownlint-disable MD002 MD041 -->
> [!NOTE]
> Im Falle von Änderungen an Ihren Geschäftsanforderungen ermöglichen Ihnen Azure-Verwaltungsgruppen eine einfache Reorganisation Ihrer Verwaltungshierarchie und Abonnementgruppenzuweisungen. Beachten Sie jedoch, dass Richtlinien- und Rollenzuweisungen, die auf eine Verwaltungsgruppe angewendet werden, an alle Abonnements unterhalb dieser Gruppe in der Hierarchie vererbt werden. Wenn Sie beabsichtigen, Abonnements zwischen Verwaltungsgruppen neu zuzuweisen, stellen Sie sicher, dass Ihnen alle Änderungen der Richtlinien und Rollenzuweisungen bekannt sind, die sich daraus ergeben können. Weitere Informationen finden Sie in der [Dokumentation zu Azure-Verwaltungsgruppen](/azure/governance/management-groups).

### <a name="governance-of-resources"></a>Governance von Ressourcen

Eine Reihe von globalen Richtlinien und RBAC-Rollen bilden eine Grundwertebene für die Durchsetzung der Governance. Um die Richtlinienanforderungen des Cloudgovernanceteams zu erfüllen, müssen zur Implementierung des Governance-MVP folgende Aufgaben ausgeführt werden:

1. Ermitteln Sie die erforderlichen Azure Policy-Definitionen zur Erzwingung von Geschäftsanforderungen. Hierzu können sowohl integrierte Definitionen verwendet als auch neue benutzerdefinierte Definitionen erstellt werden.
2. Erstellen Sie eine Blaupausendefinition unter Verwendung dieser integrierten und benutzerdefinierten Richtlinien sowie der für das Governance-MVP benötigten Rollenzuweisungen.
3. Wenden Sie Richtlinien und Konfigurationen global an, indem Sie die Blaupausendefinition zu allen Abonnements zuweisen.

#### <a name="identify-policy-definitions"></a>Ermitteln der Richtliniendefinitionen

Azure stellt mehrere integrierte Richtlinien und Rollendefinitionen zur Verfügung, die Sie jeder Verwaltungsgruppe, jedem Abonnement oder jeder Ressourcengruppe zuweisen können. Für viele allgemeine Governanceanforderungen können integrierte Definitionen verwendet werden. Wahrscheinlich müssen aber auch benutzerdefinierte Richtliniendefinitionen für die Behandlung Ihrer spezifischen Anforderungen erstellt werden.

Benutzerdefinierte Richtliniendefinitionen werden entweder in einer Verwaltungsgruppe oder in einem Abonnement gespeichert und über die Verwaltungsgruppenhierarchie vererbt. Wenn der Speicherort einer Richtliniendefinition eine Verwaltungsgruppe ist, kann diese Richtliniendefinition einer der untergeordneten Verwaltungsgruppen oder Abonnements dieser Gruppe zugewiesen werden.

Da die für das Governance-MVP erforderlichen Richtlinien für alle aktuellen Abonnements gelten sollen, werden die folgenden Geschäftsanforderungen mithilfe einer Kombination aus integrierten Definitionen und benutzerdefinierten, in der Stammverwaltungsgruppe erstellten Definitionen implementiert:

1. Schränken Sie die Liste der verfügbaren Rollenzuweisungen auf eine Reihe von integrierten Azure-Rollen ein, die von Ihrem Cloudgovernanceteam genehmigt wurden. Hierzu wird eine [benutzerdefinierte Richtliniendefinition](https://github.com/azure/azure-policy/tree/master/samples/Authorization/allowed-role-definitions) benötigt.
2. Legen Sie die folgenden Tags für alle Ressourcen als erforderlich fest: *Abrechnung/Kostenstelle*, _Geografie_, _Datenklassifizierung_, _Kritikalität_, _SLA_, _Umgebung_, _Anwendungsarchetyp_, _Anwendung_ und _Anwendungsbesitzer_. Hierfür können Sie die integrierte Definition `Require specified tag` verwenden.
3. Machen Sie es zur Bedingung, dass das Tag `Application` für Ressourcen mit dem Namen der betreffenden Ressourcengruppe übereinstimmt. Dies kann mithilfe der integrierten Definition „Tag und zugehörigen Wert erzwingen“ erreicht werden.

Informationen zur Definition benutzerdefinierter Richtlinien finden Sie in der [Dokumentation zu Azure Policy](/azure/governance/policy/tutorials/create-custom-policy-definition). Anleitungen und Beispiele für benutzerdefinierte Richtlinien finden Sie auf der [Website für Azure Policy-Beispiele](/azure/governance/policy/samples) und im zugehörigen [GitHub-Repository](https://github.com/azure/azure-policy).

#### <a name="assign-azure-policy-and-rbac-roles-using-azure-blueprints"></a>Zuweisen von Azure Policy- und RBAC-Rollen mithilfe von Azure Blueprints

Azure-Richtlinien können auf Ressourcengruppen-, Abonnement- und Verwaltungsgruppenebene zugewiesen und in [Azure Blueprints](/azure/governance/blueprints/overview)-Definitionen integriert werden. Obwohl die in diesem Governance-MVP definierten Richtlinienanforderungen für alle aktuellen Abonnements gelten, ist es sehr wahrscheinlich, dass zukünftige Bereitstellungen Ausnahmen oder alternative Richtlinien erfordern werden. Infolgedessen ist die Zuweisung von Richtlinien über Verwaltungsgruppen, wobei alle untergeordneten Abonnements diese Zuordnungen erben, möglicherweise nicht ausreichend flexibel, um diese Szenarien zu unterstützen.

Azure Blueprints ermöglicht die konsistente Zuweisung von Richtlinien und Rollen, die Anwendung von Resource Manager-Vorlagen und die Bereitstellung von Ressourcengruppen für mehrere Abonnements. Blaupausendefinitionen werden genau wie Richtliniendefinitionen in Verwaltungsgruppen oder Abonnements gespeichert. Die Richtliniendefinitionen sind durch Vererbung für alle untergeordneten Elemente in der Verwaltungsgruppenhierarchie verfügbar.

Das Cloudgovernanceteam hat entschieden, dass die Durchsetzung der erforderlichen Azure Policy- und RBAC-Zuweisungen über Abonnements hinweg durch Azure Blueprints und zugehörige Artefakte implementiert wird:

1. Erstellen Sie in der Stammverwaltungsgruppe eine Blaupausendefinition namens `governance-baseline`.
2. Fügen Sie die folgenden Blaupausenartefakte zur Blaupausendefinition hinzu:
    1. Richtlinienzuweisungen für die benutzerdefinierten Azure Policy-Definitionen, die im Stammverzeichnis der Verwaltungsgruppe definiert sind.
    2. Ressourcengruppendefinitionen für alle Gruppen, die in Abonnements erforderlich sind, die vom Governance-MVP erstellt oder verwaltet werden.
    3. Standardrollenzuweisungen, die in Abonnements erforderlich sind, die vom Governance-MVP erstellt oder verwaltet werden.
3. Veröffentlichen Sie die Blaupausendefinition.
4. Weisen Sie allen Abonnements die Blaupausendefinition `governance-baseline` zu.

Weitere Informationen zum Erstellen und Verwenden von Blaupausendefinitionen finden Sie in der [Dokumentation zu Azure Blueprints](/azure/governance/blueprints/overview).

### <a name="secure-hybrid-vnet"></a>Sicheres Hybrid-VNET

Bestimmte Abonnements erfordern häufig eine bestimmte Zugriffsebene für lokale Ressourcen. Dies ist in Migrationsszenarien oder Entwicklungsszenarien üblich, in denen sich abhängige Ressourcen im lokalen Rechenzentrum befinden.

Bis das Vertrauen in die Cloudumgebung vollständig hergestellt ist, ist es wichtig, jede zulässige Kommunikation zwischen der lokalen Umgebung und den Cloudworkloads streng zu kontrollieren und zu überwachen, und dass das lokale Netzwerk gegen potenziell unbefugten Zugriff von cloudbasierten Ressourcen geschützt ist. Um diese Szenarien zu unterstützen, fügt das Governance-MVP die folgenden bewährten Methoden hinzu:

1. Richten Sie ein cloudbasiertes, sicheres Hybrid-VNET ein.
    1. Die [VPN-Referenzarchitektur](/azure/architecture/reference-architectures/hybrid-networking/vpn) richtet ein Muster und ein Bereitstellungsmodell zur Erstellung einer VPN Gateway-Instanz in Azure ein.
    2. Vergewissern Sie sich, dass verbundene Cloudnetzwerke durch lokale Mechanismen für die Sicherheits- und Datenverkehrsverwaltung als nicht vertrauenswürdig eingestuft werden. In der Cloud gehostete Ressourcen und Dienste sollten nur Zugriff auf autorisierte lokale Dienste erhalten.
    3. Überprüfen Sie, ob das lokale Edgegerät im lokalen Rechenzentrum mit den [Azure VPN Gateway-Anforderungen](/azure/vpn-gateway/vpn-gateway-about-vpn-devices) kompatibel ist und für den Zugriff auf das öffentliche Internet konfiguriert ist.
    4. VPN-Tunnel dürfen nur für besonders einfache Workloads als produktionsbereite Verbindungen betrachtet werden. Für alle Fälle, in denen mehr als nur die lokale Konnektivität für wenige einfache Workloads erforderlich ist, sollte Azure ExpressRoute verwendet werden.
1. Erstellen Sie in der Stammverwaltungsgruppe eine zweite Blaupausendefinition namens `secure-hybrid-vnet`.
    1. Fügen Sie der Blaupausendefinition die Resource Manager-Vorlage für VPN Gateway als Artefakt hinzu.
    2. Fügen Sie der Blaupausendefinition die Resource Manager-Vorlage für das virtuelle Netzwerk als Artefakt hinzu.
    3. Veröffentlichen Sie die Blaupausendefinition.
1. Weisen Sie die Blaupausendefinition `secure-hybrid-vnet` allen Abonnements zu, die lokale Konnektivität benötigen. Diese Definition sollte zusätzlich zur Blaupausendefinition `governance-baseline` zugewiesen werden.

Eines der größten Probleme, die vom IT-Sicherheitsteam und von herkömmlichen Governanceteams angemerkt werden, ist das Risiko, dass vorhandene Ressourcen durch eine frühe Phase der Cloudeinführung kompromittiert werden. Der oben beschriebene Ansatz ermöglicht Cloudeinführungsteams das Erstellen und Migrieren von Hybridlösungen mit verringertem Risiko für lokale Ressourcen. Da das Vertrauen in die Cloudumgebung zunimmt, können spätere Entwicklungen diese temporäre Lösung möglicherweise entfernen.

> [!NOTE]
> Der obige Ansatz ist ein Ausgangspunkt für eine schnelle Erstellung eines Baselinegovernance-MVP. Dies ist erst der Anfang des Governancevorgangs. Eine Weiterentwicklung ist erforderlich, wenn das Unternehmen die Cloudeinführung fortsetzt und in folgenden Bereichen höhere Risiken eingeht:
>
> - Unternehmenskritische Workloads
> - Datenschutz
> - Kostenverwaltung
> - Szenarien mit mehreren Clouds
>
> Darüber hinaus basieren die besonderen Details dieses MVP auf dem Beispielvorgang eines fiktiven Unternehmens, der in den nachfolgenden Artikeln beschrieben wird. Vor der Implementierung dieser bewährten Methode wird dringend empfohlen, sich mit den anderen Artikeln dieser Serie vertraut zu machen.
