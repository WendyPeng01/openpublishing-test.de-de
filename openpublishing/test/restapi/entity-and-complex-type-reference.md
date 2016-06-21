---
title: Azure AD Graph-API-Entität und komplexer Typverweis
ms.TocTitle: Entity and complex type reference
ms.ContentId: 88f6e187-70db-4d90-b3b6-b8702bad1220
ms.topic: reference (API)
ms.date: 01/26/2016
---


# Entitäts- und komplexen Typverweis | Graph-API-Referenz 

    
 _**Gilt für:** Graph-API | Azure Active Directory_


<a id="Overview"> </a>
In diesem Thema wird erläutert, die Entitäten und komplexen Typen, die von der Graph-API verfügbar gemacht werden.

Der Graph-API ist ein OData 3.0 kompatibel REST-API, die programmgesteuerten Zugriff auf Verzeichnisobjekte in Azure Active Directory, z. B. Benutzer, Gruppen, Organisationseinheiten Kontakte und Clientanwendungen bereitstellt. 

> [!IMPORTANT] Azure AD Graph-API-Funktion ist auch verfügbar durch [Microsoft Graph](https://graph.microsoft.io/), eine einheitliche API, die auch von anderen Microsoft-APIs wie Outlook, OneDrive, OneNote, Planer und Office-Diagramm und alle der Zugriff erfolgt über einen einzelnen Endpunkt mit einem einzelnen Token services.

## Entitätsverweis

### Anwendungsserver-Entität <a id="ApplicationEntity"> </a>
Stellt eine Anwendung. Jede Anwendung, die Authentifizierung an Azure AD auslagert, muss in einem Verzeichnis registriert werden. Dies umfasst benötigt Azure AD zu Ihrer Anwendung, einschließlich der URL, in dem sie hat befindet, der URL zum Senden von Antworten nach der Authentifizierung den URI zur Identifizierung der Anwendung und mehr.  Weitere Informationen finden Sie unter [Grundlagen zur Registrierung einer Anwendung in Azure AD](https://azure.microsoft.com/en-us/documentation/articles/active-directory-authentication-scenarios/#basics-of-registering-an-application-in-azure-ad). Erbt von [DirectoryObject].

#### Eigenschaften
**Deklarierte Eigenschaften**

|  Name |  Typ |  Erstellen (POST) |  Lesen (GET) |  Update (PATCH) |  Beschreibung |
|:-------|:-------|:-------|:-------|:-------|:-------|
| AppID-Element | Edm.String in Version 1.5<br/><br/> Edm.Guid in früheren Versionen | Nein | Filterable | Nein | Der eindeutige Bezeichner für die Anwendung. |
| appRoles | Sammlung ([AppRole]) | Optional | Ja | Ja | Die Auflistung der Anwendungsrollen, die eine Anwendung deklarieren kann. Diese Rollen können Benutzer, Gruppen oder dienstprinzipalen zugewiesen werden.<br/><br/> **Notizen**: erfordert Version 1.5, lässt keine Nullwerte zu. |
| availableToOtherTenants | Edm.Boolean | Optional | Filterable | Ja | **true** ist die Anwendung mit anderen Mandanten gemeinsam verwendet, andernfalls **false**. |
| deletionTimestamp | Edm.DateTime | Nein | Ja | Nein | Der Zeitpunkt, an dem die Anwendung aus dem Mandanten gelöscht wurde. Wenn die Anwendung nicht gelöscht wurde, gibt **null**. Gelöschte Anwendung gelesen werden können, aus der `/deletedApplications` ressourcenauflistung. Geerbt von [DirectoryObject].<br/><br/> **Notizen**: erfordert Version 1.5 oder höher.  |
| displayName | Edm.String | Erforderlich | Ja | Ja | Der Anzeigename für die Anwendung. |
| errorUrl | Edm.String | Optional | Ja | Ja |  |
| groupMembershipClaims | Edm.String | Optional | Ja | Ja | Eine Bitmaske, die den Anspruch "Groups" ausgestellt in einem Benutzer- oder OAuth 2.0-Zugriffstoken, das die Anwendung erwartet konfiguriert. Bitmaskenwerte sind möglich: 0: keine, 1: Sicherheitsgruppen und Azure AD-Rollen, 2: reserviert und 4: reserviert. Festlegen der Bitmaske auf 7 erhalten alle Sicherheitsgruppen, Verteilergruppen und Azure AD-verzeichnisrollen, bei denen der angemeldete Benutzer ein Mitglied ist.<br/><br/> **Notizen**: erfordert Version 1.5. |
| Homepage | Edm.String | Optional | Ja | Ja | Die URL zur Startseite der Anwendung. |
| identifierUris | Collection(EDM.String) | Optional | Filterable | Ja | Die URIs, die Anwendung zu identifizieren. Weitere Informationen finden Sie unter [Anwendungsobjekte und Dienstprinzipalobjekte](https://azure.microsoft.com/en-us/documentation/articles/active-directory-application-objects/).<br/><br/> **Notizen**: lässt keine Nullwerte zu, die **alle** Operator für Filterausdrücke für mehrwertige Eigenschaften; Weitere Informationen erforderlich ist, finden Sie unter [Abfragen unterstützt, Filtern und Paging Optionen]. |
| keyCredentials | Sammlung ([KeyCredential]) | Optional | Ja | Ja | Die Auflistung der schlüsselanmeldeinformationen, die der Anwendung zugeordnet<br/><br/> **Notizen**: lässt keine Nullwerte zu |
| knownClientApplications | Collection(EDM.GUID) | Optional | Ja | Ja | Clientanwendungen, die an diese ressourcenanwendung gebunden sind. Zustimmung zu einer der bekannten Clientanwendungen führt zu impliziten Zustimmung zur ressourcenanwendung über ein kombiniertes Zustimmungsdialogfeld (mit dem OAuth-berechtigungsbereiche vom Client und der Ressource erforderlich).<br/><br/> **Notizen**: erfordert Version 1.5, lässt keine Nullwerte zu. |
| logoutUrl | Edm.String | Optional | Ja | Ja |  |
| mainLogo | Edm.Stream | Optional | Ja | Ja | Das Hauptlogo für die Anwendung.<br/><br/> **Notizen**: lässt keine Nullwerte zu |
| oauth2AllowImplicitFlow | Edm.Boolean | Optional | Ja | Ja | Gibt an, ob diese Anwendung OAuth2.0 impliziten Fluss Token anfordern kann. Der Standardwert ist **false**.<br/><br/> **Notizen**: erfordert Version 1.5, lässt keine Nullwerte zu. |
| oauth2AllowUrlPathMatching | Edm.Boolean | Optional | Ja | Ja | Gibt an, ob die im Rahmen von OAuth 2.0-tokenanforderungen, Azure AD pfadvergleich des umleitungs-URIS für der Anwendungsverzeichnis **ReplyUrls**. Der Standardwert ist **false**.<br/><br/> **Notizen**: erfordert Version 1.5, lässt keine Nullwerte zu. |
| oauth2Permissions | Sammlung ([OAuth2Permission]) | Optional | Ja | Ja | Die Auflistung der OAuth 2.0-berechtigungsbereiche, die die Web-API (Ressource)-Anwendung für Clientanwendungen bereitstellt. Diese berechtigungsbereiche können Clientanwendungen während der Zustimmung erteilt werden.<br/><br/> **Notizen**: erfordert Version 1.5, lässt keine Nullwerte zu. |
| oauth2RequiredPostResponse | Edm.Guid | Optional | Ja | Ja | Gibt an, ob der Rahmen von OAuth 2.0-tokenanforderungen Azure AD POST-Anforderungen, im Gegensatz zu GET-Anforderungen erlaubt. Der Standardwert ist false, was bedeutet, dass nur GET-Anforderungen zulässig sind.<br/><br/> **Notizen**: erfordert Version 1.5, lässt keine Nullwerte zu. |
| objectId | Edm.Guid | Nein | Ja | Nein | Der eindeutige Bezeichner für die Anwendung. Geerbt von [DirectoryObject].<br/><br/> **Notizen**: **Schlüssel**, unveränderlich, lässt keine Nullwerte zu, eindeutig. |
| Objekttyp | Edm.String | Nein | Ja | Nein | Eine Zeichenfolge, die den Objekttyp identifiziert. Für Clientanwendungen ist der Wert immer "Application". Geerbt von [DirectoryObject]. |
| passwordCredentials | Sammlung ([PasswordCredential]) | Optional | Ja | Ja | Die Auflistung der Kennwortanmeldeinformationen, die der Anwendung zugeordnet.<br/><br/> **Notizen**: lässt keine Nullwerte zu |
| publicClient | Edm.Boolean | Optional | Ja | Nein | Gibt an, ob diese Anwendung einem öffentlichen Client (z. B. eine installierte Anwendung, die auf einem mobilen Gerät ausgeführt wird). Der Standardwert ist **false**. |
| replyUrls | Collection(EDM.String) | Optional | Ja | Ja | Gibt die URLs, die Benutzertoken für die Anmeldung an gesendet werden, oder die Umleitung, URIs, OAuth 2.0-Autorisierungscodes und Zugriffstoken gesendet werden.<br/><br/> **Notizen**: lässt keine Nullwerte zu |
| requiredResourceAccess | Sammlung ([RequiredResourceAccess]) |  | Ja |  | Gibt Ressourcen an, denen diese Anwendung Zugriff benötigt, sowie die Sammlung der OAuth-berechtigungsbereiche und Anwendungsrollen, die unter jeder dieser Ressourcen benötigt. Diese Vorkonfiguration des erforderlichen Ressourcenzugriffs Laufwerke der Zustimmung.<br/><br/> **Notizen**: erfordert Version 1.5, lässt keine Nullwerte zu. |
| samlMetadataUrl | Edm.String | Optional | Ja | Ja | Die URL zu den SAML-Metadaten für die Anwendung. |

**Navigationseigenschaften**   

|  Name |  Von Multiplizität |  Nach |  Multiplizität |  Beschreibung |
|:-------|:-------|:-------|:-------|:-------|
| extensionProperties | \* | [ExtensionProperty] | \* | Der Anwendung zugeordneten Erweiterungseigenschaften. Erfordert die Version 1.5 oder höher. |
| Besitzer | \* | [DirectoryObject] | \* | Verzeichnisobjekte, die Besitzer der Anwendung sind. Die Besitzer sind eine Reihe von Benutzern ohne Administratorrechte, die berechtigt sind, dieses Objekt zu ändern. Erfordert Version 2013-11-08 oder höher. Geerbt von [DirectoryObject]. |
**Hinweis:** geerbte Navigationseigenschaften, die nicht aufgeführt sind, werden nicht unterstützt. Nicht unterstützte Navigationseigenschaften behandelt Anforderungen zurückgeben **400 Bad Request**. 

#### Unterstützte Vorgänge
Die folgenden Vorgänge werden für Applikationen unterstützt (HTTP-Methoden werden in Klammern aufgeführt):

- Erstellen (CREATE)
- Lesen (READ)
- Update (PATCH)
- Löschen (DELETE)

Die folgenden Vorgänge werden für Navigationseigenschaften der Anwendung unterstützt. Nicht alle Vorgänge möglicherweise für jede Navigationseigenschaft unterstützt.

- Lesen (READ)
- Aktualisieren (POST)
- Löschen (DELETE)

Für Clientanwendungen kann die folgende Aktion aufgerufen werden.

- [Wiederherstellung] zum Wiederherstellen einer gelöschten Anwendung. Erfordert Version 1.5 oder höher.

---

### AppRoleAssignment-Entität <a id="AppRoleAssignmentEntity"> </a>
Verwendet, um aufzuzeichnen, wenn ein Benutzer oder eine Gruppe einer Anwendung zugewiesen wird. In diesem Fall führt die rollenzuweisung zu einer anwendungskachel Zugriffsbereich für app des Benutzers angezeigt. Diese Entität kann auch verwendet werden, eine andere (als Dienstprinzipal modelliert) Anwendungszugriff auf eine Anwendung in einer bestimmten Rolle erteilen. Sie können zu erstellen, lesen, aktualisieren und Löschen von rollenzuweisungen. Erbt von [DirectoryObject].

**Wichtige**: in Version 1.5 eingeführt.
#### Eigenschaften
**Deklarierte Eigenschaften**

|  Name |  Typ |  Erstellen (POST) |  Lesen (GET) |  Update (PATCH) |  Beschreibung |
|:-------|:-------|:-------|:-------|:-------|:-------|
| creationTimestamp | Edm.DateTime | Nein | Ja | Nein | Die Zeit, wenn die Berechtigung erstellt wurde. |
| deletionTimestamp | Edm.DateTime | Nein | Ja | Nein | Diese Eigenschaft gilt nicht für die Zuweisung von app-Rolle und gibt immer **null**. Geerbt von [DirectoryObject].<br/><br/> **Notizen**: erfordert Version 1.5 oder höher.  |
| ID | Edm.Guid | Erforderlich | Ja | Ja | Die Rollen-Id, die der Prinzipal zugewiesen wurde. Diese Rolle muss deklariert werden, durch die ressourcenzielanwendung **ResourceId** in seine **AppRoles** Eigenschaft. Wenn die Ressource kein Berechtigungen deklariert wird, muss eine Standard-Id (0 (null) GUID) angegeben werden.<br/><br/> **Notizen**: lässt keine Nullwerte zu.  |
| principalDisplayName | Edm.String | Nein | Ja | Nein | Der Anzeigename des Prinzipals, der der Zugriff gewährt wurde. |
| objectId | Edm.String | Nein | Ja | Nein | Der eindeutige Bezeichner für die anwendungsrollenzuweisung. Geerbt von [DirectoryObject].<br/><br/> **Notizen**: **Schlüssel**, unveränderlich, lässt keine Nullwerte zu, eindeutig.  |
| Objekttyp | Edm.String | Nein | Ja | Nein | Eine Zeichenfolge, die den Objekttyp identifiziert. Für anwendungsrollenzuweisungen lautet der Wert immer "AppRoleAssignment". Geerbt von [DirectoryObject]. |
| principalId | Edm.Guid | Erforderlich | Ja | Ja | Der eindeutige Bezeichner (**ObjectId**) für den Prinzipal, der Zugriff gewährt wird.<br/><br/> **Notizen**: erforderlich.  |
| principalType | Edm.String | Nein | Ja | Nein | Der Typ des Prinzipals. Dies kann entweder "User", "Group" oder "ServicePrincipal" sein. |
| resourceDisplayName | Edm.String | Nein | Ja | Nein | Der Anzeigename der Ressource, auf die die Zuweisung vorgenommen wurde. |
| Ressourcen-ID | Edm.Guid | Erforderlich | Ja | Ja | Der eindeutige Bezeichner (**ObjectId**) für die Zielressource (Dienstprinzipal), für die die Zuweisung vorgenommen wurde. |
**Navigationseigenschaften**   
Keine

**Hinweis:** geerbte Navigationseigenschaften, die nicht aufgeführt sind, werden nicht unterstützt. Nicht unterstützte Navigationseigenschaften behandelt Anforderungen zurückgeben **400 Bad Request**. 

---

### Wenden Sie sich an der Entität <a id="ContactEntity"> </a>
Stellt einen Organisationseinheiten Kontakt dar. Erbt von [DirectoryObject].

Organisatorische Kontakte stellen Benutzer, die nicht in Ihrem Unternehmensverzeichnis dar. E-Mail-fähige Entitäten sind und in der Regel Personen Ihres Unternehmens oder Ihrer Organisation außerhalb darstellen. Organisations-Kontakte nicht mithilfe von Azure AD authentifiziert werden, noch können ihnen zugewiesen werden Lizenzen. 

Organisatorische Kontakte in Ihrem Mandanten über die Synchronisierung mit einem lokalen Verzeichnis mit Azure AD Connect erstellt werden können, oder über die Exchange Online Verwaltungsportale oder die Exchange Online-PowerShell-Cmdlets erstellt werden. Weitere Informationen zu Azure AD Connect finden Sie unter [Integrieren Ihrer lokalen Identitäten in Azure Active Directory](https://azure.microsoft.com/en-us/documentation/articles/active-directory-aadconnect/). Weitere Informationen zu Exchange Online Management-Tools finden Sie unter [Exchange Online-Einrichtung und Verwaltung](https://technet.microsoft.com/en-us/library/exchange-online-administration-and-management.aspx#BKMK_ExchangeAdministrationCenter). 

Sie können keine Organisationseinheit Kontakte mit der Graph-API erstellen. Sie können jedoch aktualisieren und Löschen von Kontakten, die derzeit nicht synchronisiert werden von einem lokalen Verzeichnis; d. h. für die Kontakte der **DirSyncEnabled** Eigenschaft **null** oder **false**. Sie können nicht aktualisiert oder Löschen von Kontakten für die die **DirSyncEnabled** Eigenschaft **true**.

**Hinweis**: organisatorische Kontakte werden Directory-Entitäten, die externe Benutzer darstellen. Sie sollten nicht mit Office 365 Outlook Persönliche Kontakte verwechselt werden. 
 
#### Eigenschaften
**Deklarierte Eigenschaften**

|  Name |  Typ |  Lesen (GET) |  Update (PATCH) |  Beschreibung |
|:-------|:-------|:-------|:-------|:-------|
| Ort | Edm.String | Filterable | Ja | Der Ort, in dem der Kontakt ansässig ist. |
| Land | Edm.String | Filterable | Ja | Das Land/Region, in dem der Kontakt ansässig ist. |
| deletionTimestamp | Edm.DateTime | Ja | Nein | Diese Eigenschaft ist nicht gültig für Kontakte und gibt immer **null**. Geerbt von [DirectoryObject].<br/><br/> **Notizen**: erfordert Version 1.5 oder höher.  |
| department | Edm.String | Filterable | Ja | Der Name der Abteilung, in der der Kontakt arbeitet. |
| dirSyncEnabled | Edm.Boolean | Filterable | Nein | **True,** wenn dieses Objekt, von einem lokalen Verzeichnis synchronisiert wird; **false** Wenn dieses Objekt ursprünglich von einem lokalen Verzeichnis synchronisiert wurde, aber nicht mehr synchronisiert ist; **NULL** wenn dieses Objekt noch nie von einem lokalen Verzeichnis (Standard) synchronisiert wurde. |
| displayName | Edm.String | Filterable | Ja | Der Anzeigename des Kontakts. |
| facsimileTelephoneNumber | Edm.String | Ja | Ja | Die Telefonnummer des Kontakts Business Faxgerät. |
| "givenName" | Edm.String | Filterable | Ja | Der Vorname (Rufname) des Kontakts. |
| Benutzereigenschaft | Edm.String | Filterable | Ja | Position des Kontakts. |
| lastDirSyncTime | Edm.DateTime | Filterable | Nein | Gibt den letzten, an dem das Objekt mit dem lokalen Verzeichnis synchronisiert wurde. |
| mail | Edm.String | Filterable | Nein | Die SMTP-Adresse für den Kontakt, z. B. "jeff@contoso.onmicrosoft.com". |
| mailNickname | Edm.String | Filterable | Ja | Der e-Mail-Alias des Kontakts. |
| mobile | Edm.String | Ja | Ja | Die primäre Mobilfunknummer des Kontakts. |
| objectId | Edm.String | Ja | Nein | Der eindeutige Bezeichner für den Kontakt. Geerbt von [DirectoryObject].<br/><br/> **Notizen**: **Schlüssel**, unveränderlich, lässt keine Nullwerte zu, eindeutig.  |
| Objekttyp | Edm.String | Ja | Nein | Eine Zeichenfolge, die den Objekttyp identifiziert. Bei Kontakten, die der Wert immer lautet "Contact". Geerbt von [DirectoryObject]. |
| physicalDeliveryOfficeName | Edm.String | Ja | Ja | Der Bürostandort des Kontakts an Business. |
| postalCode | Edm.String | Ja | Ja | Die Postleitzahl Postadresse des Kontakts. Die Postleitzahl ist für das Land bzw. die Region des Kontakts. In den Vereinigten Staaten von Amerika enthält dieses Attribut die Postleitzahl. |
| provisioningErrors | Sammlung ([ProvisioningError]) | Ja | Nein | Eine Auflistung von Fehlerdetails, die dieser Kontakt erfolgreich bereitgestellt wird verhindert.<br/><br/> **Hinweis:** lässt keine Nullwerte zu  |
| "proxyAddresses" | Collection(EDM.String) | Filterable | Nein | **Hinweis:** eindeutig, lässt keine Nullwerte zu, die **alle** Operator für Filterausdrücke für mehrwertige Eigenschaften; Weitere Informationen erforderlich ist, finden Sie unter [Abfragen unterstützt, Filtern und Paging Optionen].  |
| sipProxyAddress | Edm.String | Ja | Nein | Gibt die VoIP IP (VOIP) Session Initiation Protocol (SIP) Adresse für den Kontakt.<br/><br/> **Notizen**: erfordert Version 1.5 oder höher.  |
| Status | Edm.String | Filterable | Ja | Das Bundesland oder Kanton in der Adresse des Kontakts. |
| streetAddress | Edm.String | Ja | Ja | Die Straße Arbeitsort des Kontakts. |
| Nachname | Edm.String | Filterable | Ja | Der Kontakt-Nachname (Familienname oder Nachname). |
| telephoneNumber | Edm.String | Ja | Ja | Die primäre Telefonnummer Arbeitsort des Kontakts. |
| thumbnailPhoto | Edm.Stream | Ja | Ja | Ein miniaturfoto des Kontakts angezeigt werden.<br/><br/> **Hinweis:** lässt keine Nullwerte zu  |

**Navigationseigenschaften**  
 
|  Name |  Von Multiplizität |  Nach |  Multiplizität |  Beschreibung |
|:-------|:-------|:-------|:-------|:-------|
| manager | \* | [DirectoryObject]<br/><br/> (Nur [Benutzer] und [Kontakt] Objekte werden unterstützt.) | 0..1 | Der Benutzer oder Kontakt, der Vorgesetzte dieses Kontakts ist. Geerbt von [DirectoryObject].<br/><br/> HTTP-Methoden: GET, PUT, DELETE |
| directReports | \* | [DirectoryObject]<br/><br/> (Nur [Benutzer] und [Kontakt] Objekte werden unterstützt.) | \* | Direkt unterstellten Mitarbeiter des Kontakts. (Die Benutzer und Kontakte, die deren Manager-Eigenschaft, die auf diesen Kontakt festgelegt ist.) Geerbt von [DirectoryObject].<br/><br/> HTTP-Methoden: GET |
| memberOf | \* | [DirectoryObject]<br/><br/> (Nur [Gruppe] Objekte werden unterstützt.) | \* | Gruppen, denen dieser Kontakt Mitglied ist. Geerbt von [DirectoryObject].<br/><br/> HTTP-Methoden: GET |

**Hinweis:** geerbte Navigationseigenschaften, die nicht aufgeführt sind, werden nicht unterstützt. Nicht unterstützte Navigationseigenschaften behandelt Anforderungen zurückgeben **400 Bad Request**. 

#### Unterstützte Vorgänge
Die folgenden Vorgänge werden für Kontakte unterstützt (die jeweils verwendete HTTP-Methode steht in Klammern): 

- Lesen (GET)
- Update (PATCH): nur Kontakte, die nicht von einem lokalen Verzeichnis synchronisiert werden (**DirSyncEnabled** ist **null** oder **false**).
- Löschen (DELETE)

Die folgenden Vorgänge werden für kontaktnavigationseigenschaften unterstützt. nicht alle Vorgänge möglicherweise für jede Navigationseigenschaft unterstützt.

- Lesen (GET)
- Aktualisieren (PUT): **Manager** Eigenschaft, nur Kontakte, die nicht von einem lokalen Verzeichnis synchronisiert werden (**DirSyncEnabled** ist **null** oder **false**).
- Löschen (DELETE): **Manager** Eigenschaft, nur Kontakte, die nicht von einem lokalen Verzeichnis synchronisiert werden (**DirSyncEnabled** ist **null** oder  **false**).

Für Kontakte können die folgenden Aktionen und Funktionen aufgerufen werden:

- [CheckMemberGroups], um die Mitgliedschaft eines Kontakts in einer Liste von Gruppen zu überprüfen. Die Überprüfung ist transitiv.
- [GetMemberGroups], um eine Liste der Gruppen zurückzugeben, die ein Kontakt Mitglied ist. Die Überprüfung ist transitiv.
- [IsMemberOf] zu überprüfen, ob ein Kontakt Mitglied einer angegebenen Gruppe ist. Die Überprüfung ist transitiv.

#### Hinweise
Kontakte sind e-Mail-fähige Entitäten und können nicht mithilfe der Graph-API erstellt werden. Sie können aktualisiert werden. Update wird jedoch nur unterstützt, für die Kontakte mit den **DirSyncEnabled** Eigenschaftensatz **null** oder **false**. Kontakte können gelöscht werden.

---

### Vertrags-Entität <a id="ContractEntity"> </a>
In nur Partnermandanten vorhanden ist. Partnermandanten werden Azure AD-Mandanten, die zu Microsoft Partners gehören, die Teil einer Veröffentlichung von Office 365, Microsoft-Cloud-Lösungsanbieter oder Microsoft Advisor Partnerprogramme sind. Stellt eine bestehende Partnerschaft, die Partner mit einer Customer-Mandanten besitzt. Schreibgeschützt. Erbt von [DirectoryObject].

**Wichtige**: in Version 1.5 eingeführt.
#### Eigenschaften
**Deklarierte Eigenschaften**

| Name | Typ | Read(Get) | Beschreibung |
|:----|:----|:----|:----|
| customerContextId | Edm.Guid | Filterable | Der eindeutige Bezeichner für den kundenmandanten auf diese Partnerschaft verweist. Entspricht der **ObjectId** Eigenschaft der Customer-Mandanten [TenantDetail] Objekt. |
| "DefaultDomainName" | Edm.String | Filterable | Eine Kopie der Kunde Mandant-Standarddomänenname. Wenn die Partnerschaft mit dem Kunden eingerichtet ist, wird die Kopie erstellt. Es wird nicht automatisch aktualisiert, wenn der Kunde Mandant-Standarddomänenname ändert. |
| deletionTimestamp | Edm.DateTime | Ja | Diese Eigenschaft gilt nicht für Verträge und gibt immer **null**. Geerbt von [DirectoryObject].<br/><br/> **Notizen**: erfordert Version 1.5 oder höher.  |
| displayName | Edm.String | Filterable | Eine Kopie des Anzeigenamens für den des kundenmandanten. Wenn die Partnerschaft mit dem Kunden eingerichtet ist, wird die Kopie erstellt. Es wird nicht automatisch aktualisiert, wenn der Kunde Mandant Anzeigename geändert wird. |
| Objekttyp | Edm.String | Ja | Eine Zeichenfolge, die den Objekttyp identifiziert. Der Wert ist immer "Vertrag". Geerbt von [DirectoryObject]. |
| objectId | Edm.String | Ja | Der eindeutige Bezeichner für die Zusammenarbeit. Geerbt von [DirectoryObject]. <br/> <br/> **Notizen**: **Schlüssel**, unveränderlich, lässt keine Nullwerte zu, eindeutig. |

**Navigationseigenschaften**   
Keine

**Hinweis:** geerbte Navigationseigenschaften, die nicht aufgeführt sind, werden nicht unterstützt. Nicht unterstützte Navigationseigenschaften behandelt Anforderungen zurückgeben **400 Bad Request**. 

#### Unterstützte Vorgänge
Die folgenden Vorgänge werden auf Verträge unterstützt (die jeweils verwendete HTTP-Methode steht in Klammern): 

- Lesen (GET)


---

### Geräteentität <a id="DeviceEntity"> </a>
Stellt ein Gerät im Verzeichnis registriert. Erbt von [DirectoryObject].


#### Eigenschaften
**Deklarierte Eigenschaften**

|  Name |  Typ |  Erstellen (POST) |  Lesen (GET) |  Update (PATCH) |   Beschreibung |
|:-------|:-------|:-------|:-------|:-------|:-------|
| accountEnabled | Edm.Boolean | Optional | Filterable | Ja |  |
| alternativeSecurityIds | Sammlung ([AlternativeSecurityId]) | Optional | Filterable | Ja | **Notizen**: lässt keine Nullwerte zu, die **alle** Operator für Filterausdrücke für mehrwertige Eigenschaften; Weitere Informationen erforderlich ist, finden Sie unter [Abfragen unterstützt, Filtern und Paging Optionen].  |
| approximateLastLogonTimeStamp | Edm.DateTime | Optional | Ja | Ja |  |
| deletionTimestamp | Edm.DateTime | Nein | Ja | Nein | Diese Eigenschaft gilt nicht für Geräte und gibt immer **null**. Geerbt von [DirectoryObject].<br/><br/> **Notizen**: erfordert Version 1.5 oder höher.  |
| Geräte-ID | Edm.Guid | Erforderlich | Filterable | Ja |  |
| deviceObjectVersion | Int32 | Optional | Ja | Ja |  |
| deviceOSType | Edm.String | Erforderlich | Ja | Ja | Der Typ des Betriebssystems auf dem Gerät. |
| deviceOSVersion | Edm.String | Erforderlich | Ja | Ja | Die Version des Betriebssystems auf dem Gerät |
| devicePhysicalIds | Collection(EDM.String) | Optional | Filterable | Ja | **Notizen**: lässt keine Nullwerte zu  |
| dirSyncEnabled | Edm.Boolean | Nein | Filterable | Nein | **True,** wenn dieses Objekt, von einem lokalen Verzeichnis synchronisiert wird; **false** Wenn dieses Objekt ursprünglich von einem lokalen Verzeichnis synchronisiert wurde, aber nicht mehr synchronisiert ist; **NULL** wenn dieses Objekt noch nie von einem lokalen Verzeichnis (Standard) synchronisiert wurde. |
| displayName | Edm.String | Erforderlich | Filterable | Ja | Der Anzeigename für das Gerät. |
| isCompliant | Edm.Boolean | Optional | Ja | Ja | **True,** wenn das Gerät mit Richtlinien für Mobile Device Management (MDM); entspricht, andernfalls **false**. |
| IsManaged | Edm.Boolean | Optional | Ja | Ja | **True,** wenn das Gerät von einer app Mobile Device Management (MDM) wie z. B. Intune verwaltet wird, andernfalls wird **false**. |
| lastDirSyncTime | Edm.DateTime | Nein | Filterable | Nein | Der letzten, an dem das Objekt mit dem lokalen Verzeichnis synchronisiert wurde. |
| objectId | Edm.String | Nein | Ja | Nein | Der eindeutige Bezeichner für das Gerät. Geerbt von [DirectoryObject].<br/><br/> **Notizen**: **Schlüssel**, unveränderlich, lässt keine Nullwerte zu, eindeutig.  |
| Objekttyp | Edm.String | Nein | Ja | Nein | Eine Zeichenfolge, die den Objekttyp identifiziert. Für Geräte ist der Wert immer "Gerät". Geerbt von [DirectoryObject] |

**Navigationseigenschaften**
  
|  Name |  Von Multiplizität |  Nach |  Multiplizität |  Beschreibung |
|:-------|:-------|:-------|:-------|:-------|
| registeredOwners | \* | [Benutzer] | \* | Benutzer, die registrierte Besitzer des Geräts sind. |
| registeredUsers | \* | [Benutzer] | \* | Benutzer, die registrierte Benutzer des Geräts sind. |

**Hinweis:** geerbte Navigationseigenschaften, die nicht aufgeführt sind, werden nicht unterstützt. Nicht unterstützte Navigationseigenschaften behandelt Anforderungen zurückgeben **400 Bad Request**. 

#### Unterstützte Vorgänge
Die folgenden Vorgänge werden für Geräte unterstützt (HTTP-Methoden werden in Klammern aufgeführt):

- Erstellen (CREATE)
- Read (Lesen)
- Update (PATCH)
- Löschen (DELETE)

Die folgenden Vorgänge werden für Navigationseigenschaften des Geräts unterstützt. Nicht alle Vorgänge möglicherweise für jede Navigationseigenschaft unterstützt.

- Read (Lesen)
- Aktualisieren (PUT)
- Löschen (DELETE)

Keine Funktionen oder Aktionen sind auf Geräten unterstützt.

---

### DirectoryLinkChange-Entität <a id="DirectoryLinkChangeEntity"> </a>
Ein **DirectoryLinkChange** Objekt im Resultset einer differenziellen Abfrage gibt an, dass eine Eigenschaft eines Kontakts, eines Benutzers zurückgegeben wird, oder eine Gruppe, die durch einen Link dargestellt wird, die seit der letzten differenziellen Abfrage geändert hat. Die **DirectoryLinkChange** Objekt stellt eine Änderung dar, um einen Benutzer oder Kontakt **Manager** Eigenschaft oder eine Änderung an einer Gruppenstatus **Mitglieder** Eigenschaft. Weitere Informationen zu differenziellen Abfragen finden Sie unter [differenzielle Abfrage]. Erbt von [DirectoryObject].
#### Eigenschaften
**Deklarierte Eigenschaften**

|  Name |  Typ |  Lesen (GET) |  Beschreibung |
|:-------|:-------|:-------|:-------|
| associationType | Edm.String | Ja | Eine Zeichenfolge, die den Zuordnungstyp identifiziert, auf dem die Änderung angewendet wird. Der Wert ist "Mitglied" oder "Manager". |
| deletionTimestamp | Edm.DateTime | Ja | Diese Eigenschaft ist nicht gültig für Verzeichnisobjekte für Link ändern und gibt immer **null**. Geerbt von [DirectoryObject].<br/><br/> **Notizen**: erfordert Version 1.5 oder höher.  |
| objectId | Edm.String | Ja | Der eindeutige Bezeichner für den Link Verzeichnis ändern, Objekt. Für **DirectoryLinkChange** -Objekte ist der Wert immer 00000000-0000-0000-0000-000000000000. Geerbt von [DirectoryObject].<br/><br/> **Hinweis: Schlüssel** unveränderlich, lässt keine Nullwerte zu, eindeutig.  |
| Objekttyp | Edm.String | Ja | Eine Zeichenfolge, die den Objekttyp identifiziert. Für **DirectoryLinkChange** -Objekte ist der Wert immer "DirectoryLinkChange". [DirectoryObject] |
| sourceObjectId | Edm.String | Ja | Die Objekt-ID für das Quellobjekt; Beispiel: "7373b0af-d462-406e-ad26-f2bc96d823d8". |
| Objekttyp (Herkunft) | Edm.String | Ja | Eine Zeichenfolge, die den Quellobjekttyp identifiziert. Dies wird eines der folgenden sein: "Group", "User" oder "Contact". |
| sourceObjectUri | Edm.String | Ja | Der URI für das Quellobjekt beispielsweise `"https://graph.windows.net/contoso.com/groups/7373b0af-d462-406e-ad26-f2bc96d823d8"`. |
| targetObjectId | Edm.String | Ja | Die Objekt-ID für das Zielobjekt; Beispiel: "dca803ab-bf26-4753-bf20-e1c56a9c34e2". |
| targetObjectType | Edm.String | Ja | Eine Zeichenfolge, die den Quellobjekttyp identifiziert. Dies wird eines der folgenden sein: "Group", "User" oder "Contact". |
| targetObjectUri | Edm.String | Ja | Der URI für das Zielobjekt; beispielsweise `"https://graph.windows.net/contoso.com/users/dca803ab-bf26-4753-bf20-e1c56a9c34e2"`. |

**Navigationseigenschaften**   
Keine

**Hinweis:** geerbte Navigationseigenschaften, die nicht aufgeführt sind, werden nicht unterstützt. Nicht unterstützte Navigationseigenschaften behandelt Anforderungen zurückgeben **400 Bad Request**. 

---

### DirectoryObject-Entität <a id="DirectoryObjectEntity"> </a>
Stellt ein Azure Active Directory-Objekt. Die **DirectoryObject** Typ ist der Basistyp für die meisten anderen verzeichnisentitätstypen.
#### Eigenschaften
**Deklarierte Eigenschaften**

|  Name |  Typ |  Erstellen (POST) |  Lesen (GET) |  Update (PATCH) |  Beschreibung |
|:-------|:-------|:-------|:-------|:-------|:-------|
| deletionTimestamp | Edm.DateTime | Nein | Ja | Nein | Der Zeitpunkt, an dem das Verzeichnisobjekt gelöscht wurde. Es gilt nur für die Verzeichnisobjekte, die wiederhergestellt werden können. Es wird derzeit nur unterstützt für gelöschte [Anwendung] Objekten; alle anderen Entitäten zurückgeben **null** für diese Eigenschaft.<br/><br/> **Notizen**: erfordert Version 1.5 oder höher.  |
| objectId | Edm.String | Nein | Ja | Nein | Eine Guid, die den eindeutigen Bezeichner für das Objekt ist; z. B. 12345678-9abc-def0-1234-56789abcde.<br/><br/> **Notizen**: **Schlüssel**, unveränderlich, lässt keine Nullwerte zu, eindeutig.  |
| Objekttyp | Edm.String | Nein | Ja | Nein | Eine Zeichenfolge, die den Objekttyp identifiziert. Zum Beispiel für Gruppen, die der Wert immer lautet "Group". |

**Navigationseigenschaften**   

|  Name |  Von Multiplizität |  Nach |  Multiplizität |  Beschreibung |
|:-------|:-------|:-------|:-------|:-------|
| createdObjects | \* | DirectoryObject | \* | Die Verzeichnisobjekte, die vom aktuellen Objekt erstellt wurden. Schreibgeschützt. Erfordert Version 2013-11-08 oder höher. |
| createdOnBehalfOf | \* | DirectoryObject | 0..1 | Das Verzeichnisobjekt, der für dieses Objekt erstellt wurde. Schreibgeschützt. Erfordert Version 2013-11-08 oder höher. |
| manager | \* | DirectoryObject | 0..1 | Dieses Objekt-Manager. Gültig für Benutzer und Kontakte. Ein Benutzer oder ein Kontakt zurückgegeben.  |
| directReports | \* | DirectoryObject | \* | Benutzer und Kontakte, die auf dieses Objekt zu melden. Gültig für Benutzer und Kontakte. Gibt Benutzer und Kontakte. Schreibgeschützt. |
| Mitglieder | \* | DirectoryObject | \* | Objekte, die Member dieses Objekts sind. Gilt für Gruppen und Rollen. Für Gruppen werden Kontakte, Benutzer und Gruppen zurückgegeben. Für Rollen können Sie Benutzer und Dienstprinzipale zurückgegeben. |
| memberOf | \* | DirectoryObject | \* | Objekte, denen dieses Objekt angehört. Gültig für Kontakte, Gruppen, Dienstprinzipale und Benutzer. Für Kontakte und zurückgegeben Gruppen. Für Gruppen werden Gruppen zurückgegeben. Benutzer zurückgegeben Gruppen und Rollen. Dienstprinzipale zurück Rollen Schreibgeschützt.<br/><br/> Die Eigenschaft ist nicht transitiv. Beispielsweise wird, wenn Benutzer A Mitglied der Gruppe B ist und Gruppe B Mitglied der Gruppe C, die MemberOf-Eigenschaft für Benutzer A nicht Gruppe c zurück |
| ownedObjects | \* | DirectoryObject | \* | Die Verzeichnisobjekte, die vom aktuellen Objekt gehören. Schreibgeschützt. Erfordert Version 2013-11-08 oder höher. |
| Besitzer | \* | DirectoryObject | \* | Die Verzeichnisobjekte, die Besitzer des aktuellen Objekts sind. Die Besitzer sind eine Reihe von Benutzern ohne Administratorrechte, die berechtigt sind, dieses Objekt zu ändern. Erfordert Version 2013-11-08 oder höher. |

**Hinweis:** nicht alle Navigationseigenschaften sind zwangsläufig für Entitätstypen, die von erben gültig **DirectoryObject**. Wenn eine Anforderung für eine Eigenschaft, die für eine bestimmte Entität ungültig ist gesendet wird, eine **400 Bad Request** Antwort zurückgegeben. Weitere Informationen darüber, welche Navigationseigenschaften Eigenschaften für bestimmte Entitäten gültig sind, finden Sie in der Dokumentation für diesen Entitätstyp. 

#### Unterstützte Vorgänge
Der vollständige Satz von Vorgängen, die für Verzeichnisobjekte unterstützt werden sind die folgenden (die jeweils verwendete HTTP-Methode steht in Klammern): erstellen (POST), lesen (GET), aktualisieren (PATCH) und löschen (DELETE). Nicht alle diese Vorgänge werden jedoch für jeden Entitätstyp unterstützt. Der deklarierten Eigenschaften des Verzeichnisobjekts sind schreibgeschützt. nicht in angegeben werden, erstellen oder update-Vorgänge.

Die potenziellen Vorgänge, die auf jedem der Navigationseigenschaften unterstützt werden: 

- **CreatedObjects**: Lesen (GET).
- **CreatedOnBehalfOf**: Lesen (GET).
- **Manager**: Lesen (GET), aktualisieren (PUT) und löschen (DELETE).
- **DirectReports**: Lesen (GET). 
- **Mitglieder**: Lesen (GET), aktualisieren (POST) und löschen (DELETE).
- **MemberOf**: Lesen (GET).
- **OwnedObjects**: Lesen (GET).
- **Besitzer**: Lesen (GET), aktualisieren (POST) und löschen (DELETE).

Nicht alle Navigationseigenschaften sind zwangsläufig auf jeder Entitätstyp, noch sind mögliche Vorgänge für eine Navigationseigenschaft, die unbedingt für jeden Entitätstyp unterstützt unterstützt.

Ob ein bestimmtes Verzeichnisobjekt eine bestimmte Aktion oder Funktion unterstützt hängt vom Typ des Verzeichnisobjekts (die **ObjectType** Eigenschaft). Informationen darüber, welche Objekttypen der unterstützen Funktionen oder Aktionen, finden Sie unter der Dokumentation zum jeweiligen Objekt, z. B. Benutzer, Gruppen, usw. oder einer bestimmten Funktion.

Die Dokumentation für den betreffenden Entitätstyp Informationen zu Vorgängen, die für eine Entität unterstützt.

---

### DirectoryRole-Entität <a id="DirectoryRoleEntity"> </a>
Stellt ein Azure AD-Verzeichnis-Funktion. Azure AD-verzeichnisrollen sind auch bekannt als *Administratorrollen*. Weitere Informationen zu Verzeichnisfunktionen (Administrator), finden Sie unter [Zuweisen von Administratorrollen in Azure AD](http://azure.microsoft.com/documentation/articles/active-directory-assign-admin-roles/).

Mit der Graph-API können Sie Benutzer und Dienstprinzipale Directory-Rollen gewähren sie die Berechtigungen der Zielrolle zuweisen. Können Sie Verzeichnisobjekte für die Rolle zu lesen und Aktualisieren der **Member** Navigationseigenschaft Verzeichnisfunktionen jedoch nicht Verzeichnisfunktionen löschen oder ihre deklarierten Eigenschaften aktualisieren. Erbt von [DirectoryObject]. 

Um eine verzeichnisrolle lesen oder Aktualisieren von Membern, müssen sie zuerst im Mandanten aktiviert werden. In Versionen vor der Version 1.5 werden alle verzeichnisrollen standardmäßig aktiviert. Ab Version 1.5, nur die **Unternehmensadministratoren** Directory-Rolle ist standardmäßig aktiviert. Andere Rollen verfügbaren Verzeichnis zu aktivieren, die Sie Senden einer POST-Anforderung mit der **ObjectId** von der [DirectoryRoleTemplate] auf dem die verzeichnisrolle basiert. Finden Sie unter **Vorgänge unterstützt** und **Hinweise** Weitere Informationen.

**Wichtige**: ab Version 1.5, die **Rolle** Entitätstyp wird umbenannt in **DirectoryRole**.
#### Eigenschaften
**Deklarierte Eigenschaften**

| Name | Typ | Erstellen (POST)| Lesen (GET) | Beschreibung |
|:-------|:-------|:-------|:-------|:-------|
| deletionTimestamp | Edm.DateTime | Nein | Ja | Diese Eigenschaft gilt nicht für verzeichnisrollen und gibt immer **null**. Geerbt von [DirectoryObject].<br/><br/> **Notizen**: erfordert Version 1.5 oder höher.  |
| description | Edm.String | Nein | Ja | Die Beschreibung der verzeichnisrolle. |
| displayName | Edm.String | Nein | Ja | Der Anzeigename der verzeichnisrolle.  |
| Zustand | Edm.Boolean | Nein | Ja | **True,** wenn die Rolle eine Systemrolle ist; andernfalls **false**.  |
| objectId | Edm.String | Nein | Ja | Der eindeutige Bezeichner der verzeichnisrolle. Geerbt von [DirectoryObject].<br/><br/> **Notizen**: **Schlüssel**, unveränderlich, lässt keine Nullwerte zu, eindeutig.  |
| Objekttyp | Edm.String | Nein | Ja | Eine Zeichenfolge, die den Objekttyp identifiziert. Für verzeichnisrollen ist der Wert immer "DirectoryRole". Geerbt von [DirectoryObject].<br/><br/> **Hinweis**: In Versionen vor der Version 1.5, wird der Wert "Role" sein.  |
| roleDisabled | Edm.Boolean | Nein | Ja | **true** ist die verzeichnisrolle deaktiviert, andernfalls **false**.  |
| roleTemplateId | Zeichenfolge | Erforderlich | Ja |  Die **ObjectId** von der [DirectoryRoleTemplate] die dieser Rolle basiert. <br/><br/> **Notizen**: In Versionen vor Version 1.5, die Eigenschaft ist schreibgeschützt. In Version 1.5 und höher muss die Eigenschaft beim Aktivieren einer verzeichnisrolle in einem Mandanten mit einer POST-Vorgang angegeben werden. Nachdem die Directory-Rolle aktiviert wurde, ist die Eigenschaft schreibgeschützt.  |

**Navigationseigenschaften**   

|  Name |  Von Multiplizität |  Nach |  Multiplizität |  Beschreibung |
|:-------|:-------|:-------|:-------|:-------|
| Mitglieder | \* | [DirectoryObject]<br/><br/> ([Benutzer] und [ServicePrincipal] werden unterstützt. | \* | Benutzer und Dienstprinzipale, die Mitglied dieser verzeichnisrolle sind. Geerbt von [DirectoryObject].<br/><br/> HTTP-Methoden: GET, POST, DELETE |

**Hinweis:** geerbte Navigationseigenschaften, die nicht aufgeführt sind, werden nicht unterstützt. Nicht unterstützte Navigationseigenschaften behandelt Anforderungen zurückgeben **400 Bad Request**. 

#### Unterstützte Vorgänge
Die folgenden Vorgänge werden für verzeichnisrollen unterstützt (die jeweils verwendete HTTP-Methode steht in Klammern): 

- Erstellen (POST): Wird in Version 1.5 oder höher unterstützt. Aktiviert ein Verzeichnis im Mandanten, die [DirectoryRoleTemplate] anhand der **RoleTemplateId** -Eigenschaft in der Anforderung. Nachdem die Directory-Rolle aktiviert ist, können Sie hinzufügen und Löschen von Benutzern und dienstprinzipalen aus der Rolle.
- Lesen (GET)

Die folgenden Vorgänge werden für Verzeichnis rollennavigationseigenschaften unterstützt: 

- Lesen (GET)
- Aktualisieren (POST)
- Löschen (DELETE)

Für verzeichnisrollen können keine Funktionen oder Aktionen aufgerufen werden; Sie können jedoch [GetMemberObjects] aufrufen, auf einem [Benutzer] oder [ServicePrincipal] bestimmen die Rollenmitgliedschaften Verzeichnis. Beachten Sie, dass diese Funktion für Benutzer, auch die direkten und transitiven Gruppenmitgliedschaften zurückgibt.

#### Hinweise
- In Version 1.5 und höher nur die **Unternehmen Administratoren** Rolle ist aktiviert (und sichtbar) in einem Mandanten standardmäßig. Verwenden Sie den Vorgang zu erstellen (POST), um zusätzliche verzeichnisrollen zu aktivieren. Gibt der Vorgang an die **RoleTemplateId** -Eigenschaft in der Anforderung. Diese Eigenschaft enthält die **ObjectId** von der [DirectoryRoleTemplate] Instanz, die der Rolle entspricht Sie aktivieren möchten. Nach dem Aktivieren der Directory-Rolle können Sie hinzufügen und löschen Sie Benutzer und Dienstprinzipale mit der Graph-API. In Versionen vor der Version 1.5, alle verzeichnisrollen (dargestellt durch die **Rolle** Entität) werden aktiviert, und das Erstellen (POST) Vorgang wird nicht unterstützt.
- Directory-Rollen können mithilfe der Graph-API gelöscht werden. Updates werden unterstützt, auf die **Elemente** nur Navigationseigenschaft. Sowohl hinzufügen und entfernen sind für diese Eigenschaft unterstützt.
- Abfragefilterausdrücke werden nicht für verzeichnisrollen unterstützt.

---

### DirectoryRoleTemplate-Entität <a id="DirectoryRoleTemplateEntity"> </a>
Stellt eine verzeichnisrollenvorlage dar. Eine verzeichnisrollenvorlage gibt die Eigenschaftenwerte einer verzeichnisrolle ([DirectoryRole]). Es ist ein zugeordnetes Verzeichnis Rolle Vorlagenobjekt für jedes Verzeichnis Rollen, die in einem Mandanten aktiviert werden kann. Erbt von [DirectoryObject].

Um eine verzeichnisrolle lesen oder Aktualisieren von Membern, müssen sie zuerst im Mandanten aktiviert werden. In Versionen vor der Version 1.5 werden alle verzeichnisrollen standardmäßig aktiviert. Ab Version 1.5, nur die **Unternehmensadministratoren** Directory-Rolle ist standardmäßig aktiviert. Andere verfügbare verzeichnisrollen aktivieren Sie eine POST-Anforderung senden, die /directoryRoles-Endpunkt die **ObjectId** der Directory Rollenvorlage, die Directory-Rolle ist die Grundlage, gemäß der **RoleTemplateId** Parameter der Anforderung. Weitere Informationen finden Sie unter [DirectoryRole].

**Hinweis**: eine verzeichnisrollenvorlage wird verfügbar gemacht, für die **Benutzer** Directory-Rolle. Die **Benutzer** Directory-Rolle ist implizit und ist in der Directory-Clients nicht sichtbar. Jede [Benutzer] in den Mandanten wird zugewiesen, die dieser Rolle von der Infrastruktur. Die Rolle ist bereits aktiviert. Verwenden Sie diese Vorlage nicht.

**Wichtige**: in Version 1.5 eingeführt.

#### Eigenschaften
**Deklarierte Eigenschaften**

| Name | Typ | Lesen (GET) | Beschreibung |
|:-------|:-------|:-------|:-------|
| description | Edm.String | Ja | Die Beschreibung für die Directory-Rolle festlegen. |
| deletionTimestamp | Edm.DateTime | Ja | Diese Eigenschaft gilt nicht für verzeichnisrollenvorlagen und gibt immer **null**. Geerbt von [DirectoryObject].<br/><br/> **Notizen**: erfordert Version 1.5 oder höher.  |
| displayName | Edm.String |  Ja  | Der Anzeigename der verzeichnisrolle festlegen. |
| objectId | Edm.String |  Ja  | Der eindeutige Bezeichner für die Vorlage. Geerbt von [DirectoryObject]. In Version 1.5 und höher, geben Sie die **ObjectId** der verzeichnisrollenvorlage für die **RoleTemplateId** Aktivieren der Eigenschaft in der POST-Anforderung eine [DirectoryRole] in einem Mandanten. <br/><br/> **Notizen**: **Schlüssel**, unveränderlich, lässt keine Nullwerte zu, eindeutig.  |
| Objekttyp | Edm.String |  Ja  | Eine Zeichenfolge, die den Objekttyp identifiziert. Für Rollenvorlagen lautet der Wert immer "RoleTemplate". Geerbt von [DirectoryObject]. |

**Navigationseigenschaften**   
Keine

**Hinweis:** geerbte Navigationseigenschaften, die nicht aufgeführt sind, werden nicht unterstützt. Nicht unterstützte Navigationseigenschaften behandelt Anforderungen zurückgeben **400 Bad Request**. 

#### Unterstützte Vorgänge
Die folgenden Vorgänge werden für verzeichnisrollenvorlagen unterstützt (HTTP-Methoden werden in Klammern aufgeführt):

- Lesen (GET)

---

###Domänenentität (Vorschau) <a id="DomainEntity"> </a> stellt eine Domäne, die dem Mandanten zugeordnet.

**Wichtige**: nur in der Version Beta verfügbar.
####Eigenschaften **Eigenschaften deklariert**

| Name | Typ | Erstellen<br/>(POST) | Siehe<br/>(GET) | Aktualisieren<br/>(PATCH) | Beschreibung |
| -----|------|--------------|-----------|---------------|------------- |
| authenticationType | Edm.String | Nein | Ja |  | Gibt an, welchen Authentifizierungstyp für die Domäne konfiguriert ist. Der Wert ist "Verwaltet" oder "Federated". |
| availabilityStatus | Edm.String | Nein | Ja  | | Diese Eigenschaft ist immer null, außer wenn die [prüfen] Aktion verwendet wird. Wenn die [überprüfen] Aktion verwendet wird, eine **Domäne** Entität in der Antwort zurückgegeben wird. Die **AvailabilityStatus** Eigenschaft der **Domäne** Entität in der Antwort ist "AvailableImmediately" oder "EmailVerifiedDomainTakeoverScheduled". |
| isAdminManaged | Edm.Boolean | Nein | Ja |  | **false**, sofern die Verwaltung der DNS-Datensatzebene der Domäne zu Office 365 delegiert wurde. Andernfalls **true**.<br/><br/>**Notizen**: lässt keine Nullwerte zu |
| isDefault | Edm.Boolean | Nein | Ja | Ja | Gibt an, ob dies die Standarddomäne ist, die für die Erstellung des Benutzers verwendet wird. Es ist nur eine Standarddomäne pro Unternehmen.<br/><br/>**Notizen**: lässt keine Nullwerte zu |
| isInitial | Edm.Boolean | Nein | Ja |  | Gibt an, ob dies die ursprüngliche Domäne von Microsoft Online Services (companyname.onmicrosoft.com) erstellt wird. Es gibt nur eine anfängliche Domäne pro Unternehmen.<br/><br/>**Notizen**: lässt keine Nullwerte zu |
| isRoot | Edm.Boolean | Nein | Ja |  | Für Unterdomänen stellt dies die Stammdomäne. Nur Stammdomänen überprüft werden müssen, und alle Unterdomänen werden dann automatisch überprüft.<br/><br/>**Notizen**: lässt keine Nullwerte zu |
| isVerified | Edm.Boolean | Nein | Ja |  | Gibt an, ob diese Domäne Überprüfung für den Besitz der Domäne oder nicht abgeschlossen ist.<br/><br/>**Notizen**: lässt keine Nullwerte zu |
| Name | Edm.String | Erforderlich | Filterable |  | Der vollqualifizierte Name der Domäne.<br/><br/>**Notizen**: Key, unveränderlich, lässt keine Nullwerte zu, eindeutig. |
| supportedServices | Collection(EDM.String) | Nein | Ja | Ja | Die Funktionen der Domäne zugewiesen. Kann 0, 1 oder mehrere der folgenden Werte enthalten:<ul><li>"E-Mail"</li><li>"Sharepoint"</li><li>"EmailInternalRelayOnly"</li><li>"OfficeCommunicationsOnline"</li><li>"SharePointDefaultDomain"</li><li>"FullRedelegation"</li><li>"SharePointPublic"</li><li>"OrgIdAuthentication"</li><li>"Yammer"</li><li>"Intune"</li></ul><br/><br/>Die meisten dieser Werte sind schreibgeschützt. Die Werte, die Sie hinzufügen/entfernen können mithilfe der Graph-API umfasst:<ul><li>"E-Mail"</li><li>"OfficeCommunicationsOnline"</li><li>"Yammer"</li></ul><br/><br/>**Notizen**: lässt keine Nullwerte zu |

**Navigationseigenschaften**

Name | Von Multiplizität | Nach | Multiplizität | Beschreibung
-----|-----|-----|-----|-----
serviceConfigurationRecords | * | [DomainDnsRecord] | * | DNS-Einträge, die der Kunde die DNS-Zonendatei der Domäne hinzufügen, bevor die Domäne von Microsoft Online Services verwendet werden kann.
verificationDnsRecords | * | [DomainDnsRecord] | * | DNS-Einträge, die der Kunde die DNS-Zonendatei der Domäne hinzufügen, bevor der Kunde den Besitz Überprüfung der Domäne mit Azure AD abgeschlossen werden kann.

---
 
###DomainDnsRecord-Entität (Vorschau) <a id="DomainDnsRecordEntity"> </a> für alle Domänen im Mandanten möglicherweise erforderlich, um die DNS-Datensätze in die DNS-Zonendatei der Domäne hinzufügen, bevor die Domäne von Microsoft Online Services verwendet werden kann.  Die **DomainDnsRecord** Entität wird verwendet, um diese DNS-Einträge vorhanden. Basis-Entität für [DomainDnsCnameRecord], [DomainDnsMxRecord], [DomainDnsSrvRecord] und [DomainDnsSrvRecord] Entitäten.

**Wichtige**: nur in der Version Beta verfügbar.
####Eigenschaften **Eigenschaften deklariert**

Name | Typ | Siehe<br/>(GET) | Beschreibung
-----|-----|-----|-----
dnsRecordId | Edm.Guid | Ja | Eindeutiger Bezeichner, die dieser Entität zugewiesen werden.<br/><br/>**Notizen**: lässt keine Nullwerte zu
isOptional | Edm.Boolean | Ja | Gibt an, ob dieser Eintrag vom Kunden an den DNS-Host für Microsoft Online Services mit der Domäne ordnungsgemäß konfiguriert werden muss.<br/><br/>**Notizen**: lässt keine Nullwerte zu
Bezeichnung | Edm.String | Ja | Gibt den Wert zu verwenden, wenn der Name des DNS-Datensatzes auf dem DNS-Server zu konfigurieren.
recordType | Edm.String | Ja | Gibt an, welche Art von DNS-Datensatz dieser Entität darstellt. Die folgenden Werte sind möglich:<ul><li>"CName"</li><li>"Mx"</li><li>"Srv"</li><li>"Txt"</li></ul><br/><br/>**Notizen**: Schlüssel
supportedService | Edm.String | Ja | Gibt an, welche Microsoft-Onlinedienst oder die Funktion dieser DNS-Datensatz eine Abhängigkeit aufweist. Die folgenden Werte sind möglich:<ul><li>**ungültig**</li><li>"E-Mail"</li><li>"Sharepoint"</li><li>"EmailInternalRelayOnly"</li><li>"OfficeCommunicationsOnline"</li><li>"SharePointDefaultDomain"</li><li>"FullRedelegation"</li><li>"SharePointPublic"</li><li>"OrgIdAuthentication"</li><li>"Yammer"</li><li>"Intune"</li></ul>
Gültigkeitsdauer (TTL) | Int32 | Ja |  Gibt den Wert zu verwenden, wenn die Eigenschaft (Time-to-live, Ttl) für den DNS-Eintrag auf dem DNS-Server zu konfigurieren.<br/><br/>**Notizen**: lässt keine Nullwerte zu

---
 
###DomainDnsCnameRecord-Entität (Vorschau) <a id="DomainDnsCnameRecordEntity"> </a> stellt einen CNAME-Datensatz, der die DNS-Zonendatei einer bestimmten Domäne in dem Mandanten hinzugefügt werden muss. Geerbt von [DomainDnsRecord] Entität.

**Wichtige**: nur in der Version Beta verfügbar.
####Eigenschaften **Eigenschaften deklariert**

Name | Typ | Siehe<br/>(GET) | Beschreibung
-----|-----|-----|-----
canonicalName | Edm.String | Ja | Gibt den Wert zu verwenden, wenn den kanonischen Name des CNAME-Eintrag auf dem DNS-Server zu konfigurieren.
dnsRecordId | Edm.Guid | Ja | Eindeutiger Bezeichner, die dieser Entität zugewiesen werden.<br/><br/>**Notizen**: lässt keine Nullwerte zu
isOptional | Edm.Boolean | Ja | Gibt an, ob der CNAME-Datensatz vom Kunden an den DNS-Host für Microsoft Online Services mit der Domäne ordnungsgemäß konfiguriert werden muss.<br/><br/>**Notizen**: lässt keine Nullwerte zu
Bezeichnung | Edm.String | Ja | Gibt den Wert zu verwenden, wenn der Name des CNAME-Eintrag auf dem DNS-Server zu konfigurieren.
recordType | Edm.String | Ja | Gibt an, welche Art von DNS-Datensatz dieser Entität darstellt. Der Wert ist immer "CName".<br/><br/>**Notizen**: Schlüssel
supportedService | Edm.String | Ja | Gibt an, welche Microsoft-Onlinedienst oder die Funktion dieser CNAME-Datensatz eine Abhängigkeit aufweist. Die folgenden Werte sind möglich:<ul><li>**ungültig**</li><li>"E-Mail"</li><li>"Sharepoint"</li><li>"EmailInternalRelayOnly"</li><li>"OfficeCommunicationsOnline"</li><li>"SharePointDefaultDomain"</li><li>"FullRedelegation"</li><li>"SharePointPublic"</li><li>"OrgIdAuthentication"</li><li>"Yammer"</li><li>"Intune"</li></ul>
Gültigkeitsdauer (TTL) | Int32 | Ja | Gibt den Wert zu verwenden, wenn die Eigenschaft (Time-to-live, Ttl) CNAME-Datensatz auf dem DNS-Server zu konfigurieren.<br/><br/>**Notizen**: lässt keine Nullwerte zu

---
 
###DomainDnsMxRecord-Entität (Vorschau) <a id="DomainDnsMxRecordEntity"> </a> stellt einen MX-Eintrag, der die DNS-Zonendatei einer bestimmten Domäne in dem Mandanten hinzugefügt werden muss. Geerbt von [DomainDnsRecord] Entität.

**Wichtige**: nur in der Version Beta verfügbar.
####Eigenschaften **Eigenschaften deklariert**

Name | Typ | Siehe<br/>(GET) | Beschreibung
-----|-----|-----|-----
dnsRecordId | Edm.Guid | Ja | Eindeutiger Bezeichner, die dieser Entität zugewiesen werden.<br/><br/>**Notizen**: lässt keine Nullwerte zu
isOptional | Edm.Boolean | Ja | Gibt an, ob dieser MX-Eintrag vom Kunden an den DNS-Host für Microsoft Online Services mit der Domäne ordnungsgemäß konfiguriert werden muss.<br/><br/>**Notizen**: lässt keine Nullwerte zu
Bezeichnung | Edm.String | Ja | Der Wert zu verwenden, wenn die Eigenschaft Alias/Hostname des MX-Eintrag auf dem DNS-Server konfigurieren.
mailExchange | Edm.String | Ja | Wert, der beim Konfigurieren des Antwort / / Zielwert der MX-Eintrag auf dem DNS-Server verwendet werden.
recordType | Edm.String | Ja | Gibt an, welche Art von DNS-Datensatz dieser Entität darstellt. Der Wert ist immer "Mx".<br/><br/>**Notizen**: Schlüssel
Einstellung | Int32 | Ja | Der Wert zu verwenden, wenn die Einstellung/Priority-Eigenschaft von den MX-Eintrag auf dem DNS-Server zu konfigurieren.
supportedService | Edm.String | Ja | Gibt an, welche Microsoft-Onlinedienst oder die Funktion dieser CNAME-Datensatz eine Abhängigkeit aufweist. Die folgenden Werte sind möglich:<ul><li>**ungültig**</li><li>"E-Mail"</li><li>"Sharepoint"</li><li>"EmailInternalRelayOnly"</li><li>"OfficeCommunicationsOnline"</li><li>"SharePointDefaultDomain"</li><li>"FullRedelegation"</li><li>"SharePointPublic"</li><li>"OrgIdAuthentication"</li><li>"Yammer"</li><li>"Intune"</li></ul>
Gültigkeitsdauer (TTL) | Int32 | Ja | Wert für die Time-to-live (Ttl)-Eigenschaft des MX-Eintrag auf dem DNS-Server zu konfigurieren.<br/><br/>**Notizen**: lässt keine Nullwerte zu

---
 
###DomainDnsSrvRecord-Entität (Vorschau) <a id="DomainDnsSrvRecordEntity"> </a> stellt einen SRV-Datensatz, der die DNS-Zonendatei einer bestimmten Domäne in dem Mandanten hinzugefügt werden muss. Geerbt von [DomainDnsRecord] Entität.

**Wichtige**: nur in der Version Beta verfügbar.
####Eigenschaften **Eigenschaften deklariert**

Name | Typ | Siehe<br/>(GET) | Beschreibung
-----|-----|-----|-----
dnsRecordId | Edm.Guid | Ja | Eindeutiger Bezeichner, die dieser Entität zugewiesen werden.<br/><br/>**Notizen**: lässt keine Nullwerte zu
isOptional | Edm.Boolean | Ja | Gibt an, ob dieser SRV-Eintrag vom Kunden an den DNS-Host für Microsoft Online Services mit der Domäne ordnungsgemäß konfiguriert werden muss.<br/><br/>**Notizen**: lässt keine Nullwerte zu
Bezeichnung | Edm.String | Ja | Zu verwendende Wert beim Konfigurieren der **Namen** Eigenschaft der SRV-Eintrag auf dem DNS-Server.
nameTarget | Edm.String | Ja | Zu verwendende Wert beim Konfigurieren der **Ziel** Eigenschaft der SRV-Eintrag auf dem DNS-Server.
port | Int32 | Ja | Zu verwendende Wert beim Konfigurieren der **Port** Eigenschaft der SRV-Eintrag auf dem DNS-Server.
Priorität | Int32 | Ja | Zu verwendende Wert beim Konfigurieren der **Priorität** Eigenschaft der SRV-Eintrag auf dem DNS-Server.
Protokoll | Edm.String | Ja | Zu verwendende Wert beim Konfigurieren der **Protokoll** Eigenschaft der SRV-Eintrag auf dem DNS-Server.
recordType | Edm.String | Ja | Gibt an, welche Art von DNS-Datensatz dieser Entität darstellt. Der Wert ist immer "Srv".<br/><br/>**Notizen**: Schlüssel
Dienst | Edm.String | Ja | Zu verwendende Wert beim Konfigurieren der **Service** Eigenschaft der SRV-Eintrag auf dem DNS-Server.
supportedService | Edm.String | Ja | Gibt an, welche Microsoft-Onlinedienst oder die Funktion dieser SRV-Eintrag eine Abhängigkeit aufweist. Die folgenden Werte sind möglich:<ul><li>**ungültig**</li><li>"E-Mail"</li><li>"Sharepoint"</li><li>"EmailInternalRelayOnly"</li><li>"OfficeCommunicationsOnline"</li><li>"SharePointDefaultDomain"</li><li>"FullRedelegation"</li><li>"SharePointPublic"</li><li>"OrgIdAuthentication"</li><li>"Yammer"</li><li>"Intune"</li></ul>
Gültigkeitsdauer (TTL) | Int32 | Ja | Zu verwendende Wert beim Konfigurieren der **Time-To-Live** Eigenschaft der SRV-Eintrag auf dem DNS-Server.<br/><br/>**Notizen**: lässt keine Nullwerte zu
Gewichtung | Int32 | Ja | Zu verwendende Wert beim Konfigurieren der **Gewicht** Eigenschaft der SRV-Eintrag auf dem DNS-Server.

---
 
###DomainDnsTxtRecord-Entität (Vorschau) <a id="DomainDnsTxtRecordEntity"> </a> stellt einen TXT-Eintrag, der die DNS-Zonendatei einer bestimmten Domäne in dem Mandanten hinzugefügt werden muss. Geerbt von [DomainDnsRecord] Entität.

**Wichtige**: nur in der Version Beta verfügbar.
####Eigenschaften **Eigenschaften deklariert**

Name | Typ | Siehe<br/>(GET) | Beschreibung
-----|-----|-----|-----
dnsRecordId | Edm.Guid | Ja | Eindeutiger Bezeichner, die dieser Entität zugewiesen werden.<br/><br/>**Notizen**: lässt keine Nullwerte zu
isOptional | Edm.Boolean | Ja | Gibt an, ob dieser MX-Eintrag vom Kunden an den DNS-Host für Microsoft Online Services mit der Domäne ordnungsgemäß konfiguriert werden muss.<br/><br/>**Notizen**: lässt keine Nullwerte zu
Bezeichnung | Edm.String | Ja | Der Wert zu verwenden, wenn die Eigenschaft Alias/Hostname des MX-Eintrag auf dem DNS-Server konfigurieren.
recordType | Edm.String | Ja | Gibt an, welche Art von DNS-Datensatz dieser Entität darstellt. Der Wert ist immer "Mx".<br/><br/>**Notizen**: Schlüssel
supportedService | Edm.String | Ja | Gibt an, welche Microsoft-Onlinedienst oder die Funktion dieser CNAME-Datensatz eine Abhängigkeit aufweist. Die folgenden Werte sind möglich:<ul><li>**ungültig**</li><li>"E-Mail"</li><li>"Sharepoint"</li><li>"EmailInternalRelayOnly"</li><li>"OfficeCommunicationsOnline"</li><li>"SharePointDefaultDomain"</li><li>"FullRedelegation"</li><li>"SharePointPublic"</li><li>"OrgIdAuthentication"</li><li>"Yammer"</li><li>"Intune"</li></ul>
Text | Edm.String | Ja |  |        
Gültigkeitsdauer (TTL) | Int32 | Ja | Wert (in Sekunden) verwendet, wenn Sie die Time-To-Live-Eigenschaft von den TXT-Eintrag auf dem DNS-Server konfigurieren.<br/><br/>**Notizen**: lässt keine Nullwerte zu


---
 
###DomainDnsUnavailableRecord-Entität (Vorschau) <a id="DomainDnsUnavailableRecordEntity"> </a> von geerbten [DomainDnsRecord] Entität. Bei einer Abfrage für die Navigationseigenschaft **ServiceConfigurationRecords** für eine [Domäne] Entität, erhalten Sie möglicherweise mindestens eine [DomainDnsCnameRecord], [DomainDnsMxRecord], [DomainDnsSrvRecord] und/oder [DomainDnsTxtRecord] Entitäten. Diese Entitäten anzugeben, welche DNS-Datensätze, die Sie in die Zonendatei der Domäne hinzufügen müssen, bevor die Domäne von Microsoft Online Services verwendet werden kann. Wenn es nicht möglich, diese Entitäten Generieren einer **DomainDnsUnavailableRecord** wird stattdessen der Entität zurückgegeben. 

**Wichtige**: nur in der Version Beta verfügbar.
####Eigenschaften **Eigenschaften deklariert**

Name | Typ | Siehe<br/>(GET) | Beschreibung
-----|-----|-----|-----
description | Edm.String | Ja | Gibt den Grund, warum die **DomainDnsUnavailableRecord** zurückgegeben.

---

### ExtensionProperty-Entität <a id="ExtensionPropertyEntity"> </a>
Ermöglicht es einer Anwendung definieren und verwenden eine Reihe von zusätzlichen Eigenschaften, die ohne die Anwendung einen externen Datenspeicher erfordert die Verzeichnisobjekte (Benutzer, Gruppen, mandantendetails, Geräten, Applikationen und dienstprinzipalen) hinzugefügt werden können. Weitere Informationen zu Erweiterungseigenschaften finden Sie unter [Verzeichnisschemaerweiterungen]. Erbt von [DirectoryObject].

**Wichtige**: **ExtensionProperty** wird in Version 1.5 eingeführt.

#### Eigenschaften
**Deklarierte Eigenschaften**

|  Name |  Typ |  Erstellen (POST) |  Lesen (GET) |  Update (PATCH) |  Beschreibung |
|:-------|:-------|:-------|:-------|:-------|:-------|
| appDisplayName | Edm.String | Nein | Ja | Nein |  |
| Datentyp | Edm.String | Optional | Ja | Ja | Gibt den Typ, der die verzeichniserweiterungseigenschaft hinzugefügt wird. Unterstützte Typen sind: Integer, LargeInteger, DateTime (muss angegeben werden im ISO 8601 - DateTime in UTC gespeichert), Binary, Boolean und String. |
| deletionTimestamp | Edm.DateTime | Nein | Ja  | Nein | Diese Eigenschaft ist nicht gültig für Erweiterungseigenschaften und gibt immer **null**. Geerbt von [DirectoryObject].  |
| objectId | Edm.String | Nein | Ja | Nein | Der eindeutige Bezeichner für den Berechtigungsbereich. Geerbt von [DirectoryObject].<br/><br/> **Notizen**: **Schlüssel**, unveränderlich, lässt keine Nullwerte zu, eindeutig.  |
| Objekttyp | Edm.String | Nein | Ja | Nein | Eine Zeichenfolge, die den Objekttyp identifiziert. Für Erweiterungseigenschaften ist der Wert immer "ExtensionProperty". Geerbt von [DirectoryObject]. |
| Name | Edm.String | Optional | Ja | Ja | Gibt den Anzeigenamen für die verzeichniserweiterungseigenschaft an.<br/><br/> **Notizen**: lässt keine Nullwerte zu.  |
| isSyncedFromOnPremises | Edm.Boolean | Nein | Ja | Nein | Gibt an, ob die Erweiterungseigenschaft aus dem auf lokalen Verzeichnis synchronisiert wird.<br/><br/> **Notizen**: lässt keine Nullwerte zu.  |
| targetObjects | Collection(EDM.String) | Optional | Ja | Ja | Die Verzeichnisobjekte, die die verzeichniserweiterungseigenschaft hinzugefügt wird. Unterstützte Directory-Entitäten, die erweitert werden können, sind: "User", "Group", "TenantDetail", "Device", "Application" und "ServicePrincipal"<br/><br/> **Notizen**: lässt keine Nullwerte zu.  |

**Navigationseigenschaften**   
Keine

**Hinweis:** geerbte Navigationseigenschaften, die nicht aufgeführt sind, werden nicht unterstützt. Nicht unterstützte Navigationseigenschaften behandelt Anforderungen zurückgeben **400 Bad Request**. 

---

### Group-Entität <a id="GroupEntity"> </a>
Ein Azure Active Directory-Gruppe darstellt. Erbt von [DirectoryObject].
#### Eigenschaften
**Deklarierte Eigenschaften**

|  Name |  Typ |  Erstellen (POST) |  Lesen (GET) |  Update (PATCH) |  Beschreibung |
|:-------|:-------|:-------|:-------|:-------|:-------|
| deletionTimestamp | Edm.DateTime | Nein | Ja | Nein | Diese Eigenschaft gilt nicht für Gruppen und gibt immer **null**. Geerbt von [DirectoryObject].<br/><br/> **Notizen**: erfordert Version 1.5 oder höher.  |
| description | Edm.String | Optional | Ja | Ja | Eine optionale Beschreibung für die Gruppe. |
| dirSyncEnabled | Edm.Boolean | Nein | Filterable  | Nein | **True,** wenn dieses Objekt, von einem lokalen Verzeichnis synchronisiert wird; **false** Wenn dieses Objekt ursprünglich von einem lokalen Verzeichnis synchronisiert wurde, aber nicht mehr synchronisiert ist; **NULL** wenn dieses Objekt noch nie von einem lokalen Verzeichnis (Standard) synchronisiert wurde. |
| displayName | Edm.String | Erforderlich | Filterable  | Ja | Der Anzeigename für die Gruppe. Diese Eigenschaft ist erforderlich, wenn eine Gruppe erstellt und während des Updates nicht gelöscht werden kann.  |
| lastDirSyncTime | Edm.DateTime | Nein | Filterable  | Nein | Gibt den letzten, an dem das Objekt mit dem lokalen Verzeichnis synchronisiert wurde. |
| mail | Edm.String | Nein | Filterable  | Nein | Die SMTP-Adresse für die Gruppe ein, z. B. "serviceadmins@contoso.onmicrosoft.com". |
| mailEnabled | Edm.Boolean | Erforderlich | Ja | Ja | Gibt an, ob die Gruppe e-Mail-aktiviert ist. Wenn die **SecurityEnabled** -Eigenschaft ist auch **true**, handelt es sich eine e-Mail-aktivierte Sicherheitsgruppe; andernfalls ist die Gruppe eine Microsoft Exchange-Verteilergruppe. Nur (reine) Sicherheitsgruppen können mithilfe von Azure AD Graph erstellt werden. Aus diesem Grund muss die Eigenschaft festgelegt werden **false** beim Erstellen einer Gruppe nicht aktualisiert werden kann mithilfe von Azure AD Graph. |
| mailNickname | Edm.String | Erforderlich | Filterable  | Ja | Der e-Mail-Alias für die Gruppe. Diese Eigenschaft muss angegeben werden, wenn eine Gruppe erstellt wird. |
| objectId | Edm.String | Nein | Ja | Nein | Der eindeutige Bezeichner für die Gruppe. Geerbt von [DirectoryObject].<br/><br/> **Notizen**: **Schlüssel**, unveränderlich, lässt keine Nullwerte zu, eindeutig.  |
| Objekttyp | Edm.String | Nein | Ja | Nein | Eine Zeichenfolge, die den Objekttyp identifiziert. Bei Gruppen, denen, die der Wert immer "Group". Geerbt von [DirectoryObject]. |
| onPremisesSecurityIdentifier | Zeichenfolge |  | Ja |  | Enthält den lokalen Sicherheitsbezeichner (SID) für die Gruppe, die aus einer lokalen in die Cloud synchronisiert wurde.<br/><br/> **Notizen**: erfordert Version 1.5 oder höher.  |
| provisioningErrors | Sammlung ([ProvisioningError]) | Nein | Ja | Nein | Eine Auflistung von Fehlerdetails, die dieser Gruppe verhindern erfolgreich bereitgestellt wird.<br/><br/> **Notizen**: lässt keine Nullwerte zu.  |
| "proxyAddresses" | Collection(EDM.String) | Nein | Filterable  | Nein | <br/><br/> **Notizen**: lässt keine Nullwerte zu, die **alle** Operator für Filterausdrücke für mehrwertige Eigenschaften; Weitere Informationen erforderlich ist, finden Sie unter [Abfragen unterstützt, Filtern und Paging Optionen].  |
| securityEnabled | Edm.Boolean | Erforderlich | Filterable  | Ja | Gibt an, ob die Gruppe eine Sicherheitsgruppe ist. Wenn auch die MailEnabled-Eigenschaft true ist, ist die Gruppe eine e-Mail-aktivierten Sicherheitsgruppe. Andernfalls ist es eine Sicherheitsgruppe. Nur (reine) Sicherheitsgruppen können mithilfe von Azure AD Graph erstellt werden. Aus diesem Grund muss die Eigenschaft festgelegt werden **true** beim Erstellen einer Gruppe. |

**Navigationseigenschaften**   

|  Name |  Von Multiplizität |  Nach |  Multiplizität |  Beschreibung |
|:-------|:-------|:-------|:-------|:-------|
| Mitglieder | \* | [DirectoryObject]<br/><br/> (Nur [Kontakt], [Gruppe], [ServicePrincipal], und [Benutzer] Objekte werden unterstützt) | \* | Benutzer, Kontakte, Gruppen und Dienstprinzipale, die Mitglieder dieser Gruppe sind. Geerbt von [DirectoryObject].<br/><br/> HTTP-Methoden: GET (wird unterstützt für alle Gruppen), POST (für Sicherheitsgruppen und e-Mail-fähige Sicherheitsgruppen unterstützt), DELETE (wird nur für Sicherheitsgruppen unterstützt) |
| memberOf | \* | [DirectoryObject]<br/><br/> (Nur [Gruppe] Objekte werden unterstützt) | \* | Gruppen, denen diese Gruppe Mitglied ist. Geerbt von [DirectoryObject].<br/><br/> HTTP-Methoden: GET (wird unterstützt für alle Gruppen)  |
| Besitzer | \* | [DirectoryObject] | \* | Der Besitzer der Gruppe. Die Besitzer sind eine Reihe von Benutzern ohne Administratorrechte, die berechtigt sind, dieses Objekt zu ändern. Erfordert Version 2013-11-08 oder höher. Geerbt von [DirectoryObject].<br/><br/> HTTP-Methoden: GET (wird unterstützt für alle Gruppen), POST (für Sicherheitsgruppen und e-Mail-fähige Sicherheitsgruppen unterstützt), DELETE (wird nur für Sicherheitsgruppen unterstützt) |
| appRoleAssignments | \* | [DirectoryObject] | \* | Enthält den Satz von Anwendungen, denen eine Gruppe zugewiesen wird.<br/><br/> **Notizen**: erfordert Version 1.5 oder höher.  |
| extensionProperties | \* | [DirectoryObject] | \* | Enthält die der Anwendung zugeordneten Erweiterungseigenschaften. <br/><br/> **Notizen**: erfordert Version 1.5 oder höher.  |

**Hinweis:** geerbte Navigationseigenschaften, die nicht aufgeführt sind, werden nicht unterstützt. Nicht unterstützte Navigationseigenschaften behandelt Anforderungen zurückgeben **400 Bad Request**. 

#### Unterstützte Vorgänge
Die folgenden Vorgänge werden für Benutzer unterstützt (die jeweils verwendete HTTP-Methode steht in Klammern): 

- Erstellen (POST): Wird nur für Sicherheitsgruppen unterstützt.
- Lesen (GET): Wird für alle Gruppen unterstützt.
- Update (PATCH): Unterstützt nur für Sicherheitsgruppen und e-Mail-aktivierte Sicherheitsgruppen. Nicht alle Eigenschaften können aktualisiert werden.
- Löschen (DELETE): Wird nur für Sicherheitsgruppen unterstützt.

Die folgenden Vorgänge werden für gruppennavigationseigenschaften unterstützt: 

- Lesen (GET): Wird für alle Gruppen unterstützt.
- Aktualisieren (POST): Wird nur für Sicherheitsgruppen und e-Mail-fähige Sicherheitsgruppen unterstützt. (Member und nur der Besitzer.)
- Löschen (DELETE): Wird nur für Sicherheitsgruppen unterstützt. (Member und nur der Besitzer.)

Für Gruppen können die folgenden Aktionen und Funktionen aufgerufen werden:

- [CheckMemberGroups], um die Mitgliedschaft einer Gruppe in einer Liste von Gruppen zu überprüfen. Die Überprüfung ist transitiv.
- [GetAvailableExtensionProperties], um eine Liste der Erweiterungseigenschaften zurückgegeben, die für eine Gruppe registriert wurden. Erfordert Version 1.5 oder höher.
- [GetMemberGroups], um eine Liste der Gruppen zurückzugeben, die eine Gruppe Mitglied ist. Die Überprüfung ist transitiv.
- [IsMemberOf] zu überprüfen, ob eine Gruppe Mitglied einer angegebenen Gruppe ist. Die Überprüfung ist transitiv.

#### Hinweise

- Es gibt drei Arten von Gruppen: e-Mail-Verteilergruppen (**MailEnabled** Eigenschaft **true** und **SecurityEnabled** Eigenschaft **false**); e-Mail-aktivierte Sicherheitsgruppen (**MailEnabled** Eigenschaft **true** und **SecurityEnabled** Eigenschaft **true**); sowie (reine) Sicherheitsgruppen (**MailEnabled** Eigenschaft **false** und **SecurityEnabled** Eigenschaft **true**).
- Sie können nur Sicherheitsgruppen, die die Graph-API (Sie können keine e-Mail-aktivierten Gruppen erstellen oder e-Mail-Verteilergruppen) erstellen. Aus diesem Grund die **MailEnabled** Eigenschaft muss festgelegt werden **false** und **SecurityEnabled** muss **true** beim Erstellen einer Gruppe.
- Alle Eigenschaften, die als erforderlich gekennzeichnet müssen angegeben werden, wenn Sie eine Sicherheitsgruppe, die die Graph-API zu erstellen. Diese Eigenschaften sind: **DisplayName**, **MailNickname**, **MailEnabled** (**false**), **SecurityEnabled** (**true**).
- Eine Gruppe aus einer Sicherheitsgruppe in eine e-Mail-aktivierte Sicherheitsgruppe oder eine e-Mail-Verteilergruppe die Graph-API kann nicht aktualisiert werden.

---

### OAuth2PermissionGrant-Entität <a id="OAuth2PermissionGrantEntity"> </a>
Stellt die delegierten OAuth 2.0-berechtigungsbereiche, die gewährt wurden für eine Anwendung (dargestellt durch einen Dienstprinzipal) als Teil der Benutzer oder Administrator seine Zustimmung dar. 

**Wichtige**: ab Version 1.5, die **Berechtigung** Entitätstyp wird umbenannt in **OAuth2PermissionGrant**. In Versionen vor der Version 1.5, Berechtigungen, die während der Zustimmung erstellt hinzugefügt wurden die **Berechtigungen** Eigenschaft von einem Benutzer oder Dienstprinzipal.
#### Eigenschaften
**Deklarierte Eigenschaften**

| Eigenschaft | Typ | Erstellen (POST) | Lesen (GET) | Update (PATCH) | Beschreibung |
|:-----|:-----|:-----|:-----|:-----|:-----|
| Client-ID | Edm.String | Optional | Ja | Nein | Gibt die **ObjectId** des dienstprinzipals Zustimmung erteilt wurde, einen Identitätswechsel des Benutzers, den Zugriff auf die Ressource (dargestellt durch die **ResourceId**). |
| consentType | Edm.String | Optional | Ja | Nein | Gibt an, ob die Zustimmung vom Administrator im Auftrag der Organisation oder gibt an, ob die Zustimmung durch eine Einzelperson bereitgestellt wurde. Die möglichen Werte sind "allprincipals aufweist" oder "Principal". |
| expiryTime | Edm.DateTime | Optional | Ja | Ja | Reserviert. Gibt **null**. Nicht verwenden. |
| objectId | Edm.String | Nein | Ja | Nein | Der eindeutige Bezeichner für den Berechtigungsbereich.<br/><br/> **Notizen**: **Schlüssel**, lässt keine Nullwerte zu.  |
| principalId | Edm.String | Optional | Ja | Nein | Wenn **ConsentType** "allprincipals" aufweist (dieser Wert ist null, und die Zustimmung gilt für alle Benutzer in der Organisation ist. Wenn **ConsentType** "Prinzipal" ist, gibt diese Eigenschaft die **ObjectId** des Benutzers, die Zustimmung erteilt hat, und gilt nur für diesen Benutzer. |
| Ressourcen-ID | Edm.String | Optional | Ja | Nein | Gibt die **ObjectId** des ressourcendienstprinzipals an, die Zugriff erteilt wurde. |
| Bereich | Edm.String | Optional | Ja | Ja | Gibt den Wert des bereichsanspruchs an, die erwarten, dass die ressourcenanwendung das OAuth 2.0-Zugriffstoken an. |
| Startzeit | Edm.DateTime | Optional | Ja | Nein | Reserviert. Gibt **null**. Nicht verwenden. |

**Navigationseigenschaften**   
Keine

**Hinweis:** geerbte Navigationseigenschaften, die nicht aufgeführt sind, werden nicht unterstützt. Nicht unterstützte Navigationseigenschaften behandelt Anforderungen zurückgeben **400 Bad Request**. 

#### Unterstützte Vorgänge
Die folgenden Vorgänge werden für berechtigungsbereiche unterstützt (die jeweils verwendete HTTP-Methode steht in Klammern): 

- Erstellen (POST)
- Lesen (GET)
- Update (PATCH): **Bereich** nur Eigenschaft.
- Löschen (DELETE)

Für berechtigungsbereiche können keine Funktionen oder Aktionen aufgerufen werden.
####Hinweise
- In Version 1.5 und höher die **oauth2PermissionGrants** Navigationseigenschaft der **Benutzer** Entität und die **ServicePrincipal** Entität gibt die **OAuth2PermissionGrant** Objekte, die dem Benutzer oder Dienstprinzipal zugeordnet.
- Vor der Version 1.5 der **Berechtigungen** Navigationseigenschaft der **Benutzer** Entität und die **ServicePrincipal** Entität gibt die **Berechtigung** Objekte, die dem Benutzer oder Dienstprinzipal zugeordnet.

---

### ServicePrincipal-Entität <a id="ServicePrincipalEntity"> </a>
Eine Instanz einer Anwendung in einem Verzeichnis darstellt. Erbt von [DirectoryObject].
#### Eigenschaften
**Deklarierte Eigenschaften**

|  Name |  Typ |  Erstellen (POST) |  Lesen (GET) |  Update (PATCH) |  Beschreibung |
|:-------|:-------|:-------|:-------|:-------|:-------|
| accountEnabled | Edm.Boolean | Optional | Filterable | Ja | **true** ist das dienstprinzipalkonto aktiviert ist, andernfalls **false**.  |
| appDisplayName | Edm.String | Nein | Ja | Nein | Der Anzeigename, der von der zugehörigen Anwendung bereitgestellt wird. |
| AppID-Element | Edm.Guid | Erforderlich | Filterable | Ja | Der eindeutige Bezeichner für die zugehörige Anwendung (die **AppId** Eigenschaft). |
| appOwnerTenantId | Edm.Guid | Nein | Ja | Nein |  |
| appRoleAssignmentRequired | Edm.Boolean | Optional |  | Ja | Gibt an, ob ein **AppRoleAssignment** für einen Benutzer oder eine Gruppe erforderlich ist, bevor Azure AD ein Benutzer- oder Zugriffstoken für die Anwendung ausstellt.<br/><br/> **Notizen**: erfordert Version 1.5 oder höher, lässt keine Nullwerte zu.  |
| appRoles | Sammlung ([AppRole]) |  | Ja |  | Die Anwendungsrollen, die von der zugehörigen Anwendung bereitgestellt wird. Weitere Informationen finden Sie unter der **AppRoles** Eigenschaftsdefinition auf die [Anwendung] Entität<br/><br/> **Notizen**: erfordert Version 1.5 oder höher, lässt keine Nullwerte zu.  |
| authenticationPolicy |  [ServicePrincipalAuthenticationPolicy]  |  | Ja |  | Nur zur internen Verwendung reserviert. Nicht verwenden. In Version 1.5 entfernt.<br/><br/> **Notizen**: nur Version 2013-11-08 verfügbar.  |
| deletionTimestamp | Edm.DateTime | Nein | Ja | Nein | Diese Eigenschaft gilt nicht für Dienstprinzipale und gibt immer **null**. Geerbt von [DirectoryObject].<br/><br/> **Notizen**: erfordert Version 1.5 oder höher.  |
| displayName | Edm.String | Optional | Filterable | Ja | Der Anzeigename für den Dienstprinzipal. |
| errorUrl | Edm.String | Optional | Ja | Ja |  |
| Homepage | Edm.String | Optional | Ja | Ja | Die URL der Startseite der zugehörigen Anwendung. |
| keyCredentials | Sammlung ([KeyCredential]) | Optional |  | Ja | Die Auflistung der schlüsselanmeldeinformationen, die dem Dienstprinzipal zugeordnet.<br/><br/> **Notizen**: lässt keine Nullwerte zu.  |
| logoutUrl | Edm.String | Optional | Ja | Ja |  |
| oauth2Permissions | Sammlung ([OAuth2Permission]) | Nein | Ja | Nein | Die OAuth 2.0-Berechtigungen, die von der zugehörigen Anwendung bereitgestellt. Weitere Informationen finden Sie unter der **oauth2Permissions** Eigenschaftsdefinition auf die [Anwendung] Entität.<br/><br/> **Notizen**: erfordert Version 1.5 oder höher, lässt keine Nullwerte zu.  |
| objectId | Edm.String | Nein | Ja | Nein | Der eindeutige Bezeichner für den Dienstprinzipal. Geerbt von [DirectoryObject].<br/><br/> **Notizen**: **Schlüssel**, unveränderlich, lässt keine Nullwerte zu, eindeutig.  |
| Objekttyp | Edm.String | Nein | Ja | Nein | Eine Zeichenfolge, die den Objekttyp identifiziert. Für Dienstprinzipale lautet der Wert immer "ServicePrincipal". Geerbt von [DirectoryObject]. |
| passwordCredentials | Sammlung ([PasswordCredential]) | Optional | Ja | Ja | Die Auflistung der Kennwortanmeldeinformationen, die dem Dienstprinzipal zugeordnet.<br/><br/> **Notizen**: lässt keine Nullwerte zu.  |
| preferredTokenSigningKeyThumbprint | Edm.String | Ja | Ja | Ja | Nur zur internen Verwendung reserviert. Schreiben oder auf andere Weise auf diese Eigenschaft nicht. Kann in zukünftigen Versionen entfernt werden.<br/><br/> **Notizen**: erfordert Version 1.5 oder höher.  |
| publisherName | Edm.String | Optional | Filterable | Ja | Der Anzeigename des Mandanten, in dem die zugehörige Anwendung angegeben wird. |
| replyUrls | Collection(EDM.String) | Optional | Ja | Ja | Die URLs, dass Benutzertoken für die Anmeldung mit der zugehörigen Anwendung oder die Umleitung URIs, OAuth 2.0-Autorisierungscodes gesendet werden und Zugriffstoken werden für die zugehörige Anwendung gesendet.<br/><br/> **Notizen**: lässt keine Nullwerte zu.  |
| samlMetadataUrl | Edm.String | Optional | Ja | Ja |  |
| Dienstprinzipalnamen (SPN) | Collection(EDM.String) | Optional | Filterable  | Ja | Die URIs, die zugehörige Anwendung identifizieren. Weitere Informationen finden Sie unter [Anwendungsobjekte und Dienstprinzipalobjekte](https://msdn.microsoft.com/en-us/library/azure/dn132633.aspx).<br/><br/> **Notizen**: lässt keine Nullwerte zu, die **alle** Operator für Filterausdrücke für mehrwertige Eigenschaften; Weitere Informationen erforderlich ist, finden Sie unter [Abfragen unterstützt, Filtern und Paging Optionen].  |
| Tags | Collection(EDM.String) | Optional | Filterable  | Ja | <br/><br/> **Notizen**: lässt keine Nullwerte zu.  |

**Navigationseigenschaften**   

|  Name |  Von Multiplizität |  Nach |  Multiplizität |  Beschreibung |
|:-------|:-------|:-------|:-------|:-------|
| appRoleAssignedTo | \* | [AppRoleAssignment] | \* | Prinzipale (Benutzer, Gruppen und Dienstprinzipale), die diesem Dienstprinzipal zugeordnet sind. Erfordert Version 1.5 oder höher. |
| appRoleAssignments | \* | [AppRoleAssignment] | \* | Clientanwendungen, denen die der Dienstprinzipal zugeordnet ist. Erfordert Version 1.5 oder höher. |
| createdObjects | \* | [DirectoryObject] | \* | Verzeichnisobjekte, die von diesem Dienstprinzipal erstellt. Geerbt von [DirectoryObject]. Erfordert Version 2013-11-08 oder höher. |
| memberOf | \* | [DirectoryObject]<br/><br/> (Nur [DirectoryRole] und [Gruppe] Objekte werden unterstützt) | \* | Rollen und Gruppen, denen diesem Dienstprinzipal direktes Mitglied ist. Geerbt von [DirectoryObject].<br/><br/> HTTP-Methoden: GET |
| oauth2PermissionGrants | \* |  [OAuth2PermissionGrant]  | \* | Benutzeridentitätswechsel, die diesem Dienstprinzipal zugeordnet werden. Erfordert Version 1.5 oder höher. |
| ownedObjects | \* | [DirectoryObject] | \* | Verzeichnisobjekte, die diesem Dienstprinzipal gehören. Geerbt von [DirectoryObject]. Erfordert Version 2013-11-08 oder höher. |
| Besitzer | \* | [DirectoryObject] | \* | Verzeichnisobjekte, die Besitzer dieses dienstprinzipals sind. Die Besitzer sind eine Reihe von Benutzern ohne Administratorrechte, die berechtigt sind, dieses Objekt zu ändern. Geerbt von [DirectoryObject]. Erfordert Version 2013-11-08 oder höher. |
| Berechtigungen | \* | **Berechtigung** | \* | Umbenannt in **oauth2PermissionGrants** in Version 1.5 und höher. In früheren Versionen, die dem Dienstprinzipal zugeordneten Berechtigungen gezeigt wird. Informationen zu den **Berechtigung** Entitätstyp ist, finden Sie unter [OAuth2PermissionGrant]. |

**Hinweis:** geerbte Navigationseigenschaften, die nicht aufgeführt sind, werden nicht unterstützt. Nicht unterstützte Navigationseigenschaften behandelt Anforderungen zurückgeben **400 Bad Request**. 

#### Unterstützte Vorgänge
Die folgenden Vorgänge werden für Dienstprinzipale unterstützt (die jeweils verwendete HTTP-Methode steht in Klammern): 

- Erstellen (POST)
- Lesen (GET)
- Update (PATCH)
- Löschen (DELETE)

Der folgende Vorgang wird für Navigationseigenschaften unterstützt:

- Lesen (GET)

Für Gruppen können die folgenden Aktionen und Funktionen aufgerufen werden:

- [CheckMemberGroups], um einen Dienstprinzipal Mitgliedschaft in einer Liste von Gruppen zu überprüfen. Die Überprüfung ist transitiv.
- [GetMemberGroups], um eine Liste der Gruppen zurückzugeben, die ein Dienstprinzipal Mitglied ist. Die Überprüfung ist transitiv.
- [GetMemberObjects] zum Zurückgeben einer Liste der Gruppen und verzeichnisrollen, denen ein Dienstprinzipal Mitglied ist. Die Überprüfung ist transitiv.

Ein Prinzipal muss in der Rolle Unternehmensadministrator, Vorgänge für Dienstprinzipale ausführen können. 
###Hinweise, müssen Sie festlegen, die **AppId** -Eigenschaft auf die ID einer Anwendung in das Verzeichnis, wenn Sie einen Dienstprinzipal erstellen.

---

### SubscribedSku-Entität <a id="SubscribedSkuEntity"> </a>
Nur der Lesevorgang wird für abonnierte SKUs unterstützt. Erstellen, aktualisieren und löschen werden nicht unterstützt. Abfragefilterausdrücke werden nicht unterstützt. Erbt von [DirectoryObject].
#### Eigenschaften
**Deklarierte Eigenschaften**

| Eigenschaft | Typ | Lesen (GET) | Beschreibung |
|:-----|:-----|:-----|
| capabilityStatus | Edm.String | Ja |  |
| consumedUnits | Int32 | Ja |  |
| deletionTimestamp | Edm.DateTime | Ja | Diese Eigenschaft gilt nicht für abonnierte SKUs und gibt immer **null**. Geerbt von [DirectoryObject].<br/><br/> **Notizen**: erfordert Version 1.5 oder höher.  |
| objectId | Edm.String | Ja | <br/><br/> **Notizen**: **Schlüssel**, lässt keine Nullwerte zu.  |
| prepaidUnits |  [LicenseUnitsDetail]  | Ja |  |
| servicePlans | Sammlung ([ServicePlanInfo]) | Ja | <br/><br/> **Notizen**: lässt keine Nullwerte zu  |
| skuId | Edm.Guid | Ja |  |
| skuPartNumber | Edm.String | Ja |  |

**Navigationseigenschaften**   
Keine

**Hinweis:** geerbte Navigationseigenschaften, die nicht aufgeführt sind, werden nicht unterstützt. Nicht unterstützte Navigationseigenschaften behandelt Anforderungen zurückgeben **400 Bad Request**. 

#### Unterstützte Vorgänge
Die folgenden Vorgänge werden für abonnierte SKUs unterstützt (die jeweils verwendete HTTP-Methode steht in Klammern):

- Lesen (GET)

Abonnierte SKUs stellen keine Navigationseigenschaften bereit. 

Für abonnierte SKUs können keine Funktionen oder Aktionen aufgerufen werden.

---

### TenantDetail-Entität <a id="TenantDetailEntity"> </a>
Stellt einen Azure Active Directory-Mandanten. Nur die Lese- und Aktualisierungsvorgänge werden für Mandanten unterstützt. Erstellen und löschen werden nicht unterstützt. Erbt von [DirectoryOjbect].
#### Eigenschaften
**Deklarierte Eigenschaften**

|  Name |  Typ |  Lesen (GET) |  Update (PATCH) |  Beschreibung |
|:-------|:-------|:-------|:-------|:-------|
| assignedPlans | Sammlung ([AssignedPlan]) | Ja | Nein | Die Auflistung der Dienstpläne, die dem Mandanten zugeordnet.<br/><br/> **Notizen**: lässt keine Nullwerte zu.  |
| Ort | Edm.String |  | Nein |  |
| companyLastDirSyncTime | Edm.DateTime | Ja | Nein | Das Datum und die letzte des Mandanten mit dem lokalen Verzeichnis Synchronisierung. |
| Land | Edm.String | Ja | Nein |  |
| countryLetterCode | Edm.String | Ja | Nein |  |
| deletionTimestamp | Edm.DateTime | Ja | Nein | Diese Eigenschaft gilt nicht für Mandanten und gibt immer **null**. Geerbt von [DirectoryObject].<br/><br/> **Notizen**: erfordert Version 1.5 oder höher.  |
| dirSyncEnabled | Edm.Boolean | Ja | Nein | **True,** wenn dieses Objekt, von einem lokalen Verzeichnis synchronisiert wird; **false** Wenn dieses Objekt ursprünglich von einem lokalen Verzeichnis synchronisiert wurde, aber nicht mehr synchronisiert ist; **NULL** wenn dieses Objekt noch nie von einem lokalen Verzeichnis (Standard) synchronisiert wurde. |
| displayName | Edm.String | Ja | Nein | Der Anzeigename für den Mandanten. |
| marketingNotificationEmails | Collection(EDM.String)  | Ja | Optional | <br/><br/> **Notizen**: lässt keine Nullwerte zu.  |
| objectId | Edm.String | Ja | Nein | Der eindeutige Bezeichner für den Mandanten. Geerbt von [DirectoryObject].<br/><br/> **Notizen**: **Schlüssel**, unveränderlich, lässt keine Nullwerte zu, eindeutig.  |
| Objekttyp | Edm.String | Ja | Nein | Eine Zeichenfolge, die den Objekttyp identifiziert. Für Mandanten ist der Wert immer "Company". Geerbt von [DirectoryObject]. |
| postalCode | Edm.String | Ja | Nein |  |
| preferredLanguage | Edm.String |  | Nein |  |
| provisionedPlans | Sammlung ([ProvisionedPlan]) | Ja | Nein | <br/><br/> **Notizen**: lässt keine Nullwerte zu.  |
| provisioningErrors | Sammlung ([ProvisioningError]) | Ja | Nein | <br/><br/> **Notizen**: lässt keine Nullwerte zu.  |
| Status | Edm.String | Ja | Nein |  |
| Straße | Edm.String | Ja | Nein |  |
| technicalNotificationMails | Collection(EDM.String) | Ja | Optional | <br/><br/> **Notizen**: lässt keine Nullwerte zu.  |
| telephoneNumber | Edm.String | Ja | Nein |  |
| tenantType | Edm.String | Ja | Nein | <br/><br/> **Notizen**: entfernt in Version 1.5 und höher.  |
| verifiedDomains | Sammlung ([VerifiedDomain]) | Ja | Nein | Die Auflistung der Domänen, die diesem Mandanten zugeordnet ist.<br/><br/> **Notizen**: lässt keine Nullwerte zu.  |

**Navigationseigenschaften**   
Keine

**Hinweis:** geerbte Navigationseigenschaften, die nicht aufgeführt sind, werden nicht unterstützt. Nicht unterstützte Navigationseigenschaften behandelt Anforderungen zurückgeben **400 Bad Request**. 

#### Unterstützte Vorgänge
Die folgenden Vorgänge werden für Mandanten unterstützt (die jeweils verwendete HTTP-Methode steht in Klammern): 

- Lesen (GET)
- Update (PATCH). nur die **MarketingNotificationMails** und **TechnicalNotificationMails** Eigenschaften können mithilfe der Graph-API aktualisiert werden.

Mandanten stellen keine Navigationseigenschaften bereit. 

Für Mandanten können keine Funktionen oder Aktionen aufgerufen werden.
####Hinweise

- Erstellen oder Löschen von Mandanten mithilfe der Graph-API.
- Nur die **MarketingNotificationMails** und **TechnicalNotificationMails** Eigenschaften können mithilfe der Graph-API aktualisiert werden.
- Abfragefilterausdrücke werden nicht für Mandanten unterstützt.

---

### Entität "User" <a id="UserEntity"> </a>
Stellt ein Azure AD-Benutzerkonto dar. Erbt von [DirectoryObject].
#### Eigenschaften
**Deklarierte Eigenschaften**

|  Name |  Typ |  Erstellen (POST) |  Lesen (GET) |  Update (PATCH) |  Beschreibung |
|:-------|:-------|:-------|:-------|:-------|:-------|
| accountEnabled | Edm.Boolean | Erforderlich | Filterable | Ja | **true** ist das Konto aktiviert ist, andernfalls **false**. Diese Eigenschaft ist erforderlich, wenn ein Benutzer erstellt wird.  |
| assignedLicenses | Sammlung ([AssignedLicense]) | Optional | Ja | Ja | Die Lizenzen, die dem Benutzer zugewiesen sind.<br/><br/> **Notizen**: lässt keine Nullwerte zu.  |
| assignedPlans | Sammlung ([AssignedPlan]) | Nein | Ja | Nein | Die Pläne, die dem Benutzer zugewiesen sind.<br/><br/> **Notizen**: lässt keine Nullwerte zu.  |
| Ort | Edm.String | Optional | Filterable | Ja | Der Ort, in dem sich der Benutzer befindet. |
| Land | Edm.String | Optional | Filterable | Ja | Das Land/Region, in dem sich der Benutzer befindet; z. B. "US" oder "UK". |
| deletionTimestamp | Edm.DateTime | Nein | Ja | Nein | Diese Eigenschaft gilt nicht für Benutzer und gibt immer **null**. Geerbt von [DirectoryObject].<br/><br/> **Notizen**: erfordert Version 1.5 oder höher.  |
| department | Edm.String | Optional | Filterable | Ja | Der Name der Abteilung, in der der Benutzer arbeitet. |
| dirSyncEnabled | Edm.Boolean | Nein | Filterable | Nein | **True,** wenn dieses Objekt, von einem lokalen Verzeichnis synchronisiert wird; **false** Wenn dieses Objekt ursprünglich von einem lokalen Verzeichnis synchronisiert wurde, aber nicht mehr synchronisiert ist; **NULL** wenn dieses Objekt noch nie von einem lokalen Verzeichnis (Standard) synchronisiert wurde.  |
| displayName | Edm.String | Erforderlich | Filterable | Ja, aber nicht gelöscht werden | Der Name, der im Adressbuch für den Benutzer angezeigt wird. Dies ist normalerweise die Kombination des Benutzers Vorname, mittlere Vornamens und Nachname. Diese Eigenschaft ist erforderlich, wenn ein Benutzer erstellt und während des Updates nicht gelöscht werden kann. |
| facsimileTelephoneNumber | Edm.String | Optional | Ja | Ja | Die Telefonnummer des Benutzers Business Faxgerät. |
| "givenName" | Edm.String | Optional | Filterable  | Ja | Der Vorname (Rufname) des Benutzers. |
| immutableId | Edm.String | Erforderlich, wenn eine verbunddomäne für den UPN verwenden | Filterable | Ja | Diese Eigenschaft wird verwendet, um eine lokale Active Directory-Benutzerkonto in ihrer Azure AD-Benutzerobjekt zuzuordnen. Diese Eigenschaft muss angegeben werden, beim Erstellen eines neuen Benutzerkontos in Graph, wenn Sie eine verbunddomäne für des Benutzers verwenden **UserPrincipalName** (UPN)-Eigenschaft.<br/><br/> **Wichtig:** der **$** und **_** Zeichen können nicht verwendet werden, wenn Sie diese Eigenschaft angeben. <br/><br/> **Notizen**: erfordert Version 2013-11-08 oder höher.  |
| Benutzereigenschaft | Edm.String | Optional | Filterable | Ja | Die Berufsbezeichnung des Benutzers. |
| lastDirSyncTime | Edm.DateTime | Nein | Filterable | Nein | Gibt den letzten, an dem das Objekt mit dem lokalen Verzeichnis synchronisiert wurde. zum Beispiel: "2013-02-16T03:04:54Z"  |
| mail | Edm.String | Optional | Filterable | Nein | Die SMTP-Adresse für den Benutzer, z. B. "jeff@contoso.onmicrosoft.com". |
| mailNickname | Edm.String | Erforderlich | Filterable  | Ja | Der e-Mail-Alias für den Benutzer. Diese Eigenschaft muss angegeben werden, wenn ein Benutzer erstellt wird. |
| mobile | Edm.String | Optional | Ja | Ja | Die primäre Mobilfunknummer des Benutzers. |
| objectId | Edm.Guid | Nein | Ja | Nein | Der eindeutige Bezeichner für den Benutzer. Geerbt von [DirectoryObject].<br/><br/> **Notizen**: **Schlüssel**, unveränderlich, lässt keine Nullwerte zu, eindeutig.  |
| Objekttyp | Edm.String | Nein | Ja | Nein | Eine Zeichenfolge, die den Objekttyp identifiziert. Für Benutzer ist der Wert immer "User". Geerbt von [DirectoryObject]. |
| onPremisesSecurityIdentifier | Edm.String | Nein | Ja | Nein | Enthält den lokalen Sicherheitsbezeichner (SID) für den Benutzer, der lokal in der Cloud synchronisiert wurde.<br/><br/> **Notizen**: erfordert Version 1.5 oder höher.  |
| otherMails | Collection(EDM.String) | Optional | Filterable  | Ja | Eine Liste zusätzlicher e-Mail-Adressen für den Benutzer zum Beispiel: ["bob@contoso.com", "Robert@fabrikam.com"].<br/><br/> **Notizen**: lässt keine Nullwerte zu, die **alle** Operator für Filterausdrücke für mehrwertige Eigenschaften; Weitere Informationen erforderlich ist, finden Sie unter [Abfragen unterstützt, Filtern und Paging Optionen].  |
| passwordPolicies | Edm.String | Optional | Ja | Ja | Gibt die Kennwortrichtlinien für den Benutzer. Dieser Wert ist eine Enumeration mit nur einem möglichen Wert wird "DisableStrongPassword", wodurch schwächere Kennwörter die Standardrichtlinie angegeben werden. "DisablePasswordExpiration" kann auch angegeben werden. Die beiden können zusammen angegeben werden. zum Beispiel: "DisablePasswordExpiration, DisableStrongPassword". |
| passwordProfile |  [PasswordProfile]  | Erforderlich | Ja | Ja | Gibt das kennwortprofil für den Benutzer. Das Profil enthält das Kennwort des Benutzers. Diese Eigenschaft ist erforderlich, wenn ein Benutzer erstellt wird.<br/><br/> Die im Profil enthaltene Kennwort muss die Mindestanforderungen gemäß der **PasswordPolicies** Eigenschaft. Standardmäßig ist ein sicheres Kennwort erforderlich. Weitere Informationen zu den Einschränkungen, die für sichere Kennwörter erfüllt sein müssen, finden Sie unter **Kennwortrichtlinie** unter [Ändern Sie Ihr Kennwort](http://onlinehelp.microsoft.com/office365-enterprises/ff637578.aspx) in der Microsoft Office 365-Hilfeseiten.  |
| physicalDeliveryOfficeName | Edm.String | Optional | Ja | Ja | Der Bürostandort des Benutzers an Business. |
| postalCode | Edm.String | Optional | Ja | Ja | Die Postleitzahl Postadresse des Benutzers. Die Postleitzahl ist für das Land bzw. die Region des Benutzers spezifisch. In den Vereinigten Staaten von Amerika enthält dieses Attribut die Postleitzahl. |
| preferredLanguage | Edm.String | Optional | Ja | Ja | Die bevorzugte Sprache für den Benutzer. Muss es sich um Code nach ISO 639-1 folgen. Beispiel: "En-US". |
| provisionedPlans | Sammlung ([ProvisionedPlan]) | Nein | Ja | Nein | Die Pläne, die für den Benutzer bereitgestellt werden.<br/><br/> **Notizen**: lässt keine Nullwerte zu.  |
| provisioningErrors | Sammlung ([ProvisioningError]) | Nein | Ja | Nein | Eine Auflistung von Fehlerdetails, die diesem Benutzer daran gehindert werden, erfolgreich bereitgestellt wird. |
| "proxyAddresses" | Collection(EDM.String) | Nein | Filterable | Nein | Beispiel: ["SMTP: bob@contoso.com", "smtp: bob@sales.contoso.com"]<br/><br/> **Notizen**: eindeutig, lässt keine Nullwerte zu, die **alle** Operator für Filterausdrücke für mehrwertige Eigenschaften; Weitere Informationen erforderlich ist, finden Sie unter [Abfragen unterstützt, Filtern und Paging Optionen].  |
| sipProxyAddress | Edm.String | Nein | Ja | Nein | Gibt die VoIP IP (VOIP) Session Initiation Protocol (SIP) Adresse für den Benutzer.<br/><br/> **Notizen**: erfordert Version 1.5 oder höher.  |
| Status | Edm.String | Optional | Filterable | Ja | Das Bundesland oder Kanton für die Adresse des Benutzers. |
| streetAddress | Edm.String | Optional | Ja | Ja | Die Straße Arbeitsort des Benutzers. |
| Nachname | Edm.String | Optional | Filterable | Ja | Der Nachname des Benutzers (Familienname oder Nachname).<br/><br/> **Notizen**: gefiltert.  |
| telephoneNumber | Edm.String | Optional | Ja | Ja | Die primäre Telefonnummer Arbeitsort des Benutzers. |
| thumbnailPhoto | Edm.Stream | Optional | Ja | Ja | Ein miniaturfoto für den Benutzer angezeigt werden soll.<br/><br/> **Notizen**: lässt keine Nullwerte zu.  |
| usageLocation | Edm.String | Optional | Filterable | Ja | Ein aus zwei Buchstaben bestehender Ländercode (ISO-standard 3166). Die Benutzer, die Lizenzen aufgrund gesetzlicher Anforderungen zur Überprüfung der Verfügbarkeit von Diensten in Ländern zugewiesen werden. Beispiele hierfür sind: "US", "JP" und "GB".<br/><br/> **Notizen**: lässt keine Nullwerte zu.  |
| "userPrincipalName" | Edm.String | Erforderlich | Filterable | Ja | Der Benutzer Benutzerprinzipalnamen (UPN) des Benutzers. Der UPN ist ein im Internet-Anmeldename des Benutzers auf dem Internetstandard RFC 822 basiert. Gemäß der Konvention sollte dies die e-Mail-Namen des Benutzers entsprechen. Das allgemeine Format ist "alias@domain", wobei Domäne Auflistung überprüfter Domänen des Mandanten muss. Diese Eigenschaft ist erforderlich, wenn ein Benutzer erstellt wird. <br/><br/> Der überprüften Domänen des Mandanten können zugegriffen werden, aus der **VerifiedDomains** -Eigenschaft des [TenantDetail]. <br/><br/> **Notizen**: **Schlüssel**, eindeutig.  |
| Benutzertyp | Edm.String | Optional | Filterable | Ja | Ein Zeichenfolgenwert, der zum Klassifizieren von Benutzertypen in Ihrem Verzeichnis, z. B. "Mitglied" oder "Gast" verwendet werden kann.<br/><br/> **Notizen**: erfordert Version 2013-11-08 oder höher.  |

**Navigationseigenschaften**   

|  Name |  Von Multiplizität |  Nach |  Multiplizität |  Beschreibung |
|:-------|:-------|:-------|:-------|:-------|
| manager | \* | [DirectoryObject]<br/><br/> (Nur Benutzer und [Kontakt] Objekte werden unterstützt.) | 0..1 | Der Benutzer oder Kontakt, der Manager des Benutzers ist. Geerbt von [DirectoryObject].<br/><br/> HTTP-Methoden: GET, PUT, DELETE |
| directReports | \* | [DirectoryObject]<br/><br/> (Nur Benutzer und [Kontakt] Objekte werden unterstützt.) | \* | Die Benutzer und Kontakte, die an den Benutzer melden. (Die Benutzer und Kontakte, die deren Manager-Eigenschaft, die auf diesen Benutzer festgelegt ist.) Geerbt von [DirectoryObject].<br/><br/> HTTP-Methoden: GET |
| memberOf | \* | [DirectoryObject]<br/><br/> (Nur [Gruppe] und [DirectoryRole] Objekte werden unterstützt.) | \* | Die Gruppen und verzeichnisrollen, bei denen der Benutzer Mitglied ist. Geerbt von [DirectoryObject].<br/><br/> HTTP-Methoden: GET |
| ownedDevices | \* |  [Gerät]  | \* | Geräte, die der Benutzer besitzt. |
| Berechtigungen | \* | **Berechtigung** | \* | Die Berechtigungen, die dem Benutzer zugeordnet. Die Eigenschaft wird umbenannt in **oauth2PermissionGrants** und **Berechtigung** Entität wird umbenannt in [OAuth2PermissionGrant] in Version 1.5 und höher. Entnehmen Sie der Dokumentation **OAuth2PermssionGrant** Dokumentation zu den **Berechtigung** Entitätstyp.<br/><br/>  |
| registeredDevices | \* |  [Gerät]  | \* | Geräte, die registriert sind für den Benutzer. |
| createdObjects | \* |  [DirectoryObject]  | \* | Verzeichnisobjekte, die vom Benutzer erstellt wurden. Erfordert Version 2013-11-08 oder höher. |
| ownedObjects | \* |  [DirectoryObject]  | \* | Verzeichnisobjekte, die der Benutzer besitzt. Erfordert Version 2013-11-08 oder höher. |
| appRoleAssignments | \* |  [AppRoleAssignment]  | \* | Der Satz von Programmen, denen diesem Benutzer zugewiesen ist. Erfordert Version 1.5 oder höher.<br/><br/> HTTP-Methoden: GET, POST, DELETE |
| oauth2PermissionGrants | \* |  [OAuth2PermissionGrant]  | \* | Die Sammlung der Anwendungen, die Zustimmung erteilt wurde, um die Identität dieses Benutzers anzunehmen. Erfordert Version 1.5 oder höher.<br/><br/> HTTP-Methoden: GET, POST, DELETE |

**Hinweis:** geerbte Navigationseigenschaften, die nicht aufgeführt sind, werden nicht unterstützt. Nicht unterstützte Navigationseigenschaften behandelt Anforderungen zurückgeben **400 Bad Request**. 

#### Unterstützte Vorgänge
Die folgenden Vorgänge werden für Benutzer unterstützt (die jeweils verwendete HTTP-Methode steht in Klammern): 

- Erstellen (POST)
- Lesen (GET)
- Update (PATCH)
- Löschen (DELETE)

Die folgenden Vorgänge werden für Navigationseigenschaften des Benutzers unterstützt. nicht alle Vorgänge werden für jede Navigationseigenschaft unterstützt.

- Lesen (GET)
- Aktualisieren (PUT)
- Löschen (DELETE)

Benutzer können die folgenden Aktionen und Funktionen aufgerufen werden:

- [AssignLicense] zuweisen und/oder eine angegebene Liste von Lizenzen von einem Benutzer entfernen. Erfordert Version 2013-11-08 oder höher.
- [CheckMemberGroups], um die Mitgliedschaft des Benutzers in einer Liste von Gruppen zu überprüfen. Die Überprüfung ist transitiv.
- [GetAvailableExtensionProperties], um eine Liste der Erweiterungseigenschaften zurückgegeben, die für einen Benutzer registriert wurden. Erfordert Version 1.5 oder höher.
- [GetMemberGroups], um eine Liste der Gruppen zurückzugeben, die ein Benutzer Mitglied ist. Die Überprüfung ist transitiv.
- [GetMemberObjects] zum Zurückgeben einer Liste der Gruppen und verzeichnisrollen, bei denen ein Benutzer Mitglied ist. Die Überprüfung ist transitiv.
- [IsMemberOf] zu überprüfen, ob ein Benutzer Mitglied einer angegebenen Gruppe ist. Die Überprüfung ist transitiv.

####Hinweise

- Sie müssen mindestens die folgenden Eigenschaften angeben, beim Erstellen eines Benutzers: **AccountEnabled**, **DisplayName**, **MailNickname**, **PasswordProfile**, und **UserPrincipalName**. Das Kennwort, die gemäß der **PasswordProfile** Eigenschaft erfüllt die Anforderungen an die Kennwortkomplexität des Mandanten. Weitere Informationen finden Sie unter der **PasswordPolicies** Eigenschaft.
- In Version 2013-11-08 oder höher, die **ImmutableId** -Eigenschaft muss angegeben werden, beim Erstellen eines neuen Benutzerkontos in Graph, wenn Sie eine verbunddomäne für des Benutzers verwenden **UserPrincipalName** (UPN)-Eigenschaft.
- Die **DisplayName** Eigenschaft kann nicht für Updates gelöscht werden.
- Die **PasswordProfile** -Eigenschaft gibt immer **null**. Dadurch wird verhindert, dass das Kennwort des Benutzers angezeigt wird. Sie können das Benutzerkennwort zurücksetzen, durch die Aktualisierung der **PasswordProfile** Eigenschaft.
- Zusätzlich zur standardadressierung für alle verzeichnisentitäten verfügbar Benutzer möglicherweise adressiert werden mithilfe der **UserPrincipalName** Eigenschaft, z. B. `https://graph.windows.net/contoso.onmicrosoft.com/users/john@contoso.onmicrosoft.com?api-version=1.5`.

---

## Referenz zum komplexen Typ

### AlternativeSecurityId-Typ <a id="AlternativeSecurityIdType"> </a>
Enthält eine alternative Sicherheits-ID, die einem Gerät zugeordnet. Die **AlternativeSecurityIds** Eigenschaft der [Gerät] Entität ist eine Sammlung von **AlternativeSecurityId**.
#### Eigenschaften

|  Name |  Typ |  Hinweise |  Lesen/Schreiben |  Beschreibung |
|:-------|:-------|:-------|:-------|:-------|
| identityProvider | Edm.String |  |  |  |
| Schlüssel | Edm.Binary |  |  |  |
| type | Int32 |  |  |  |

---

### AppRole-Typ <a id="AppRoleType"> </a>
Stellt eine Anwendungsrolle, die möglicherweise von einer Clientanwendung Aufrufen einer anderen Anwendung dazu aufgefordert werden oder, die verwendet werden kann, eine Anwendung für Benutzer oder Gruppen in einer angegebenen Rolle zugewiesen. Die **AppRoles** Eigenschaft der [ServicePrincipal] Entität und die [Anwendung] Entität ist eine Sammlung von **AppRole**.

**Wichtige**: erfordert Version 1.5 oder höher.
#### Eigenschaften

|  Name |  Typ |  Hinweise |  Lesen/Schreiben |  Beschreibung |
|:-------|:-------|:-------|:-------|:-------|
| allowedMemberTypes | Collection(EDM.String) | Lässt keine Nullwerte zu | RW | Gibt an, ob diese app-Rollendefinition, um Benutzer und Gruppen durch die Einstellung "Benutzer" oder anderen Programmen zugewiesen wird (, die diese Anwendung in daemondienstszenario zugreifen) durch Einstellung auf "Application" oder beides. |
| description | Edm.String  |  | RW | Berechtigung zur administratorzustimmung und Hilfetext, die in der app-Zuordnung angezeigt. |
| displayName | Edm.String |  | RW | Der Anzeigename für die Berechtigung, die in der app und Zustimmung Zuordnung angezeigt wird. |
| ID | Edm.Guid |  | RW | Eindeutiger Rollenbezeichner in der **AppRoles** Auflistung. |
| isEnabled | Edm.Boolean |  | RW | Beim Erstellen oder Aktualisieren einer Rollendefinition, muss dies auf festgelegt werden **true** (Dies ist die Standardeinstellung). Um eine Rolle zu löschen, dies muss zuerst festgelegt werden **false**. An diesem Punkt kann in einem nachfolgenden Aufruf dieser Rolle entfernt werden. |
| Wert | Edm.String |  | RW | Gibt den Wert des rollenanspruchs, die erwarten, dass die Anwendung in den Token-Authentifizierung und Zugriff. |

---

### AssignedLicense-Typ <a id="AssignedLicenseType"> </a>
Stellt eine einem Benutzer zugewiesene Lizenz dar. Die **AssignedLicenses** Eigenschaft der [Benutzer] Entität ist eine Sammlung von **AssignedLicense**.
####Eigenschaften

|  Name |  Typ |  Hinweise |  Lesen/Schreiben |  Beschreibung |
|:-------|:-------|:-------|:-------|:-------|
| disabledPlans | Collection(EDM.GUID) | Lässt keine Nullwerte zu | R | Eine Auflistung der eindeutige Bezeichner für Pläne, die deaktiviert wurden. |
| skuId | Edm.Guid |  | R | Der eindeutige Bezeichner für die SKU. |

---

### AssignedPlan-Typ <a id="AssignedPlanType"> </a>
Die **AssignedPlans** -Eigenschaft beider der [Benutzer] Entität und die [TenantDetail] Entität ist eine Sammlung von **AssignedPlan**.
####Eigenschaften

|  Name |  Typ |  Hinweise |  Lesen/Schreiben |  Beschreibung |
|:-------|:-------|:-------|:-------|:-------|
| assignedTimestamp | Edm.DateTime |  | R | Datum und Uhrzeit, an dem der Plan zugeordnet wurde; zum Beispiel: 2013-01-02T19:32:30Z. |
| capabilityStatus | Edm.String |  | R | Beispielsweise aktiviert. |
| Dienst | Edm.String |  | R | Den Namen des Diensts auf. z. B. "AccessControlServiceS2S". |
| servicePlanId | Edm.Guid |  | R | Eine GUID, die Dienstplan identifiziert. |

---

### KeyCredential-Typ <a id="KeyCredentialType"> </a>
Enthält die schlüsselanmeldeinformationen einer Anwendung oder einem Dienstprinzipal zugeordnet. Die **KeyCredentials** Eigenschaft der [Anwendung] und [ServicePrincipal] ist eine Auflistung von **KeyCredential**.
#### Eigenschaften

|  Name |  Typ |  Hinweise |  Lesen/Schreiben |  Beschreibung |
|:-------|:-------|:-------|:-------|:-------|
| customKeyIdentifier | Edm.Binary |  |  |  |
| Enddatum | Edm.DateTime |  |  | Das Datum und die Uhrzeit des Ablaufs der Anmeldeinformationen. |
| Schlüssel-ID | Edm.Guid |  |  | Der eindeutige Bezeichner (GUID) für den Schlüssel. |
| startDate | Edm.DateTime |  |  | Das Datum und die Uhrzeit, an dem die Anmeldeinformationen gültig. |
| type | Edm.String |  |  | Der Typ der Schlüssel. Beispielsweise ist "Symmetric". |
| Verwendung | Edm.String |  |  | Eine Zeichenfolge, die den Zweck beschreibt, für den der Schlüssel verwendet werden kann. z. B. "Überprüfen". |
| Wert | Edm.String |  |  |  |

---

### LicenseUnitsDetail-Typ <a id="LicenseUnitsDetailType"> </a>
Die **PrepaidUnits** Eigenschaft der [SubscribedSku] Entität ist vom Typ **LicenseUnitsDetail**.
#### Eigenschaften

|  Name |  Typ |  Hinweise |  Lesen/Schreiben |  Beschreibung |
|:-------|:-------|:-------|:-------|:-------|
| aktiviert | Int32 |  |  |  |
| angehalten | Int32 |  |  |  |
| Warnung | Int32 |  |  |  |

---

### OAuth2Permission-Typ <a id="OAuth2PermissionType"> </a>
Stellt ein OAuth 2.0 delegierte Berechtigungsbereich. Der angegebene OAuth 2.0-Bereiche für Delegierte Berechtigung von Clientanwendungen angefordert werden können (über die **RequiredResourceAccess** Auflistung auf die [Anwendung] Objekt), wenn eine ressourcenanwendung aufgerufen. Die **oauth2Permissions** Eigenschaft der [ServicePrincipal] Entität und die [Anwendung] Entität ist eine Sammlung von **OAuth2Permission**.

**Wichtige**: erfordert Version 1.5 oder höher.
#### Eigenschaften
|  Name |  Typ |  Hinweise |  Lesen/Schreiben |  Beschreibung |
|:-------|:-------|:-------|:-------|:-------|
| adminConsentDescription | Edm.String |  | RW | Berechtigungshilfetext, der in der app und Zustimmung Zuordnung angezeigt wird. |
| adminConsentDisplayName | Edm.String |  | RW | Der Anzeigename für die Berechtigung, die in der app und Zustimmung Zuordnung angezeigt wird. |
| ID | Edm. GUID |  | RW | Bezeichner für eindeutigen Bereich innerhalb der oauth2Permissions-Auflistung. |
| isEnabled | Edm.Boolean | Lässt keine Nullwerte zu | RW | Beim Erstellen oder Aktualisieren einer Berechtigung, muss diese Eigenschaft festgelegt werden, um **true** (Dies ist die Standardeinstellung). Um eine Berechtigung zu löschen, muss diese Eigenschaft zunächst auf festgelegt werden **false**. An diesem Punkt kann die Berechtigung in einem nachfolgenden Aufruf entfernt werden. |
| type | Edm.String |  | RW | Gibt an, ob diesem Berechtigungsbereich, durch einen Endbenutzer zugestimmt werden kann oder ob es eine mandantenweite Berechtigung handelt, die durch einen Unternehmensadministrator zugestimmt werden muss. Mögliche Werte sind "User" oder "Admin". |
| userConsentDescription | Edm.String |  | RW | Berechtigungshilfetext, der in der Benutzeroberfläche zur Zustimmung angezeigt wird. |
| userConsentDisplayName | Edm.String |  | RW | Der Anzeigename für die Berechtigung, die in der Benutzeroberfläche zur Zustimmung angezeigt wird. |
| Wert | Edm.String |  | RW | Der Wert des bereichsanspruchs an, die die ressourcenanwendung im OAuth 2.0-Zugriffstoken erwarten. |

---

### PasswordCredential-Typ <a id="PasswordCredentialType"> </a>
Enthält die Kennwortanmeldeinformationen einer Anwendung oder einem Dienstprinzipal zugeordnet. Die **PasswordCredentials** Eigenschaft der [ServicePrincipal] Entität und die [Anwendung] Entität ist eine Sammlung von **PasswordCredential**.
#### Eigenschaften

|  Name |  Typ |  Hinweise |  Lesen/Schreiben |  Beschreibung |
|:-------|:-------|:-------|:-------|:-------|
| customKeyIdentifier | Edm.Binary |  |  |  |
| Enddatum | Edm.DateTime |  |  | Datum und Uhrzeit, an dem das Kennwort abläuft. |
| Schlüssel-ID | Edm.Guid |  |  |  |
| startDate | Edm.DateTime |  |  | Das Datum und die Uhrzeit, an dem das Kennwort gültig. |
| Wert | Edm.String |  |  |  |

---

### PasswordProfile-Typ <a id="PasswordProfileType"> </a>
Enthält das kennwortprofil, das einem Benutzer zugeordnet. Die **PasswordProfile** Eigenschaft der [Benutzer] Entität ist ein **PasswordProfile** Objekt.
####Eigenschaften

|  Name |  Typ |  Hinweise |  Lesen/Schreiben |  Beschreibung |
|:-------|:-------|:-------|:-------|:-------|
| Kennwort | Edm.String |  | RW | Das Kennwort für den Benutzer. Diese Eigenschaft ist erforderlich, wenn ein Benutzer erstellt wird. Kann aktualisiert werden, aber der Benutzer das Kennwort bei der nächsten Anmeldung ändern muss. <br/><br/> Das Kennwort muss die Mindestanforderungen gemäß des Benutzers erfüllen **PasswordPolicies** Eigenschaft. Standardmäßig ist ein sicheres Kennwort erforderlich. |
| forceChangePasswordNextLogin | Edm.Boolean |  | RW | **True,** wenn der Benutzer das Kennwort bei der nächsten Anmeldung ändern muss andernfalls **false**.  |

---

### ProvisionedPlan-Typ <a id="ProvisionedPlanType"> </a>
Die **ProvisionedPlans** Eigenschaft der [Benutzer] Entität und die [TenantDetail] Entität ist eine Sammlung von **ProvisionedPlan**.
#### Eigenschaften
|  Name |  Typ |  Hinweise |  Lesen/Schreiben |  Beschreibung |
|:-------|:-------|:-------|:-------|:-------|
| capabilityStatus | Edm.String |  | R | Beispielsweise aktiviert. |
| provisioningStatus | Edm.String |  | R | Beispiel: "Success". |
| Dienst | Edm.String |  | R | Den Namen des Diensts auf. zum Beispiel "AccessControlS2S" |

---

### ProvisioningError-Typ <a id="ProvisioningErrorType"> </a>
Die **ProvisioningErrors** Eigenschaft der [Kontakt], [Benutzer], und [Gruppe] ist eine Auflistung von **ProvisioningError**.
#### Eigenschaften

|  Name |  Typ |  Hinweise |  Lesen/Schreiben |  Beschreibung |
|:-------|:-------|:-------|:-------|:-------|
| "errordetail" | Edm.String |  | R | Eine Beschreibung des Fehlers. |
| aufgelöst | Edm.Boolean |  | R | **True,** wenn der Fehler gelöst; andernfalls wurde **false**.  |
| serviceInstance | Edm.String |  | R | Die Dienstinstanz, bei der der Fehler aufgetreten ist.  |
| Zeitstempel | Edm.DateTime |  | R | Datum und Uhrzeit, an dem der Fehler aufgetreten ist. |

---

### RequiredResourceAccess-Typ <a id="RequiredResourceAccessType"> </a>
Gibt den Satz der OAuth 2.0-berechtigungsbereiche und app-Rollen unter der angegebenen Ressource, der eine Anwendung Zugriff benötigt. Die angegebenen OAuth 2.0-berechtigungsbereiche werden ggf. von Clientanwendungen angefordert (über die **RequiredResourceAccess** Auflistung), wenn eine ressourcenanwendung aufgerufen. Die **RequiredResourceAccess** Eigenschaft der [Anwendung] Entität ist eine Sammlung von **ReqiredResourceAccess**.

**Wichtige**: erfordert Version 1.5 oder höher.
#### Eigenschaften

|  Name |  Typ |  Hinweise |  Lesen/Schreiben |  Beschreibung |
|:-------|:-------|:-------|:-------|:-------|
| resourceAppId | Edm.String |  | RW | Der eindeutige Bezeichner für die Ressource, der die Anwendung Zugriff benötigt. Das sollte gleich der **AppId** für die zielressourcenanwendung deklariert. |
| resourceAccess | Sammlung ([ResourceAccess]) | Lässt keine Nullwerte zu | RW | Die Liste der OAuth2.0-berechtigungsbereiche und app-Rollen, die die Anwendung aus der angegebenen Ressource benötigt. |

---

### ResourceAccess-Typ <a id="ResourceAccessType"> </a>
Gibt einen OAuth 2.0-Berechtigungsbereich oder eine app-Rolle, die eine Anwendung benötigt. Die **ResourceAccess** Eigenschaft der [RequiredResourceAccess] Typ ist eine Sammlung von **ResourceAccess**.

**Wichtige**: erfordert Version 1.5 oder höher.
#### Eigenschaften

|  Name |  Typ |  Hinweise |  Lesen/Schreiben |  Beschreibung |
|:-------|:-------|:-------|:-------|:-------|
| ID | Edm.Guid | Lässt keine Nullwerte zu | RW | Der eindeutige Bezeichner für eine von der [OAuth2Permission] oder [AppRole] -Instanzen, die die ressourcenanwendung bereitstellt. |
| type | Edm.String  | | RW | Gibt an, ob die **Id** Eigenschaftenverweise ein [OAuth2Permission] oder [AppRole]. Mögliche Werte sind "Scope" oder "Role". |

---

### ServicePlanInfo-Typ <a id="ServicePlanInfoType"> </a>
Enthält Informationen zu einem Dienstplan, der einer abonnierten SKU zugeordnet. Die **ServicePlans** Eigenschaft der [SubscribedSku] Entität ist eine Sammlung von **ServicePlanInfo**.
#### Eigenschaften

|  Name |  Typ |  Hinweise |  Lesen/Schreiben |  Beschreibung |
|:-------|:-------|:-------|:-------|:-------|
| servicePlanId | Edm.Guid |  |  | Der eindeutige Bezeichner des Service-Plans. |
| servicePlanName | Edm.String |  |  | Der Name des Service-Plans. |

---

### ServicePrincipalAuthenticationPolicy-Typ <a id="ServicePrincipalAuthenticationPolicyType"> </a>
Enthält die Authentifizierungsrichtlinie eines dienstprinzipals.

**Wichtige**: nur in Version 2013-11-08; verfügbar, aber es nur zur internen Verwendung reserviert ist und wird in Version 1.5 und höher entfernt.
#### Eigenschaften

|  Name |  Typ |  Hinweise |  Lesen/Schreiben |  Beschreibung |
|:-------|:-------|:-------|:-------|:-------|
| defaultPolicy | Edm.String |  | R/W | Nur zur internen Verwendung reserviert. Nicht verwenden. In Version 1.5 entfernt. |
| allowedPolicies | Collection(EDM.String) | Lässt keine Nullwerte zu | R/W | Nur zur internen Verwendung reserviert. Nicht verwenden. In Version 1.5 entfernt. |

---

### VerifiedDomain-Typ <a id="VerifiedDomainType"> </a>
Gibt eine Domäne für einen Mandanten. Die **VerifiedDomains** Eigenschaft der [TenantDetail] Entität ist eine Sammlung von **VerifiedDomain**.
####Eigenschaften

|  Name |  Typ |  Hinweise |  Lesen/Schreiben |  In BPOS_API |  Beschreibung |
|:-------|:-------|:-------|:-------|:-------|:-------|
| Funktionen | Edm.String |  | R | Ja | Beispielsweise "Email", "OfficeCommunicationsOnline". |
| Standard | Edm.Boolean |  | R | Ja | **True,** wenn dies die Standarddomäne, die dem Mandanten zugeordnet ist, andernfalls **false**.  |
| ID | Edm.String |  | R | Ja | Beispiel: "00057FFE80187238". |
| anfängliche | Edm.Boolean |  | R | Ja |  |
| Name | Edm.String |  | R | Ja | Der Domänenname; z. B. "contoso.onmicrosoft.com" |
| type | Edm.String |  | R | Ja | Z. B. verwaltet"." |

##Zusätzliche Ressourcen

- Erfahren Sie mehr über die Graph-API-Funktionen, Funktionen und Features der Vorschauversion in [Graph-API-Konzepte] unterstützt


[Anwendung]: #ApplicationEntity
[AppRoleAssignment]: #AppRoleAssignmentEntity
[Wenden Sie sich an]: #ContactEntity
[Vertrag]: #ContractEntity
[Gerät]: #DeviceEntity
[DirectoryLinkChange]: #DirectoryLinkChangeEntity
[DirectoryObject]: #DirectoryObjectEntity
[DirectoryRole]: #DirectoryRoleEntity
[DirectoryRoleTemplate]: #DirectoryRoleTemplateEntity
[Domain]: #DomainEntity
[DomainDnsRecord]: #DomainDnsRecordEntity
[DomainDnsCnameRecord]: #DomainDnsCnameRecordEntity
[DomainDnsMxRecord]: #DomainDnsMxRecordEntity
[DomainDnsSrvRecord]: #DomainDnsSrvRecordEntity
[DomainDnsTxtRecord]: #DomainDnsTxtRecordEntity
[DomainDnsUnavailableRecord]: #DomainDnsUnavailableRecordEntity
[ExtensionProperty]: #ExtensionPropertyEntity
[Gruppe]: #GroupEntity
[OAuth2PermissionGrant]: #OAuth2PermissionGrantEntity
[ServicePrincipal]: #ServicePrincipalEntity
[SubscribedSku]: #SubscribedSkuEntity
[TenantDetail]: #TenantDetailEntity
[Benutzer]: #UserEntity

[AlternativeSecurityId]: #AlternativeSecurityIdType
[AppRole]: #AppRoleType
[AssignedLicense]: #AssignedLicenseType
[AssignedPlan]: #AssignedPlanType
[KeyCredential]: #KeyCredentialType
[LicenseUnitsDetail]: #LicenseUnitsDetailType
[OAuth2Permission]: #OAuth2PermissionType
[PasswordCredential]: #PasswordCredentialType
[PasswordProfile]: #PasswordProfileType
[ProvisionedPlan]: #ProvisionedPlanType
[ProvisioningError]: #ProvisioningErrorType
[RequiredResourceAccess]: #RequiredResourceAccessType
[ResourceAccess]: #ResourceAccessType
[ServicePlanInfo]: #ServicePlanInfoType
[ServicePrincipalAuthenticationPolicy]: #ServicePrincipalAuthenticationPolicyType
[VerifiedDomain]: #VerifiedDomainType
    
[Graph-API-Schnellstart auf Azure auf Azure.com]: https://azure.microsoft.com/documentation/articles/active-directory-graph-api-quickstart/


<!--HONumber=May16_HO4-->


