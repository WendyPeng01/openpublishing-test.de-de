---
uid: graph.windows.net/myorganization/Contacts/1.6
title: Azure AD Graph-API-Vorgänge für Kontakte
ms.TocTitle: Operations on contacts
ms.ContentId: 477161a7-aebf-4d4b-981d-fcbc148e25c1
ms.topic: reference (API)
ms.date: 01/26/2016
sections:
  - graph.windows.net/myorganization/Contacts/1.6/get contacts
  - graph.windows.net/myorganization/Contacts/1.6/get contact by id
  - graph.windows.net/myorganization/Contacts/1.6/update contact
  - graph.windows.net/myorganization/Contacts/1.6/delete contact
  - graph.windows.net/myorganization/Contacts/1.6/get contact manager link
  - graph.windows.net/myorganization/Contacts/1.6/update contact manager
  - graph.windows.net/myorganization/Contacts/1.6/get contact direct reports links
  - graph.windows.net/myorganization/Contacts/1.6/get contact memberOf links
---

# Vorgänge für Kontakte | Graph-API-Referenz


 _**Gilt für:** Graph-API | Azure Active Directory_


<a id="Overview"> </a>
In diesem Thema erläutert, wie Vorgänge in der Organisation Kontakte mithilfe der Graph-API von Azure Active Directory (AD). Organisatorische Kontakte darstellen, in der Regel Benutzer Ihres Unternehmens oder Ihrer Organisation außerhalb. Sie unterscheiden sich von persönlichen O365 Outlook-Kontakte. Mit der Azure AD Graph-API können Sie Organisationseinheiten Kontakte und deren Beziehungen zu anderen Verzeichnisobjekten, wie ihre Manager, Mitarbeiter und Gruppenmitgliedschaften lesen. Organisations-Kontakte zu schreiben ist auf die Kontakte, die derzeit nicht von einem lokalen Verzeichnis synchronisiert werden (die **DirSyncEnabled** Eigenschaft  **null** oder **false**). Für solche Kontakte können Sie aktualisiert oder löscht, der Kontakt selbst oder die Manager-Eigenschaft. Sie können keine Organisationseinheit Kontakte mit der Graph-API erstellen. Weitere Informationen zu Organisationseinheiten Kontakte, z. B., wie sie in Ihrem Mandanten erstellt werden finden Sie unter [Kontakt].

Der Graph-API ist eine REST-basierte API, die programmgesteuerten Zugriff auf Verzeichnisobjekte in Azure Active Directory, z. B. Benutzer, Gruppen, Organisationseinheiten Kontakte und Clientanwendungen bereitstellt.

> [!IMPORTANT] Azure AD Graph-API-Funktion ist auch verfügbar durch [Microsoft Graph](https://graph.microsoft.io/), eine einheitliche API, die auch von anderen Microsoft-APIs wie Outlook, OneDrive, OneNote, Planer und Office-Diagramm und alle der Zugriff erfolgt über einen einzelnen Endpunkt mit einem einzelnen Token services.

## REST-Vorgänge für Kontakte

Zum Ausführen von Vorgängen für organisatorische Kontakte mit der Graph-API senden Sie HTTP-Anforderungen mit einer unterstützten Methode (GET, POST, PATCH, PUT oder DELETE), um einen Endpunkt, die Ziel der Ressourcensammlung Kontakte, einen bestimmten Kontakt, eine Navigationseigenschaft eines Kontakts oder eine Funktion oder eine Aktion, die für einen Kontakt aufgerufen werden kann.

Graph-API-Anforderungen verwenden Sie die folgenden grundlegenden URL:
```no-highlight
https://graph.windows.net/{tenant_id}/{resource_path}?{api_version}[odata_query_parameters]
```

> [!IMPORTANT]
> Anforderungen an die Graph-API gesendet müssen wohlgeformt sein, eine gültige Endpunkt und die Version der Graph-API als Ziel und enthalten ein gültiges Zugangstoken erhalten von Azure AD in ihren `Authorization` Header. Weitere ausführliche Informationen zum Erstellen von Anforderungen und Empfangen von Antworten mit der Graph-API finden Sie unter [Übersicht].

Geben Sie die `{resource_path}` unterschiedlich, abhängig davon, ob Sie auf die Auflistung aller Kontakte in Ihrem Mandanten einen einzelnen Kontakt oder eine Navigationseigenschaft eines bestimmten Kontakts abzielen.

- `/contacts` ist der Kontakt Ressourcensammlung ausgerichtet. Der Pfad dieser Ressource können alle Kontakte oder eine gefilterte Liste der Kontakte in Ihrem Mandanten zu lesen.
- `/contacts/{object_id}` zielt auf einen einzelnen Kontakt in Ihrem Mandanten. Geben Sie den Ziel-Kontakt mit der Objekt-ID (GUID). Sie können diesen Ressourcenpfad verwenden, zum Abrufen der deklarierten Eigenschaften eines Kontakts. Für Kontakte, die nicht von einem lokalen Verzeichnis synchronisiert werden, können Sie diesen Ressourcenpfad deklarierten Eigenschaften eines Kontakts zu ändern oder Löschen eines Kontakts verwenden.
- `/contacts/{object_id}/{nav_property}` zielt auf die angegebene Navigationseigenschaft eines Kontakts. Sie können einem oder mehreren Objekten verwiesen wird, von der Ziel-Navigationseigenschaft des angegebenen Kontakts zurückgegeben. **Hinweis**: Diese Form der Adressierung ist nur für Lesevorgänge verfügbar.
- `/contacts/{object_id}/$links/{nav_property}` zielt auf die angegebene Navigationseigenschaft eines Kontakts. Sie können diese Form der Adressierung lesen und bearbeiten eine Navigationseigenschaft. Lesevorgängen werden Objekte durch die Eigenschaft als eine oder mehrere Links im Antworttext zurückgegeben. Nur die Manager-Navigationseigenschaft von Kontakten, die nicht von einem lokalen Verzeichnis synchronisiert werden, kann geändert werden. Der Manager wird als Link im Text Anforderung angegeben.

Die folgende Anforderung gibt z. B. einen Link zu den angegebenen Kontakt-Manager:

```no-highlight
GET https://graph.windows.net/myorganization/contacts/a2fb3752-08b4-413d-af6f-1d99c4c131d9/$links/manager?api-version=1.6
```

## Grundlegende Vorgänge für Kontakte <a id="BasicContactOperations"> </a>
Sie können auf der Kontakt Ressourcensammlung oder eines bestimmten Kontakts Kontakte Lesevorgänge ausführen. Sie können aktualisieren und Löschen von Kontakten, die nicht synchronisiert werden von einem lokalen Verzeichnis durch Verwendung eines bestimmten Kontakts. Der Graph-API unterstützt keine Kontakte. Außerdem unterstützt er auch aktualisieren oder Löschen von Kontakten, die synchronisiert werden von einem lokalen Verzeichnis (der **DirSyncEnabled** Eigenschaft **true**). Die folgenden Themen zeigen, wie grundlegende Vorgänge für Kontakte.

****

---
UID: graph.windows.net/myorganization/Contacts/1.6/get kontaktiert CodeGenerator: true
---

### Abrufen von Kontakten <a id="GetContacts"> </a>
Ruft eine Auflistung von Kontakten. Sie können OData-Abfrageparameter hinzufügen, auf die Anforderung, filtern, Sortieren und die Antwort Seite. Weitere Informationen finden Sie unter [Abfragen unterstützt, Filtern und Paging Optionen].

Bei Erfolg wird eine Auflistung von [Kontakt] Objekte; andernfalls enthält der Antworttext Fehlerdetails. Weitere Informationen zu Fehlern finden Sie unter [Fehlercodes und Fehlerbehandlung].

****

---
UID: graph.windows.net/myorganization/Contacts/1.6/get Kontakt Id CodeGenerator: true
---

###Kontakt <a id="GetAContact"> </a>

Ruft einen angegebenen Kontakt. Verwenden Sie die Objekt-ID (GUID), um den Ziel-Kontakt zu identifizieren.

Bei Erfolg wird der [wenden Sie sich an] Objekt für den angegebenen Kontakt andernfalls, enthält der Antworttext Fehlerdetails. Weitere Informationen zu Fehlern finden Sie unter [Fehlercodes und Fehlerbehandlung].

****
---
UID: graph.windows.net/myorganization/Contacts/1.6/update Kontakt
---

### Aktualisieren eines Kontakts <a id="UpdateContact"> </a>

Aktualisieren Sie die Eigenschaften eines Kontakts. Geben Sie alle beschreibbaren [Kontakt] Eigenschaft im Hauptteil Anforderung. Die Eigenschaften, die Sie angeben, werden geändert. Sie können nur Kontakte, die nicht von einem lokalen Verzeichnis synchronisiert werden aktualisieren (die **DirSyncEnabled** Eigenschaft ist **null** oder **false**).

Bei Erfolg wird kein Antworttext zurückgegeben. Andernfalls enthält der Antworttext Fehlerdetails. Weitere Informationen zu Fehlern finden Sie unter [Fehlercodes und Fehlerbehandlung].

****
---
UID: graph.windows.net/myorganization/Contacts/1.6/delete Kontakt
---
### Löschen eines Kontakts <a id="DeleteContact"> </a>

Löscht einen Kontakt an. Sie können nur Kontakte, die nicht synchronisiert werden von einem lokalen Verzeichnis löschen (die **DirSyncEnabled** Eigenschaft **null** oder  **false**).

Bei Erfolg wird kein Antworttext zurückgegeben. Andernfalls enthält der Antworttext Fehlerdetails. Weitere Informationen zu Fehlern finden Sie unter [Fehlercodes und Fehlerbehandlung].

****

## Vorgänge für Navigationseigenschaften des Kontakts <a id="ContactNavigationOps"> </a>

Beziehung zwischen einem Kontakt und anderen Objekten in das Verzeichnis, z. B. Manager, direkten Gruppenmitgliedschaften und direkt unterstellten Mitarbeiter des Kontakts werden mithilfe von Navigationseigenschaften verfügbar gemacht. Sie können lesen und ändern diese Beziehungen in einigen Fällen durch abzielen auf diese Navigationseigenschaften in Ihren Anforderungen.

---
UID: graph.windows.net/myorganization/Contacts/1.6/get Content Manager Link CodeGenerator: true
---

### Hier erhalten Sie einen Kontakt-manager <a id="GetContactsManager"> </a>

Ruft den Kontakt-Manager aus der **Manager** Navigationseigenschaft.

Bei Erfolg wird einen Link zu der [Benutzer] oder [wenden Sie sich an] wie der Kontakt-Manager zugewiesen ist; andernfalls enthält der Antworttext Fehlerdetails. Weitere Informationen zu Fehlern finden Sie unter [Fehlercodes und Fehlerbehandlung].

**Hinweis**: können, entfernen Sie das "$links"-Segment aus der URL zum Zurückgeben der [Benutzer] oder [Kontakt] Objekt anstelle einer Verknüpfung.

****

---
UID: graph.windows.net/myorganization/Contacts/1.6/update Kontakt-Manager
---
### Weisen Sie einen Kontakt-manager <a id="AssignContactsManager"> </a>

Weist einen Kontakt-Manager über die **Manager** Eigenschaft. Um einen Benutzer oder ein Kontakt kann zugewiesen werden. Der Anforderungstext enthält einen Link zu der [Benutzer] oder [Kontakt] zuweisen. Aktualisieren den Manager nur für Kontakte, die nicht von einem lokalen Verzeichnis synchronisiert werden (die **DirSyncEnabled** Eigenschaft **null** oder **false**).

Bei Erfolg wird kein Antworttext zurückgegeben. Andernfalls enthält der Antworttext Fehlerdetails. Weitere Informationen zu Fehlern finden Sie unter [Fehlercodes und Fehlerbehandlung].

****
---
UID: graph.windows.net/myorganization/Contacts/1.6/get Kontakt direkt unterstellten Mitarbeiter Links CodeGenerator: true
---
### Abrufen der direkt unterstellten Mitarbeiter des Kontakts <a id="GetContactsDirectReports"> </a>

Ruft den Kontakt direkt unterstellten Mitarbeiter aus der **DirectReports** Navigationseigenschaft.

Bei Erfolg wird eine Auflistung von Links zu den [Benutzer]und [wenden Sie sich an]des für den dieser Kontakt, andernfalls als Manager zugewiesen ist, der Antworttext enthält Fehlerdetails. Weitere Informationen zu Fehlern finden Sie unter [Fehlercodes und Fehlerbehandlung].

**Hinweis**: Sie können das "$links"-Segment entfernen, von der URL zurückgegeben  [DirectoryObject]s für die Benutzer und Kontakte anstelle von Links.

****
---
UID: graph.windows.net/myorganization/Contacts/1.6/get Kontakt MemberOf CodeGenerator verknüpft: true
---
### Abrufen der Gruppenmitgliedschaften eines Kontakts <a id="GetContactsMemberships"> </a>

Ruft den Kontakt Gruppenmitgliedschaften der **MemberOf** Navigationseigenschaft.

Diese Eigenschaft gibt nur die Gruppen, denen der Kontakt ein direktes Mitglied ist. Um alle Gruppen zu erhalten, die der Kontakt direkt oder transitiv Mitglied hat, rufen Sie die [GetMemberGroups]-Funktion.

Bei Erfolg wird eine Auflistung von Links zu den [Gruppe]s, denen dieser Kontakt Mitglied ist; andernfalls enthält des Antworttexts Fehlerdetails. Weitere Informationen zu Fehlern finden Sie unter [Fehlercodes und Fehlerbehandlung].

**Hinweis**: können, entfernen Sie das "$links"-Segment aus der URL zum Zurückgeben der [DirectoryObject]s für die Gruppen anstelle von Links.

****
## Funktionen und Aktionen für Kontakte <a id="ContactFunctions"> </a>
Sie können die folgenden Funktionen für einen Kontakt aufrufen.

### Überprüfen Sie die Mitgliedschaft in einer bestimmten Gruppe (transitiv)
Sie können die [IsMemberOf]-Funktion, die Mitgliedschaft in einer bestimmten Gruppe überprüfen aufrufen. Die Überprüfung ist transitiv.

### Überprüfen Sie die Mitgliedschaft in einer Liste von Gruppen (transitiv)
Sie können die [CheckMemberGroups]-Funktion, die Mitgliedschaft in einer Liste von Gruppen überprüfen aufrufen. Die Überprüfung ist transitiv.

### Abrufen Sie aller Gruppenmitgliedschaft (transitiv)
Sie können die [GetMemberGroups]-Funktion, um alle Gruppen zurück, denen der Kontakt Mitglied ist aufrufen. Die Überprüfung ist transitiv ist, im Gegensatz zum Lesen der [MemberOf](#GetContactsMemberships) Navigationseigenschaft, die nur die Gruppen zurück, der der Kontakt ein direktes Mitglied ist.

****

##Zusätzliche Ressourcen

- Erfahren Sie mehr über die Graph-API-Funktionen, Funktionen und Features der Vorschauversion in [Graph-API-Konzepte] unterstützt


[Anwendung]: ./entity-and-complex-type-reference.md#ApplicationEntity
[AppRoleAssignment]: ./entity-and-complex-type-reference.md#AppRoleAssignmentEntity
[Wenden Sie sich an]: ./entity-and-complex-type-reference.md#ContactEntity
[Vertrag]: ./entity-and-complex-type-reference.md#ContractEntity
[Gerät]: ./entity-and-complex-type-reference.md#DeviceEntity
[DirectoryLinkChange]: ./entity-and-complex-type-reference.md#DirectoryLinkChangeEntity
[DirectoryObject]: ./entity-and-complex-type-reference.md#DirectoryObjectEntity
[DirectoryRole]: ./entity-and-complex-type-reference.md#DirectoryRoleEntity
[DirectoryRoleTemplate]: ./entity-and-complex-type-reference.md#DirectoryRoleTemplateEntity
[Domäne (Vorschau)]: ./entity-and-complex-type-reference.md#DomainEntity
[DomainDnsRecord]: ./entity-and-complex-type-reference.md#DomainDnsRecordEntity
[DomainDnsCnameRecord]: ./entity-and-complex-type-reference.md#DomainDnsCnameRecordEntity
[DomainDnsMxRecord]: ./entity-and-complex-type-reference.md#DomainDnsMxRecordEntity
[DomainDnsSrvRecord]: ./entity-and-complex-type-reference.md#DomainDnsSrvRecordEntity
[DomainDnsTxtRecord]: ./entity-and-complex-type-reference.md#DomainDnsTxtRecordEntity
[DomainDnsUnavailableRecord]: ./entity-and-complex-type-reference.md#DomainDnsUnavailableRecordEntity
[ExtensionProperty]: ./entity-and-complex-type-reference.md#ExtensionPropertyEntity
[Gruppe]: ./entity-and-complex-type-reference.md#GroupEntity
[OAuth2PermissionGrant]: ./entity-and-complex-type-reference.md#OAuth2PermissionGrantEntity
[ServicePrincipal]: ./entity-and-complex-type-reference.md#ServicePrincipalEntity
[SubscribedSku]: ./entity-and-complex-type-reference.md#SubscribedSkuEntity
[TenantDetail]: ./entity-and-complex-type-reference.md#TenantDetailEntity
[Benutzer]: ./entity-and-complex-type-reference.md#UserEntity

[AlternativeSecurityId]: ./entity-and-complex-type-reference.md#AlternativeSecurityIdType
[AppRole]: ./entity-and-complex-type-reference.md#AppRoleType
[AssignedLicense]: ./entity-and-complex-type-reference.md#AssignedLicenseType
[AssignedPlan]: ./entity-and-complex-type-reference.md#AssignedPlanType
[KeyCredential]: ./entity-and-complex-type-reference.md#KeyCredentialType
[LicenseUnitsDetail]: ./entity-and-complex-type-reference.md#LicenseUnitsDetailType
[OAuth2Permission]: ./entity-and-complex-type-reference.md#OAuth2PermissionType
[PasswordCredential]: ./entity-and-complex-type-reference.md#PasswordCredentialType
[PasswordProfile]: ./entity-and-complex-type-reference.md#PasswordProfileType
[ProvisionedPlan]: ./entity-and-complex-type-reference.md#ProvisionedPlanType
[ProvisioningError]: ./entity-and-complex-type-reference.md#ProvisioningErrorType
[RequiredResourceAccess]: ./entity-and-complex-type-reference.md#RequiredResourceAccessType
[ResourceAccess]: ./entity-and-complex-type-reference.md#ResourceAccessType
[ServicePlanInfo]: ./entity-and-complex-type-reference.md#ServicePlanInfoType
[ServicePrincipalAuthenticationPolicy]: ./entity-and-complex-type-reference.md#ServicePrincipalAuthenticationPolicyType
[VerifiedDomain]: ./entity-and-complex-type-reference.md#VerifiedDomainType

[Graph-API-Schnellstart auf Azure auf Azure.com]: https://azure.microsoft.com/documentation/articles/active-directory-graph-api-quickstart/

<!--HONumber=May16_HO4-->


